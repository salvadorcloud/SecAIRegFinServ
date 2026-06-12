# Consolidated control catalogue (AR-007)

**Purpose.** The book's controls in one place, as importable data. Each row names the
control, the **chapter that owns it** (where the design, caveats, and sources live), and the
**regimes that control helps answer**, expressed as pointers to the Part VI chapter that owns
and states each obligation.

**When to use.** Audit an estate row by row (confirm each control exists, is owned, and is
evidenced); seed your governance, risk, and compliance (GRC) register; or assemble a board or
regulator pack. Pair it with the companion CSV (`control-catalogue.csv`) for a direct import.

**How to read the regime column.** It **restates no obligation**: it tells you *which* Part VI
chapter to open, where the article, clause, threshold, and date live. The master
control-to-regime crosswalk in **Chapter 19** is the single authoritative mapping; this
catalogue is an index into it. Where a control answers no in-scope obligation this book maps
onto it, the column reads "none mapped", which is information, not an omission. Follow the
pointer into the named chapter to see *how* a control answers a regime.

The regimes covered are DORA (Chapter 20), the EU AI Act (Chapter 21), FCA/PRA rules (Chapter
22), PCI DSS (Chapter 23), UK/EU GDPR (Chapter 24), and NIS2 / UK NIS / the Cyber Resilience
Act (Chapter 25).

## Catalogue

| # | Control | Owning chapter | Regimes it answers (Part VI pointer) |
|---|---------|----------------|--------------------------------------|
| 1 | Autonomy-spectrum classification & agent-topology mapping | Chapter 2 | none mapped (a classification input; obligations attach to the controls it scopes) |
| 2 | Deployment topology & data-residency selection | Chapter 2 | GDPR transfers/residency (Chapter 24) |
| 3 | AI threat-model template & framework application | Chapter 4 | none mapped (method feeding the mapped controls) |
| 4 | FS abuse-case assessment | Chapter 4 | none mapped (method feeding the mapped controls) |
| 5 | Prompt-injection defence (direct & indirect) | Chapter 5 | EU AI Act high-risk robustness/cybersecurity (Chapter 21) |
| 6 | Excessive-autonomy & tool-abuse mitigation | Chapter 5 | EU AI Act high-risk robustness (Chapter 21) |
| 7 | MCP / connector supply-chain threat assessment | Chapter 6 | NIS2/UK NIS/CRA supply-chain duty (Chapter 25) |
| 8 | Data-exfiltration-path control | Chapter 6 | GDPR minimisation (Chapter 24); PCI data protection (Chapter 23) |
| 9 | Model/data-poisoning & provenance control | Chapter 7 | EU AI Act high-risk robustness/cybersecurity (Chapter 21); NIS2/CRA supply chain (Chapter 25) |
| 10 | Agent identity & least-privilege | Chapter 8 | PCI access control/authN (Chapter 23); EU AI Act oversight (Chapter 21) |
| 11 | Decisioning-domain human-in-the-loop pattern | Chapter 8 | EU AI Act Art 14 oversight (Chapter 21); GDPR automated-decisioning floor (Art 22 EU / s.4A UK) (Chapter 24) |
| 12 | MCP / model supply-chain hardening | Chapter 8 | NIS2/UK NIS/CRA supply-chain & CRA SBOM (Chapter 25); EU AI Act cybersecurity (Chapter 21) |
| 13 | AI gateway / control-plane | Chapter 8 | DORA (Chapter 20), EU AI Act (Chapter 21), FCA/PRA (Chapter 22), PCI (Chapter 23), GDPR (Chapter 24), NIS2/UK NIS/CRA (Chapter 25) (see gateway crosswalk, Chapter 19) |
| 14 | Control-placement motif (gateway/runtime/MCP/endpoint) | Chapter 8 | none mapped (an architecture motif; obligations attach to the placed controls) |
| 15 | Gateway-config-to-obligations-evidenced crosswalk | Chapter 19 | all six regimes (Chapters 20 to 25; sparse NIS2/UK NIS/CRA entries; owned in Chapter 19) |
| 16 | AI data-protection control | Chapter 9 | GDPR lawful basis/minimisation (Chapter 24); PCI stored-account-data (Chapter 23) |
| 17 | PCI scope-reduction architecture | Chapter 9 | PCI stored-account-data scope (Chapter 23) |
| 18 | AI-provider data-handling contracts (ZDR etc.) | Chapter 15 | DORA third-party (Chapter 20); FCA/PRA outsourcing (Chapter 22); GDPR transfers (Chapter 24); NIS2 supplier duty (Chapter 25) |
| 19 | AI observability / telemetry | Chapter 11 | PCI logging/monitoring (Chapter 23); EU AI Act logging/transparency (Chapter 21); DORA ICT risk (Chapter 20) |
| 20 | Runtime containment (kill switch / circuit breaker) | Chapter 11 | DORA ICT risk management (Chapter 20) |
| 21 | Resilience & IR control design | Chapter 12 | DORA incident reporting & resilience testing (Chapter 20); FCA/PRA operational resilience (Chapter 22) |
| 22 | AI governance operating model | Chapter 13 | FCA/PRA SM&CR accountability (Chapter 22); EU AI Act risk-tier intake (Chapter 21) |
| 23 | Firm-internal AI risk-tiering | Chapter 13 | EU AI Act risk-tier classification (Chapter 21); GDPR DPIA gating (Chapter 24) |
| 24 | MRM-as-control for genAI | Chapter 14 | EU AI Act Art 9 risk-management system (Chapter 21) |
| 25 | Third-party AI governance | Chapter 15 | DORA third-party / register (Chapter 20); FCA/PRA outsourcing (Chapter 22); NIS2 supplier due diligence (Chapter 25); GDPR transfers (Chapter 24) |
| 26 | FAIR risk quantification | Chapter 16 | none mapped (prioritisation, not a compliance obligation) |
| 27 | Assurance / evidence map | Chapter 17 | none mapped (packages evidence into every regime; points in, not mapped to one) |
| 28 | Master control-to-regime crosswalk | Chapter 19 | all six regimes (Chapters 20 to 25; owned and authoritative in Chapter 19) |

## Worked example

How a row fills in when you import it into a register and work it for one FS AI use case.

**Use case:** a customer-facing retail-banking assistant (an LLM agent behind an AI gateway)
that answers balance and transaction queries and can raise, but not action, a dispute.

Taking **row 10, Agent identity & least-privilege (Chapter 8)**, a populated register entry
might read:

| Field | Example value |
|---|---|
| Control # / name | 10, Agent identity & least-privilege |
| Owning chapter (read for design) | Chapter 8 |
| Regimes it answers | PCI access control/authN (Chapter 23); EU AI Act oversight (Chapter 21) |
| Owner (your firm) | Platform security lead, AI assistant squad |
| Status | Implemented |
| Evidence (per Chapter 17 assurance map) | IAM policy export showing the assistant's service identity scoped to read-only balance/transaction APIs and a raise-only (no-action) dispute API; access-review record |
| Notes | Dispute *action* routes to the human-in-the-loop pattern (row 11); no autonomous write path |

The catalogue tells you *where to look* (Chapter 8 for the design, Chapters 23 and 21 for what
it evidences); your register captures *how it stands* in your estate.

---

*Practitioner aid, provided "as is", not legal or compliance advice. The owning chapter in the
book governs: verify each control against it before you rely on this catalogue. © 2026 Salvador
Cloud Ltd, released under the MIT Licence; keep the attribution notice with any copy.*
