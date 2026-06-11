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
control-to-regime crosswalk in **Chapter 18** is the single authoritative mapping; this
catalogue is an index into it. Where a control answers no in-scope obligation this book maps
onto it, the column reads "none mapped", which is information, not an omission. Follow the
pointer into the named chapter to see *how* a control answers a regime.

The regimes covered are DORA (Chapter 19), the EU AI Act (Chapter 20), FCA/PRA rules (Chapter
21), PCI DSS (Chapter 22), UK/EU GDPR (Chapter 23), and NIS2 / UK NIS / the Cyber Resilience
Act (Chapter 24).

## Catalogue

| # | Control | Owning chapter | Regimes it answers (Part VI pointer) |
|---|---------|----------------|--------------------------------------|
| 1 | Autonomy-spectrum classification & agent-topology mapping | Chapter 2 | none mapped (a classification input; obligations attach to the controls it scopes) |
| 2 | Deployment topology & data-residency selection | Chapter 2 | GDPR transfers/residency (Chapter 23) |
| 3 | AI threat-model template & framework application | Chapter 4 | none mapped (method feeding the mapped controls) |
| 4 | FS abuse-case assessment | Chapter 4 | none mapped (method feeding the mapped controls) |
| 5 | Prompt-injection defence (direct & indirect) | Chapter 5 | EU AI Act high-risk robustness/cybersecurity (Chapter 20) |
| 6 | Excessive-autonomy & tool-abuse mitigation | Chapter 5 | EU AI Act high-risk robustness (Chapter 20) |
| 7 | MCP / connector supply-chain threat assessment | Chapter 6 | NIS2/UK NIS/CRA supply-chain duty (Chapter 24) |
| 8 | Data-exfiltration-path control | Chapter 6 | GDPR minimisation (Chapter 23); PCI data protection (Chapter 22) |
| 9 | Model/data-poisoning & provenance control | Chapter 7 | EU AI Act high-risk robustness/cybersecurity (Chapter 20); NIS2/CRA supply chain (Chapter 24) |
| 10 | Agent identity & least-privilege | Chapter 8 | PCI access control/authN (Chapter 22); EU AI Act oversight (Chapter 20) |
| 11 | Decisioning-domain human-in-the-loop pattern | Chapter 8 | EU AI Act Art 14 oversight (Chapter 20); GDPR Art 22 ADM floor (Chapter 23) |
| 12 | MCP / model supply-chain hardening | Chapter 8 | NIS2/UK NIS/CRA supply-chain & CRA SBOM (Chapter 24); EU AI Act cybersecurity (Chapter 20) |
| 13 | AI gateway / control-plane | Chapter 8 | DORA (Chapter 19), EU AI Act (Chapter 20), FCA/PRA (Chapter 21), PCI (Chapter 22), GDPR (Chapter 23), NIS2/UK NIS/CRA (Chapter 24) (see gateway crosswalk, Chapter 18) |
| 14 | Control-placement motif (gateway/runtime/MCP/endpoint) | Chapter 8 | none mapped (an architecture motif; obligations attach to the placed controls) |
| 15 | Gateway-config-to-obligations-evidenced crosswalk | Chapter 18 | all six regimes (Chapters 19 to 24; sparse NIS2/UK NIS/CRA entries; owned in Chapter 18) |
| 16 | AI data-protection control | Chapter 9 | GDPR lawful basis/minimisation (Chapter 23); PCI stored-account-data (Chapter 22) |
| 17 | PCI scope-reduction architecture | Chapter 9 | PCI stored-account-data scope (Chapter 22) |
| 18 | AI-provider data-handling contracts (ZDR etc.) | Chapter 15 | DORA third-party (Chapter 19); FCA/PRA outsourcing (Chapter 21); GDPR transfers (Chapter 23); NIS2 supplier duty (Chapter 24) |
| 19 | AI observability / telemetry | Chapter 11 | PCI logging/monitoring (Chapter 22); EU AI Act logging/transparency (Chapter 20); DORA ICT risk (Chapter 19) |
| 20 | Runtime containment (kill switch / circuit breaker) | Chapter 11 | DORA ICT risk management (Chapter 19) |
| 21 | Resilience & IR control design | Chapter 12 | DORA incident reporting & resilience testing (Chapter 19); FCA/PRA operational resilience (Chapter 21) |
| 22 | AI governance operating model | Chapter 13 | FCA/PRA SM&CR accountability (Chapter 21); EU AI Act risk-tier intake (Chapter 20) |
| 23 | Firm-internal AI risk-tiering | Chapter 13 | EU AI Act risk-tier classification (Chapter 20); GDPR DPIA gating (Chapter 23) |
| 24 | MRM-as-control for genAI | Chapter 14 | EU AI Act Art 9 risk-management system (Chapter 20) |
| 25 | Third-party AI governance | Chapter 15 | DORA third-party / register (Chapter 19); FCA/PRA outsourcing (Chapter 21); NIS2 supplier due diligence (Chapter 24); GDPR transfers (Chapter 23) |
| 26 | FAIR risk quantification | Chapter 16 | none mapped (prioritisation, not a compliance obligation) |
| 27 | Assurance / evidence map | Chapter 17 | none mapped (packages evidence into every regime; points in, not mapped to one) |
| 28 | Master control-to-regime crosswalk | Chapter 18 | all six regimes (Chapters 19 to 24; owned and authoritative in Chapter 18) |

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
| Regimes it answers | PCI access control/authN (Chapter 22); EU AI Act oversight (Chapter 20) |
| Owner (your firm) | Platform security lead, AI assistant squad |
| Status | Implemented |
| Evidence (per Chapter 17 assurance map) | IAM policy export showing the assistant's service identity scoped to read-only balance/transaction APIs and a raise-only (no-action) dispute API; access-review record |
| Notes | Dispute *action* routes to the human-in-the-loop pattern (row 11); no autonomous write path |

The catalogue tells you *where to look* (Chapter 8 for the design, Chapters 22 and 20 for what
it evidences); your register captures *how it stands* in your estate.

---

*Practitioner aid, provided "as is", not legal or compliance advice. The owning chapter in the
book governs: verify each control against it before you rely on this catalogue. © 2026 Salvador
Cloud Ltd, released under the MIT Licence; keep the attribution notice with any copy.*
