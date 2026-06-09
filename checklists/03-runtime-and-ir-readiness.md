# Checklist 3 — Runtime and incident-response readiness (Part IV)

Run this before go-live, and re-run it after any material change to autonomy, tools, or data flows.

- [ ] **AI observability and telemetry** capture prompts, tool calls, decisions, and outputs at the fidelity investigations and assurance need — owner **C11-S2**. *Done when:* a sample investigation can be reconstructed end to end.
- [ ] **Runtime containment** wired and tested: a kill switch / circuit breaker can halt an agent or tool path without a full-system outage — owner **C11-S3**. *Done when:* containment has been exercised in a test.
- [ ] **Resilience and IR control design** covers AI-specific failure and abuse modes, playbooks mapped to incident-reporting obligations — owners **C12-S1, C12-S2**. *Done when:* each mode has a playbook naming its reporting obligation.

> *Practitioner aid, not a compliance position. Each item names its **owning section** in the book;
> where a line and its owning chapter diverge, the chapter governs.*
