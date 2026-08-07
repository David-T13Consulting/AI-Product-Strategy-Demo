# Three-Horizon Roadmap & Board Pitch

## Roadmap

### Horizon 1, Ship (0–4 weeks)
 
| Initiative | Strategy Component | Why it ships now | Confidence |
|---|---|---|---|
| Correction Capture Loop | Bet *(I'd say Moat — see disagreements)* | The override / edited-SOAP events already fire in-product today; this is instrumentation on existing surfaces, no new model work. | H |
| In-Consult Interaction & Dosing Lookup | Bet | This *is* the Oracle. The prototype (quick-clinic-tip) exists and your M1 kill criteria already assume it's in pilot. Suggest-and-confirm, practitioner-gated — low autonomy risk. | H |
 
### Horizon 2, Validate (1–3 months)
 
| Initiative | Strategy Component | Hypothesis | Kill Criteria | Confidence |
|---|---|---|---|---|
| Multi-Provider Model Routing | Moat | Dynamic routing on an ~80% Haiku / 20% Opus cascade preserves clinical quality while cutting AI COGS. | If Haiku-routed requests fall more than [X pts] below the Opus golden-set accuracy baseline by week 6, stop the cascade and route high-stakes traffic to the higher tier. | M |
| F2 Formulation-Safety Guardrail | Guardrails | An automated formulation/interaction rail catches dangerous combinations without drowning GPs in false alerts. | If it misses *any* known-dangerous interaction on the clinical golden set, or GP dismissal/override exceeds [X]% (alert fatigue), by week 6, stop and rethink. | M |
 
### Horizon 3, Explore (3–6 months)
 
| Initiative | Strategy Component | What must be true first | Confidence |
|---|---|---|---|
| Metered Pricing Rollout | Margin | M3 has to *choose* a pricing model (currently all four listed, none selected), and usage metering + a willingness-to-pay signal must exist. Pilot, don't "roll out." | L |
| Patient Translation Partnership | Bet *(I'd mark Unmapped — see disagreements)* | It must attach to the GP-facing Oracle thesis or a defined revenue line. Today it's patient-facing, off the "embedded in medical software" bet. | L |

## Board Pitch

**Thesis (1 sentence):**
Doc turns the clinical software our GPs already use every day into a live second opinion on prescribing and documentation — cutting risk and admin time without ever taking the pen out of the doctor's hand.

**The case:**
1. Why now: The strategy doesn't state an explicit market-timing catalyst, so treat this as an inference, not a fact to repeat verbatim: M1 names health-data centralization by INAMI/eHealth or the EU as the top risk to this bet. That's also the closest thing to a clock — the window to build an independent, GP-trusted data asset narrows if a centralized alternative arrives first. We already have a working prototype (quick-clinic-tip) and the in-consult surface is live; the H1 initiatives are instrumentation on top of what already ships, not a rebuild.
2. What's defensible: The named threat is iCURE, and our answer is the correction-capture loop — every prescription override or edited SOAP note becomes training signal, and it's already firing in-product, just not captured yet. Be straight about where this stands today: the Moat's own self-assessment lists every loop as weakest, and the data flywheel score is unscored. The defensibility case is a thesis with a four-week build behind it, not a moat that exists yet. That's exactly why it's the first thing we ship.
3. The economics: AI compresses gross margin from 75% to 60% — a real 15-point hit — but it still adds $26.45 of absolute profit per GP per month, mainly by cutting the human review burden the AI creates for itself. The 80/20 Haiku/Opus routing cascade is how we keep COGS down as volume grows. What we don't have yet: a chosen pricing model (all four are still on the table) or a break-even date. We're asking for money before we've picked how we charge for it — that's a real gap, not a formality.

**The risks:**
1. Trust / failure modes: The system is confirm-gated end to end — Doc drafts the SOAP note, the GP reviews and confirms, nothing writes to the patient file or issues a prescription without a human trigger. The front-page scenario is a missed drug interaction or contraindication that a GP didn't catch because they trusted the draft. The honest answer on how the system catches it: we don't have one yet. Reliability target and golden dataset are both unspecified in the strategy today — that's the single most important thing this funding needs to produce in H1, before we scale exposure.
2. Scale / governance: Governance today covers note drafting, prescription assistance, and monitoring — billing is explicitly out of scope. Escalation triggers exist (low confidence, high-risk drug class, red-flag content) and audit cadence is defined (weekly automated eval, monthly clinical/legal review). Regulatory exposure is real: EU AI Act high-risk tier, MDR, GDPR Art. 9. What breaks at 10x isn't the model, it's the human-in-the-loop review cost — that's the thing the correction loop is supposed to bring down, and until it's built, HITL cost scales linearly with usage.
3. Competitive: Kill criteria are explicit and we should hold to them: sub-20% pilot GP engagement at 60 days, hallucination rate over 0.5% on the golden set twice running, or a national data-centralization initiative that makes an independent patient data asset moot. iCURE is the named competitive threat to watch on the encroachment side.

**The ask:**
$3M, 7 headcount, 5-month horizon. In exchange: a working correction-capture loop (the moat, finally instrumented), a validated routing cascade with a real COGS number, and — critically — a defined reliability target and golden dataset, which don't exist yet. What waits: the Patient Translation Partnership. It's coded as a Bet-strategy item in the roadmap, but it's patient-facing and doesn't clearly attach to the GP-embedded Oracle thesis — it reads as unmapped, and it's the first thing that should come off the table if this is funded.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:**
Our goal is to ship and improve the product faster. Out strategy is to use AI to test, ship and iterate faster. The Product doesn’t need to be labelled as AI, it just needs to work. AI can be a solution, it doesn’t have to be. 

**Now:**
