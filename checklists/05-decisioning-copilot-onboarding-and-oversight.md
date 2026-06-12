# Checklist 5: Decisioning-copilot onboarding and oversight (Chapter 18)

Run this per copilot, organised by decisioning domain, before a decisioning copilot reaches a regulated workload, and re-run it after any material change to autonomy, tools, or data flows. It is the per-domain onboarding step for the worked playbook owned in **Chapter 18** (`#sec-18-playbook`); none of the controls or obligations it references is re-derived here. Work the domain block that matches the copilot you are standing up; a copilot that spans domains works each relevant block.

**Human-oversight floor (read once, applies to every domain).** Before reading any ceiling off appetite, check it against the regulatory human-oversight floor. The **EU AI Act Article 14** human-oversight obligation is owned in **Chapter 21**, and the **GDPR Article 22** protection against decisions based solely on automated processing is owned in **Chapter 24**. They are referenced here, never restated: if appetite would set a ceiling below the floor, the floor wins, and the floor lives in Part VI. Apply the high-risk test (**Chapter 21**) and the legal-or-similarly-significant-effect test (**Chapter 24**) per domain there, not here.

**The agent-checks-agent caveat (applies to every segregation-of-duties (SoD) split below).** When the checker is itself an LLM agent, a separate identity does not by itself buy an independent failure mode: the same injected or poisoned context that steers the maker can steer the checker; owner **Chapter 8** (mechanism in **Chapter 5**). For high-blast-radius actions, prefer a human checker or a deterministic policy-as-code check over a second LLM judgement on the same context.

## Credit / limit decisions

- [ ] **Autonomy ceiling set against the firm's tiering**, no higher than draft-for-approval (act-with-guardrails only for low-value, fully-reversible limit changes); owner **Chapter 13** (tiering), **Chapter 2** (spectrum). *Done when:* the ceiling is recorded against an assigned tier, read as "no higher than", not a vendor default.
- [ ] **HITL gate placed at the consequential action:** a human decides any adverse or significant credit outcome and any new-money or limit increase above a low threshold; owner **Chapter 8**. *Done when:* a human-decision point sits at the adverse / significant-outcome action with no autonomous path around it.
- [ ] **Agent-checks-agent independence confirmed** for the gate: any non-human checker has independently sourced inputs or is a deterministic policy-as-code check, not a second LLM on shared context; owner **Chapter 8**. *Done when:* the checker on the consequential action is a human or a deterministic check.
- [ ] **Domain failure modes pre-mortemed:** credit / limit manipulation, and discriminatory outcomes (the bias risk owned as a model risk in **Chapter 14**, watched for here at the gate); owner **Chapter 4** (abuse cases). *Done when:* each named failure mode has a confirmed containing control.
- [ ] **Containing controls confirmed:** HITL gate at the adverse-decision point and SoD on proposal-versus-authorisation (**Chapter 8**); gateway logging and redaction of regulated data in prompt and grounding context (**Chapter 8**); provider no-training / retention terms (**Chapter 15**); deployment topology chosen against residency (**Chapter 2**). *Done when:* a named control answers each containing line.

## Fraud operations

- [ ] **Autonomy ceiling set per action against the firm's tiering:** act-with-guardrails permitted only for protective, broadly-reversible actions (hold, step-up, soft block); draft-for-approval for anything that denies service or moves funds; owner **Chapter 13** (tiering), **Chapter 2** (spectrum). *Done when:* the ceiling is recorded per action, not per domain, against an assigned tier.
- [ ] **HITL gate placed at the consequential action:** a human decides irreversible or service-denying actions and the release of held funds; owner **Chapter 8**. *Done when:* the gate sits on irreversible and fund-moving actions with no autonomous path around it.
- [ ] **Agent-checks-agent independence confirmed** for the gate; owner **Chapter 8**. *Done when:* the checker on any irreversible or fund-moving action is a human or a deterministic check.
- [ ] **Domain failure modes pre-mortemed:** detection-model evasion and threshold / risk-score manipulation; account takeover and scam / APP-fraud enablement; mule and fraud-ring detection evasion; owner **Chapter 4**. *Done when:* each named failure mode has a confirmed containing control.
- [ ] **Containing controls confirmed:** HITL gate on irreversible actions and fund release (**Chapter 8**); SoD so the detecting agent and the fund-releasing party are distinct (**Chapter 8**); runtime blast-radius limits sized to each action's autonomy (**Chapter 5**); gateway rate and cost limits (**Chapter 8**). *Done when:* a named control answers each containing line.

## AML transaction-monitoring & sanctions alerting

*Named as a decisioning domain for security and autonomy purposes only. No AML/CTF obligation is stated or mapped here; the low ceiling is a security and operating-model choice, not an asserted legal requirement (see the closing adjacency note).*

- [ ] **Autonomy ceiling set against the firm's tiering**, no higher than suggest / triage: the copilot prioritises, enriches, and drafts; it does not close, suppress, or clear alerts autonomously; owner **Chapter 13** (tiering), **Chapter 2** (spectrum). *Done when:* the ceiling is recorded as triage-only against an assigned tier, with disposition kept non-delegated.
- [ ] **HITL gate placed at the consequential action:** a human decides every alert disposition (clear, escalate, file); the copilot never closes an alert alone; owner **Chapter 8**. *Done when:* a hard human-decision gate sits on disposition with no autonomous close path.
- [ ] **Agent-checks-agent independence confirmed** for the disposition gate; owner **Chapter 8**. *Done when:* the disposition checker is a human or a deterministic check, not a second LLM on shared context.
- [ ] **Domain failure modes pre-mortemed:** alert suppression (alerts silently closed or down-ranked) and alert flooding (true positives drowned); detection-model poisoning (mechanism in **Chapter 7**), durable until retrained; sanctions / PEP / adverse-media screening false-negatives; tipping-off via context or logging leakage; owner **Chapter 4**. *Done when:* each named failure mode has a confirmed containing control.
- [ ] **Containing controls confirmed:** hard HITL gate on disposition (**Chapter 8**); SoD so no single identity can both raise and close an alert (**Chapter 8**); gateway logging of disposition decisions with redaction to contain the tipping-off path (**Chapter 8**); blast-radius caution on any suppression-capable autonomy (**Chapter 5**). *Done when:* a named control answers each containing line.

## SAR/STR reporting

*Named as a decisioning domain only. The SAR/STR sign-off is an AML/CTF human-decision expectation treated as adjacent and not stated as an obligation here (see the closing adjacency note).*

- [ ] **Autonomy ceiling set against the firm's tiering**, no higher than draft-for-approval: the copilot assembles and drafts; it never submits; owner **Chapter 13** (tiering), **Chapter 2** (spectrum). *Done when:* the ceiling is recorded as draft-only against an assigned tier, with submission non-delegated.
- [ ] **HITL gate placed at the consequential action:** the nominated officer / MLRO decides whether to file; no autonomous submission, ever; owner **Chapter 8**. *Done when:* a hard no-autonomous-submission gate sits at the file decision.
- [ ] **Agent-checks-agent independence confirmed** for the file gate: a human submitting authority (the nominated officer / MLRO) or a deterministic submission check closes the draft-to-file span, because an LLM checker on shared context is not an independent failure mode; owner **Chapter 8**. *Done when:* the draft-to-file span is closed by a human authority or a deterministic check.
- [ ] **Domain failure modes pre-mortemed:** sign-off bypass (a report submitted without the human determination); model-driven under-reporting (systematic "no action" drafting); tipping-off via context or logging leakage; owner **Chapter 4**. *Done when:* each named failure mode has a confirmed containing control.
- [ ] **Containing controls confirmed:** hard no-autonomous-submission HITL gate (**Chapter 8**); SoD separating the drafting agent from the submitting authority (**Chapter 8**); gateway logging and redaction to preserve the audit trail and contain tipping-off (**Chapter 8**). *Done when:* a named control answers each containing line.

## Disputes / chargebacks

- [ ] **Autonomy ceiling set against the firm's tiering:** act-with-guardrails only for clear, low-value, well-evidenced auto-decisions; draft-for-approval as value, ambiguity, or fraud signal rises; owner **Chapter 13** (tiering), **Chapter 2** (spectrum). *Done when:* the ceiling is recorded against an assigned tier and rises in caution with value, ambiguity, and fraud signal.
- [ ] **HITL gate placed at the consequential action:** a human decides contested, high-value, or fraud-flagged disputes and any decision against the customer above a threshold; owner **Chapter 8**. *Done when:* the gate sits on contested / high-value / fraud-flagged and against-customer decisions with no autonomous path around it.
- [ ] **Agent-checks-agent independence confirmed** for the gate; owner **Chapter 8**. *Done when:* the checker on contested or high-value decisions is a human or a deterministic check.
- [ ] **Domain failure modes pre-mortemed:** dispute / chargeback manipulation, including fabricated or AI-generated evidence (deepfaked receipts and proofs) and first-party / collusive dispute fraud industrialised against an autonomous decisioner; owner **Chapter 4**. *Done when:* each named failure mode has a confirmed containing control.
- [ ] **Containing controls confirmed:** HITL gate that rises with value, ambiguity, and fraud signal (**Chapter 8**); SoD so the party that proposes a refund does not also authorise it (**Chapter 8**); blast-radius caution on a directly-monetisable autonomous decisioner (**Chapter 5**); provider data-handling terms over dispute evidence and retrieved customer data (**Chapter 15**). *Done when:* a named control answers each containing line.

## KYC / onboarding

- [ ] **Autonomy ceiling set against the firm's tiering:** draft-for-approval for standard cases; suggest-only for elevated-risk, PEP, or adverse-media cases; owner **Chapter 13** (tiering), **Chapter 2** (spectrum). *Done when:* the ceiling is recorded against an assigned tier and drops for elevated-risk, PEP, and adverse-media cases.
- [ ] **HITL gate placed at the consequential action:** a human decides onboarding approval for elevated-risk cases and any case the copilot flags as anomalous; owner **Chapter 8**. *Done when:* the gate sits on elevated-risk and anomalous-case onboarding with no autonomous path around it.
- [ ] **Agent-checks-agent independence confirmed** for the gate; owner **Chapter 8**. *Done when:* the checker on elevated-risk and anomalous cases is a human or a deterministic check.
- [ ] **Domain failure modes pre-mortemed:** KYC / CDD onboarding bypass and synthetic / first-party identity at onboarding (the single home for synthetic identity in the abuse-case catalogue); allow-list / trusted-entity poisoning; owner **Chapter 4**. *Done when:* each named failure mode has a confirmed containing control.
- [ ] **Containing controls confirmed:** HITL gate on elevated-risk and anomalous cases (**Chapter 8**); SoD so the onboarding decision is separated from the identity the new customer will later transact under (**Chapter 8**); gateway logging and redaction of identity documents in the flow (**Chapter 8**); provider no-training / retention terms over identity data (**Chapter 15**); deployment topology chosen so high-sensitivity identity data is processed where residency and retention can be controlled (**Chapter 2**). *Done when:* a named control answers each containing line.

## Adjacency note

AML transaction-monitoring, sanctions alerting, and SAR/STR appear in this checklist only as *decisioning domains* for security and autonomy purposes. This checklist states no AML/CTF or SAR/STR legal obligation, maps none, and asserts none; those duties are adjacent to and outside the book's mapped regulatory scope (the adjacency boundary is registered in **Chapter 3**). The low autonomy ceilings these domains carry are security and operating-model choices (a non-delegated disposition, a human sign-off the firm does not let an agent span), not legal requirements. Where a firm's AML/CTF or reporting duties bear on these workflows, that is a question for its compliance function and counsel.

*This material is for information only and does not constitute legal advice. Regulation changes; verify the current position and consult qualified counsel for your situation.*

> *Practitioner aid, not a compliance position. Each item names its **owning chapter** in the book;
> where a line and its owning chapter diverge, the chapter governs.*
