# Cost Curve & Pricing Strategy

## Packaging Decision
- Leader: consultation recording/transcription, automated notes taking
- Filler: automatic prescription based on consultation recording
- Killer: patient file scanning and monitoring for intelligent alerts, proactive prevention, drugs misuse warnings, etc

## Cost Model

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) |$20  |Claude Opus 5 |
| Inference (cascading/triage) |$8 |Claude Haiku 4.5 |
| Infrastructure |$0.55 |outsourcing |
| Data/storage |$0 |outsourced to infra |
| Human-in-the-loop |$20  | ~7 escalated reviews/GP/month (per M4's <50% and 50-90% confidence tiers) at ~$2.85 loaded clinician-minute cost|
| **Total AI COGS** | $48.55| corrected — $20 + $8 + $0.55 + $20 sums to $48.55, not $50.55|

## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->

**Triage model: Haiku 4.5**
**Frontier model: Opus 5**
**Routing rule:** Haiku-first for F1 transcription and F3 monitoring scans (low/medium complexity); escalate to Opus for F2 prescription reasoning, or whenever Haiku confidence drops below 70%.
**Expected cascade ratio:** ~80% Haiku / 20% Opus by request volume.

**Bridging this to the COGS table above:** assume ~45 AI-assisted actions per GP per month (notes + prescription checks + monitoring alerts combined). At the $0.63 blended cost/request from the feature table below, that's ≈$28 — consistent with the $20 Opus + $8 Haiku line above.

| Feature | Complexity | Model Tier | Cost/Req | Volume % | Weighted |
|--------------|----------|-------|-------|-------|-------|
|Transcription|Low|Mid|$0.50|70%|$0.35|
|Automated prescription|Complex|Frontier|$1.00|20%|$0.20|
|Patient file monitoring|Medium|Mid|$$0.80|10%|$0.08|
|Total||||100%|$0.63|


## Pricing Model

**Current pricing:**
**Proposed AI pricing:**
**Model:** seat-based / usage-based / outcome-based / hybrid

Pricing Strategy Block, Module 3

Pricing Strategy
- Strategy posture: Skim
- Pricing model: Seat / Access
- Unit of work metered: Prescriptions filled (F2), with F1 transcription and F3 monitoring/insight — the actual "Killer" tier — folded into the base/access fee as included platform value
- Base fee ($/month): 45 (raised from 30 — the original base fee didn't charge for the Killer tier at all)
- Price per unit: $0.15
- Estimated units/user/month: 200
- Implied revenue/user/month: $75.00

Decision Note
Why this pricing structure fits the buyer and the value delivered: At $75 revenue against the corrected $48.55 AI COGS, the AI layer carries ≈35% margin on its own — and it's now charging for the tier (patient-file monitoring) that's actually the differentiator, not just the prescription-assist Filler tier.



## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x |horrible |raise price per use|
| Heaviest segment doubles |the ship sinks | add weekly/Monthly limits|
| Model provider raises prices 50% |404 |disable feature |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

| | Revenue | COGS | Profit | Margin |
|---|---|---|---|---|
| Core DMS only | $120 | $30 | $90 | 75% |
| + AI layer | $195 | $78.55 | $116.45 | ~60% |

**Before (traditional SaaS):** reasonable margins at 75%
**After (AI-enabled):** ~60% blended margin (not -180% — that figure had no derivation behind it)
**Net margin shift:** a real ~15-point compression, but AI adds $26.45 of absolute profit per GP per month. Watch HITL cost as volume scales — that's what the Correction-loop fix (M2/M5) is designed to bring down over time.
