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

**Scope:** AI features in the SupportCopilot product line, automated reply drafting, routing, and resolution scoring. Excludes: Internal-only analytics dashboards (covered by separate data-team policy).

**Autonomy boundaries:** Drafting automated replies, auto. Sending replies under $0 risk (FAQ, account info), auto. Sending replies with promised remedies (refunds, credits, escalations), even if confidence > 95%, human approval required. Closing tickets without reply, never auto.

**Escalation triggers:** (1) Confidence < 70% on response. (2) Customer message flagged legal, medical, or distressed. (3) Any reply mentioning refund, credit, or policy exception. (4) Customer requests human contact. (5) Three or more turns in a single conversation.

**Audit cadence:** Weekly, Automated eval against golden dataset (PM: Sam). Monthly, Human review of 50 random conversations + all escalation cases (Legal: Priya). Quarterly, Full policy review with security + legal (CTO sign-off).

**Regulatory exposure (EU AI Act / other):** EU AI Act, GDPR, SOC 2. Risk tier: limited. Controls: Data minimization in prompts · No training on customer PII · SOC 2 log retention controls in place · DPIA on file..

## Agent Topology

_Not shipping agents this version._


## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? -->

## Shadow AI Audit

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
| | | H / M / L | keep / govern / kill |
| | | H / M / L | keep / govern / kill |
| | | H / M / L | keep / govern / kill |

**Total tools found:**
**Tools after triage:**
**Estimated hidden spend:**
