# Checklist 2 — Secure design and agent onboarding (Part III)

Run this as the design-and-build gate before an agent reaches a regulated workload. The control architecture these items reference is owned once, in C08-S4; do not re-derive it per system.

- [ ] Each agent has a **distinct identity and least-privilege grant** scoped to what it genuinely needs — owner **C08-S2**.
- [ ] Decisioning-domain actions route through the agreed **human-in-the-loop pattern**, no autonomous path around it — owner **C08-S2**.
- [ ] The agent sits behind the **AI gateway / control-plane**; no direct, unmediated model or tool access — owner **C08-S4**.
- [ ] **Control placement** (gateway/agent-runtime/MCP/endpoint) decided deliberately per control — owner **C08-S4**.
- [ ] The **MCP / model supply chain is hardened** (pinned, attested, provenance-checked connectors and models) — owner **C08-S3**.
- [ ] **AI data-protection controls** (minimisation, masking, retention at the boundary) applied to inputs and outputs — owner **C09-S1**.
- [ ] **AI-provider data-handling contracts** (zero-data-retention or equivalent) in place for every external model/connector — owner **C15-S1**.
- [ ] **Deployment topology and data-residency** chosen against residency and sovereignty requirements — owner **C02-S1**.
- [ ] Where card data is in scope, the **PCI scope-reduction architecture** keeps AI components out of the CDE by design — owner **C09-S2**.

> *Practitioner aid, not a compliance position. Each item names its **owning section** in the book;
> where a line and its owning chapter diverge, the chapter governs.*
