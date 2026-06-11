# Checklist 2: Secure design and agent onboarding (Part III)

Run this as the design-and-build gate before an agent reaches a regulated workload. The control architecture these items reference is owned once, in Chapter 8; do not re-derive it per system.

- [ ] Each agent has a **distinct identity and least-privilege grant** scoped to what it genuinely needs; owner **Chapter 8**. *Done when:* the agent has a unique identity and its grant lists only justified tools and data scopes.
- [ ] Decisioning-domain actions route through the agreed **human-in-the-loop pattern**, no autonomous path around it; owner **Chapter 8**. *Done when:* every decisioning-domain action has a defined human checkpoint and no autonomous path around it.
- [ ] The agent sits behind the **AI gateway / control-plane**; no direct, unmediated model or tool access; owner **Chapter 8**. *Done when:* all model and tool traffic is shown to traverse the gateway, with no bypass route open.
- [ ] **Control placement** (gateway/agent-runtime/MCP/endpoint) decided deliberately per control; owner **Chapter 8**. *Done when:* each control has a recorded placement decision rather than a default.
- [ ] The **MCP / model supply chain is hardened** (pinned, attested, provenance-checked connectors and models); owner **Chapter 8**. *Done when:* every connector and model is pinned to a version with attestation and a provenance record.
- [ ] **AI data-protection controls** (minimisation, masking, retention at the boundary) applied to inputs and outputs; owner **Chapter 9**. *Done when:* minimisation, masking, and retention are each configured and evidenced at the boundary.
- [ ] **AI-provider data-handling contracts** (zero-data-retention or equivalent) in place for every external model/connector; owner **Chapter 15**. *Done when:* a signed contract with the relevant terms exists for each external provider.
- [ ] **Deployment topology and data-residency** chosen against residency and sovereignty requirements; owner **Chapter 2**. *Done when:* the topology is documented and reconciled against each applicable residency requirement.
- [ ] Where card data is in scope, the **PCI scope-reduction architecture** keeps AI components out of the cardholder-data environment (CDE) by design; owner **Chapter 9**. *Done when:* a scoping diagram shows no AI component inside the cardholder-data environment.

> *Practitioner aid, not a compliance position. Each item names its **owning chapter** in the book;
> where a line and its owning chapter diverge, the chapter governs.*
