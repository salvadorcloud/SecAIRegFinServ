# Checklist 2 — Secure design and agent onboarding (Part III)

Run this as the design-and-build gate before an agent reaches a regulated workload. The control architecture these items reference is owned once, in Chapter 8; do not re-derive it per system.

- [ ] Each agent has a **distinct identity and least-privilege grant** scoped to what it genuinely needs — owner **Chapter 8**.
- [ ] Decisioning-domain actions route through the agreed **human-in-the-loop pattern**, no autonomous path around it — owner **Chapter 8**.
- [ ] The agent sits behind the **AI gateway / control-plane**; no direct, unmediated model or tool access — owner **Chapter 8**.
- [ ] **Control placement** (gateway/agent-runtime/MCP/endpoint) decided deliberately per control — owner **Chapter 8**.
- [ ] The **MCP / model supply chain is hardened** (pinned, attested, provenance-checked connectors and models) — owner **Chapter 8**.
- [ ] **AI data-protection controls** (minimisation, masking, retention at the boundary) applied to inputs and outputs — owner **Chapter 9**.
- [ ] **AI-provider data-handling contracts** (zero-data-retention or equivalent) in place for every external model/connector — owner **Chapter 15**.
- [ ] **Deployment topology and data-residency** chosen against residency and sovereignty requirements — owner **Chapter 2**.
- [ ] Where card data is in scope, the **PCI scope-reduction architecture** keeps AI components out of the CDE by design — owner **Chapter 9**.

> *Practitioner aid, not a compliance position. Each item names its **owning section** in the book;
> where a line and its owning chapter diverge, the chapter governs.*
