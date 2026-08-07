# Doc — the AI Oracle module embedded inside current medical software (not a standalone product)

> For Belgian GPs drowning in patient-file review time, Doc surfaces the one insight that matters the moment they open a chart — turning medical software from a records system into a clinical co-pilot, defensible through workflow embedding rather than data lock-in, for now.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [x] | `05-the-guardrails/` |
| **The Pitch** | M6 | [x] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Doc — the AI Oracle module embedded inside medical software (not a standalone product)
- **AI Value Archetype:** Oracle
- **Vulnerability Scores:** _(add: Moat _/5 · Data _/5 · Platform _/5)_
- **Top Risk:** Centralization of health data by federal agencies and EU.
- **Confidence:** M
- **Prototype:** https://quick-clinic-tip.lovable.app
- **Kill Criteria:** Kill if: (1) fewer than 20% of pilot GPs open the tip panel in more than half their consultations after 60 days; (2) hallucination rate on the golden set exceeds 0.5% twice in a row; or (3) a national health-data centralization initiative (INAMI/eHealth) makes an independent pati…

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:**
- **Weakest Loop:** ALL OF THEM
- **Top Encroachment Threat:** iCURE
- **Encroachment Defense:** Correction loop, first. Every prescription override or edited SOAP note already happens in the product today — it just isn't captured.…
- **Vendor Portability:** Partial — abstraction layer exists (API calls only, no routing yet). Target: Ready once dynamic routing ships, per the Routing row's own 1-month commitment above.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** 75%
- **Gross Margin (AI-adjusted):** 60%
- **Pricing Model:** seat-based / usage-based / outcome-based / hybrid
- **Pricing Today → Tomorrow:** **Proposed AI pricing:** → **Model:** seat-based / usage-based / outcome-based / hybrid
- **Total AI COGS / unit:**
- **Cascading Strategy:** ratio ~80% Haiku / 20% Opus by request volume.
- **Net Margin Shift:** a real ~15-point compression, but AI adds $26.45 of absolute profit per GP per month. Watch HITL cost as volume scales — that's what the Correction-loop fix (M2/M5) is designed to bring down over time…
- **Break-even at:**

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:**
- **Golden Dataset:**
- **Confidence UX:** Tiered confidence with a mandatory practitioner gate — the AI *proposes*, never prescribes. The visible treatment of the proposal (pre-fill → suggest → withhold) shifts by confidence, every guideline-backed suggestion ci…
- **HITL Architecture:** **F1 (Consultation capture):** AI drafts the SOAP note in real time; the GP reviews and confirms before it saves to the patient file. No auto-save without confirmation.
- **Failure Mode Coverage:** *What failure mode did your partner find that you missed?*

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales, and what compounds.**

- **Compounding System:** | Loop | Input | Output | Compounds? | Status | |------|-------|--------|-----------|--------| | Recursive Learning | User prescriptions correction | updated data set rows | Y | missing | | Cross-Domain Transfer | sympto…
- **Governance Posture:** Doc v1 (medical software AI module) — clinical note drafting, prescription assistance, and patient-file monitoring. Excludes: eFact / eAttest billing automation (covered by separate billing policy).
- **Autonomy Boundaries:** Drafting notes and surfacing suggestions or flags, auto. Writing anything to the patient record, practitioner confirmation required. Issuing or eHealth-signing a prescription, never auto.
- **Escalation Triggers:** (1) Low model confidence on a suggestion. (2) High-risk drug class or a detected interaction / contraindication. (3) Red-flag or distressed clinical content.…
- **Audit Cadence:** Weekly, automated eval against golden dataset (PM: David). Monthly, clinical + legal review of a random sample + all escalation cases (Clinical + Legal).…
- **Shadow AI Audit (user-side):**
- **Agent Boundaries:** Not shipping autonomous agents this version — Doc is suggest-and-confirm only, no action taken without a human trigger. Revisit if Horizon 2's differential/second-opinion assistant ships (see scope note below); it would stay confirm-gated, …
- **Regulatory Exposure:** EU AI Act (high-risk, clinical decision support), MDR, GDPR Art. 9, Belgian eHealth / MyCareNet. Risk tier: high.…

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):**
- **Horizon 2 (Next):**
- **Horizon 3 (Bet):**
- **Board Narrative:** **The case:**
- **Ask:** ## M1 Baseline vs. Now
- **Key Strategic Change:**

→ Details: [`06-the-pitch/`](06-the-pitch/)

