# AI threat-model template (AR-001)
*Owner: Chapter 4 (method, C04-S1) · Chapter 2 (autonomy/topology) · Chapter 4 (FS abuse cases, C04-S2)*

Run the three-lens, single-pass method from Chapter 4: STRIDE-for-AI to find the boundaries,
OWASP LLM for the weaknesses at each, MITRE ATLAS to trace adversary paths to FS impact. Find
the three trust boundaries once, then map weaknesses and attack paths onto them.

## 1. System
- System / capability:
- Owner & date:
- Autonomy level (per Chapter 2 spectrum):
- Agent topology (annotated dataflow link, context window + each tool/connector marked):
- Deployment topology & data residency (Chapter 2):

## 2. Frameworks applied (record the version you modelled against and the date)
- [ ] OWASP Top 10 for LLM Applications, version ____ , assessed ____
- [ ] MITRE ATLAS, version ____ , assessed ____
- [ ] STRIDE-for-AI (per Chapter 4), assessed ____

## 3. Trust boundaries (the spine: mark TB-1/TB-2/TB-3, then enumerate OWASP weaknesses per boundary)
| Boundary | Where it sits | OWASP weakness categories to check | Present in this system? | Notes |
|---|---|---|---|---|
| **TB-1** input-to-model | context window, where trusted instructions and untrusted data mix | prompt injection (direct/indirect), sensitive-info disclosure | | |
| **TB-2** model-to-action | every tool / function call the model can make | excessive agency, improper output to action, tool abuse | | |
| **TB-3** connector-to-regulated-systems | MCP / connector holding standing credentials and scope | supply-chain weakness, over-scoped connector identity | | |
| Cross-cutting | spans all three | data / model poisoning, logging / exfiltration paths | | |

## 4. Threats → mitigations
| # | Boundary (TB-1/2/3) | Threat (framework) | Affected component | Mitigation / accepted-risk | Owning control |
|---|---|---|---|---|---|

## 5. Adversary paths (Step 3: trace at least one path from untrusted input to regulated-system impact)
| # | Path (recon → initial access → execution → impact) | FS impact reached | Priority (monetisation × autonomy × irreversibility) |
|---|---|---|---|
| | | | |

*Worked example:* untrusted email content (TB-1 indirect injection) → payments-agent tool call
(TB-2 excessive agency) → transfer initiated and cleared (irreversible money movement). Autonomy:
act-with-guardrails. Priority: high (directly monetisable, autonomous, irreversible).

## 6. FS abuse cases (Chapter 4 base catalogue, weighted by monetisation × autonomy × irreversibility)
| Abuse case | Reachable here? | Autonomy at which it becomes acute | Boundary exploited | Control |
|---|---|---|---|---|
| Money movement | | act-with-guardrails → autonomous | TB-2 | |
| Credit / limit manipulation | | draft-for-approval → autonomous | TB-1 → TB-2 | |
| Data exfiltration | | any (rises with retrieval breadth) | TB-1 / TB-2 / TB-3 | |
| Fraud at scale | | act-with-guardrails → autonomous | TB-2 | |
| Market abuse | | suggest → autonomous | TB-1 / TB-2 | |
| Sanctions evasion | | act-with-guardrails → autonomous | TB-1 → TB-2 | |

*Extend with the Chapter 4 cases relevant to this system's capability and data access (add a row each):*
- *Base extensions: compliance-pipeline abuse (alert suppression/flooding); dispute & chargeback manipulation.*
- *Cluster A (customer is the victim): account takeover via the servicing AI; scam / APP-fraud via the external-facing AI (the consumer-outcome obligation is owned in Chapter 21).*
- *Cluster B (detection / onboarding models): KYC / CDD onboarding bypass and synthetic identity; detection-model poisoning (mechanism owned in Chapter 7); threshold / calibration evasion; allow-list / trusted-entity poisoning; fabricated and first-party dispute fraud.*

## 7. Residual risk & sign-off
- Residual risks accepted by (named owner) / date:

> *Template, provided "as is", not legal or compliance advice. Adapt to your environment and obligations; the owning chapter in the book governs.*
