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
| Human-in-the-loop |$20  | unknown, estimated worst case|
| **Total AI COGS** | $50.55| |

## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->

**Triage model: Opus**
**Frontier model: Haiku**
**Routing rule:**
**Expected cascade ratio:**

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
- Unit of work metered: Prescriptions filled
- Base fee ($/month): 30
- Price per unit: $0.15
- Estimated units/user/month: 200
- Implied revenue/user/month: $60.00

Decision Note
Why this pricing structure fits the buyer and the value delivered: ·



## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | | |
| Heaviest segment doubles | | |
| Model provider raises prices 50% | | |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):**
**After (AI-enabled):**
**Net margin shift:**
