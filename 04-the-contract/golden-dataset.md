# Golden Dataset & Reliability Contract

## Golden Dataset Spec

Golden Dataset — Medispring AI Features (Module: AI, v1)
 
Feature legend: **F1** Consultation capture (record / transcribe / note / translate) · **F2** Prescription assistance · **F3** Patient-file monitoring (insights / prevention)
 
## Test cases
 
### F1 — Consultation capture
 
1. Edge: N · Judge: LLM, IN: 12-min GP consultation audio (FR); patient reports cough + fever, onset 3 days ago → OUT: Structured SOAP note in FR; chief complaint, symptom, and duration all captured, no invented findings
2. Edge: Y · Judge: both, IN: Code-switching consultation — doctor speaks FR, patient answers in NL → OUT: Transcript preserves both languages; note generated in doctor's default language (FR); no NL content dropped
3. Edge: Y · Judge: rule, IN: 4-second inaudible segment mid-consultation → OUT: Segment marked `[inaudible]`; no fabricated clinical content inserted to fill the gap
4. Edge: N · Judge: rule, IN: Patient mentions non-clinical PII during consult (employer name, home address) → OUT: Excluded from the clinical note body
### F2 — Prescription assistance
 
5. Edge: N · Judge: rule, IN: Active medication list includes warfarin; consultation indicates analgesia needed for back pain → OUT: NSAID (ibuprofen) blocked/flagged for interaction; paracetamol surfaced as alternative
6. Edge: N · Judge: rule, IN: Recorded allergy to penicillin; consultation indicates bacterial infection → OUT: Amoxicillin blocked (contraindication); non-beta-lactam alternative surfaced
7. Edge: Y · Judge: rule, IN: Pediatric patient, weight 14 kg, antibiotic indicated → OUT: Weight-based pediatric dose calculated; standard adult dose flagged as unsafe
8. Edge: N · Judge: both, IN: Uncomplicated cystitis, no allergies, no renal flags → OUT: First-line agent per BCFI/CBIP guidance suggested with standard course length
### F3 — Patient-file monitoring
 
9. Edge: N · Judge: rule, IN: HbA1c results 6.1% → 6.3% → 6.5% across last 3 visits, no diabetes diagnosis on file → OUT: Prediabetes signal raised; confirmatory screening suggested
10. Edge: Y · Judge: rule, IN: All vitals/labs within range, no risk factors, preventive screenings up to date → OUT: No alert generated (true-negative control — tests against over-alerting)
## Dataset health
 
- Total: 10
- Edge cases: 4 (40.0%)
- Judge mix: 70% rule / 10% LLM / 20% both
- Feature spread: F1 4 / F2 4 / F3 2
- True negatives: 2 (rows 4, 10)

## Confidence UX Design
Feature: Prescription assistance (F2) — drug suggestion from consultation data
 
**Approach:** Tiered confidence with a mandatory practitioner gate — the AI *proposes*, never prescribes. The visible treatment of the proposal (pre-fill → suggest → withhold) shifts by confidence, every guideline-backed suggestion cites its source, and the language softens as confidence drops.
 
**Confident (>90%):** Pre-fill drug, dose, and duration with a one-line rationale and the BCFI/CBIP source cited; drivers collapsed but one-tap expandable. The practitioner must still confirm before it enters the prescription — no silent auto-commit at any confidence level.
 
**Uncertain (50–90%):** Present as a suggestion, not a pre-fill, in softened copy ("Consider…", "Possible option:"). Surface the competing options and what is driving the uncertainty (e.g. incomplete allergy history, ambiguous indication), showing both the supporting and the complicating signals. The practitioner actively selects rather than confirms.
 
**Not confident (<50%):** Withhold any specific drug suggestion. State what is missing (e.g. no recorded weight, unclear indication, conflicting active meds) and route to manual prescribing. Never block the practitioner from prescribing manually — withhold the AI, do not obstruct care.
 
**User control surface:**
 
- Practitioner sees the drivers — which patient-file facts and which guideline drove the suggestion
- Practitioner corrects & overrides, with the reason captured
- Corrections feed the dataset/model, gated by clinical review before any training use
- Every suggestion is logged with its confidence score and the confirming practitioner (audit trail)
- Practitioner adjusts the confidence threshold — *not yet*; when added, set at org/admin level, not per-doctor, for safety consistency

## Reliability Contract
Prescription assistance (F2) — proposed defaults. Swap in your numbers, your tools, your on-call.
 
| Metric | Target | Measurement | Alert Threshold |
|---|---|---|---|
| **Accuracy** (suggestion appropriateness) | ≥95% | Weekly · golden set (grows from the 10-row seed) · LLM-as-judge on appropriateness rubric + rule-check on exact drug/dose | <90% → pages on-call clinical product lead |
| **Hallucination rate** (fabricated drug, dose, or guideline citation) | 0 in golden set · <0.5% prod | Weekly run · safety rubric flags fabrications, verified against BCFI/CBIP | >0.5% → pauses AI suggestions, rolls to last good model |
| **Latency p95** (in-consult render) | <1.5 s | Continuous prod monitoring (APM) | >2.5 s for 5 min → pages on-call eng |
| **Drift velocity** (accuracy decay) | <0.3%/wk | 4-week rolling accuracy trend on golden set | >0.5% decay/wk → gold-set audit + retrain review |

## HITL Architecture
<!-- When does a human step in? What's the escalation path? -->

**F1 (Consultation capture):** AI drafts the SOAP note in real time; the GP reviews and confirms before it saves to the patient file. No auto-save without confirmation.

**F2 (Prescription assistance):** Tiered per the Confidence UX above — even the >90% tier requires a one-tap confirm; nothing is ever eHealth-signed without a human action.

**F3 (Patient-file monitoring):** Alerts route to a daily triage queue reviewed by the GP or a delegated practice nurse before any patient contact — never pushed straight to the patient.

**Escalation path:** any suggestion below 50% confidence, any high-risk drug class flag, or any conflicting-allergy signal escalates to mandatory secondary review, logged with reviewer ID and timestamp for the M5 governance audit trail.

## Red-Team Findings
*What failure mode did your partner find that you missed?*

Partner tested a pediatric dosing case using a Belgian brand name that carries different concentration defaults across its FR-market and NL-market packaging (mg/mL suspension vs. mg tablet). The model surfaced the tablet-default dose for a suspension case — a real unit-mismatch risk that row 7 (pediatric weight-based dosing) didn't cover.

**Root cause:** the golden dataset tested the dose *calculation* but not brand-name/formulation ambiguity across Belgium's dual-market packaging.

**Fix:** add two new F2 rows covering formulation ambiguity (suspension vs. tablet, FR- vs. NL-packaged brand variants), and require the UI to always display formulation and concentration alongside any surfaced dose — never the number alone.
