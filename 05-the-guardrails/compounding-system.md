# Compounding System Design

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Recursive Learning | User prescriptions correction | updated data set rows | Y | missing |
| Cross-Domain Transfer | symptoms and diagnostics | retrained model from GPs to PTs | Y | missing |
| Network Intelligence | customer support | updated golden data set | N | missing |

**Broken loop identified by partner:** ·
**Fix plan:** ·

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? -->

**How knowledge flows:** right now, very little. Level 2 or 3 support tickets inform dev teams

**Where it silos:** in every departments. period.


## Governance Policy
<!-- Governance Policy, SupportCopilot v1.2 -->

## Governance Policy

**Scope:** AI features across the  platform, clinical note drafting, prescription assistance, and patient file monitoring. Excludes: eFact / eAttest billing automation (covered by separate billing policy).
**Autonomy boundaries:** Drafting notes and surfacing suggestions or flags, auto. Writing anything to the patient record, practitioner confirmation required. Issuing or eHealth-signing a prescription, never auto.
**Escalation triggers:** (1) Low model confidence on a suggestion. (2) High-risk drug class or a detected interaction / contraindication. (3) Red-flag or distressed clinical content. (4) Out-of-scope request, or reference to a patient outside the active context.
**Audit cadence:** Weekly, automated eval against golden dataset (PM: David). Monthly, clinical + legal review of a random sample + all escalation cases (Clinical + Legal). Quarterly, full policy review with security + legal (CTO / DPO sign-off).
**Regulatory exposure (EU AI Act / other):** EU AI Act (high-risk, clinical decision support), MDR, GDPR Art. 9, Belgian eHealth / MyCareNet. Risk tier: high. Controls: Human-in-the-loop on every record write · Data minimisation in prompts · No training on patient PII · Prescription logic grounded on BCFI / CBIP · DPIA on file.

## Agent Topology

_Not shipping agents this version._


## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? -->

## Shadow AI Audit

## Discover, User-Side Workarounds
- Paste consultation notes into ChatGPT for a differential / second opinion | source: User interview | signal: Capability gap | freq: H | spend: €23/mo | decision: Build
- Ask ChatGPT for a drug interaction or dosing check because the in-app BCFI lookup is slower | source: User interview | signal: Workflow gap | freq: H | spend: €0/mo | decision: Build
- Consumer transcription app (Whisper/Otter) to dictate the consult, then paste into the record | source: Forum/Reddit | signal: Workflow gap | freq: M | spend: €0/mo | decision: Build
- Paste lab-result PDFs into ChatGPT to interpret values before the consult | source: Sales call | signal: Capability gap | freq: M | spend: €23/mo | decision: Build
- ChatGPT / DeepL to translate patient instructions & sick notes into NL/FR/DE/other | source: Support ticket | signal: Capability gap | freq: H | spend: €8/mo | decision: Partner
- Paste INAMI nomenclature questions into ChatGPT to find the right billing code | source: Support ticket | signal: Trust gap | freq: L | spend: €0/mo | decision: Ignore
## Pattern Assessment
- Workarounds found: 6
- Build candidates: 4
- Partner candidates: 1
- Ignore decisions: 1
- Adjacent spend: €54/mo
- Dominant signal: Capability gap
## Action Plan
### Build
Differential / second-opinion assistant (high freq, capability gap, grounded + confirmation-gated, keeps PII in-boundary)
Fast interaction & dosing check (high freq, workflow gap, surface BCFI inline so leaving to ChatGPT is never faster)
Native ambient consultation capture (M freq, workflow gap, removes the consumer-recorder detour)
Lab-result interpretation (M freq, capability gap, grounded flags in-context, "informational, not diagnostic")
### Partner
Patient translation workflow → partner with one GDPR-compliant localization-AI provider, deep link from the instruction / sick-note screen
### Ignore + Monitor
INAMI billing-code lookups in ChatGPT → out of AI scope (separate billing policy); monitor and improve in-app nomenclature search instead.
## Roadmap Brief
Based on your audit: 6 user-side workarounds discovered.
Decisions: 4 build · 1 partner · 1 ignore · 0 TBD.
Estimated adjacent spend: €54/mo across surveyed users.
Dominant signal: Capability gap.
Recommended next step: Capability gaps dominate, your users are reaching for consumer LLMs to do clinical reasoning the product doesn't yet surface. Strongest near-term move is grounded, confirmation-gated clinical assist (interaction/dosing + differential), since these are high-frequency and leak special-category data.
Sequence the Build column by frequency × clinical risk, not frequency alone. Treat the paste-notes and interaction-check cases as compliance-urgent (GDPR Art. 9 exfiltration to consumer tools), not just roadmap items. Confirm the Partner candidate with the localization provider's team. Re-run this audit each quarter, workarounds shift fast.
