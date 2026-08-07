# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** |Google, only model available per company policy | H  | Raise awareness with leadership within 2 weeks|
| **Abstraction** | API Calls | H  |Study lowering abstraction to multi provider routing within a month |
| **Routing** | None| H | implement dynamic routing and remove hardcoded vendors|
| **Eval** | only functional evals| H | Create harness this quarter|

## Portability Score
<!-- Locked -->
Partial — abstraction layer exists (API calls only, no routing yet). Target: Ready once dynamic routing ships, per the Routing row's own 1-month commitment above.

## If [primary vendor] doubles pricing tomorrow:
<!-- What's your 48-hour response? --> Shift ~80% of triage-tier (Haiku-class) traffic to the standby provider via the abstraction layer within 48 hours — routing is already scoped this quarter. Absorb the frontier-tier (Opus-class) cost short-term, since F2 prescription reasoning can't be re-validated on a different model without re-running the golden dataset. Use the abstraction-layer leverage to renegotiate before the next billing cycle.

## If [primary vendor] ships a competing product:
<!-- What's defensible that they can't replicate? --> Today, the real defense is workflow depth: Doc lives inside the patient-file-open moment in Medispring, not a separate tab a GP has to remember to open. It is not yet a data moat — the Data Flywheel score is 4/20. That gap is exactly what the Correction-loop fix (M2 flywheel, M5 compounding system) is meant to close before a competing product forces the question.
