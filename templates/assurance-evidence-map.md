# Assurance / evidence map template

**Purpose.** Tie each control in your AI control estate to the evidence that proves it
actually operates, classified into the three evidence types the book's evidence model uses:
**design** (the control exists and is specified), **operating** (the control ran and had an
effect), and **oversight** (someone accountable reviewed it). The map is an *index* to
where evidence lives, not a copy of it. It is the reader-facing companion to the book's
control-to-regulation crosswalk: this map proves a control *operates*; the crosswalk says
which obligation a control *helps meet*. Keep the wall between them.

**When to use.** Build this once off your AI use-case inventory, then maintain it
continuously. Reach for it when you are standing up internal-audit readiness, assembling a
SOC 2 / ISO 42001 evidence pack, preparing a board assurance summary, or answering a
supervisor's "show me how this AI system is controlled, and prove it." See **Chapter 17**
of the book for the full design/operating/oversight evidence model and how to assemble the
map; see **Chapter 18** for the obligation mapping this template deliberately does not
restate.

**How it fits the other templates.** Seed rows from your use-case inventory and risk
tiering (tier sets how much evidence depth a use case warrants). Record raw findings of
missing or stale evidence in the **evidence register** (sibling file
`assurance-evidence-register.md`), and confirm you are ready for scrutiny with the
**audit-readiness checklist** (sibling file `audit-readiness-checklist.md`).

---

## How to fill this in

1. **Seed from the inventory.** Every AI use case is a row-set; its risk tier sets evidence
   depth (high-tier decisioning copilots earn the fullest trail, a low-tier summariser a
   lighter one). Do not gold-plate evidence for trivial use cases.
2. **Capture all three evidence types per control.** Prefer machine-generated evidence
   (logs, signed config, gate results) over human-authored descriptions: it is harder to
   fake, easier to sample, and cheaper to keep current.
3. **Point, do not copy.** In "Where it lives", name the log store / ticketing system /
   minutes repository / policy register, not the artefact itself. The map is an index.
4. **State the placement** (AI gateway · agent runtime · MCP server/connector · endpoint)
   so the evidence location is unambiguous. The gateway is your most consolidated evidence
   source but is necessary, not sufficient: agent-runtime, connector, and endpoint evidence
   still stand on their own (see Chapter 8).
5. **Set a refresh cadence.** Continuous for machine-generated evidence; periodic
   (quarterly, or on material change) for design and oversight evidence. Stale evidence is a
   finding: log it in the evidence register.
6. **Cross-reference, never restate, obligations.** Link a control to the obligation(s) it
   helps satisfy via the master crosswalk (Chapter 18). Do not paraphrase any obligation,
   clause, threshold, or date into this map.

---

## Section A - Map header

| Field | Value |
|---|---|
| Firm / entity | |
| Estate / scope covered | |
| Map owner (named, accountable) | |
| Period covered | |
| Last full refresh | |
| Linked use-case inventory | |
| Linked crosswalk (obligations) | Chapter 18 master crosswalk |

---

## Section B - Control-to-evidence map

One row per control instance protecting a use case. Tier and placement are tags; the three
evidence columns are the spine.

| # | Use case (tier) | Control (enforcement placement) | Design evidence | Operating evidence | Oversight evidence | Where it lives (index, not copy) | Refresh cadence | Owner | Last verified |
|---|---|---|---|---|---|---|---|---|---|
| EX-1 | Customer-facing servicing copilot (Tier 1 / high) | Least-privilege tool scoping + human-in-the-loop gates on account actions (agent runtime) | Tool-scope catalogue; autonomy placement for each workflow; HITL-gate criteria as code | Tool-call authorization logs; HITL approval/decline records per transaction | Quarterly decisioning-workflow oversight review minutes; named-owner attestation | Scope catalogue in config repo; auth + HITL logs in SIEM (`agent-actions` index); minutes in governance register | Logs continuous; design + oversight quarterly | Head of AI Platform Security | _yyyy-mm-dd_ |
| | | | | | | | | | |
| | | | | | | | | | |
| | | | | | | | | | |

**Placement key.** AI gateway · agent runtime · MCP server/connector · endpoint. Tag each
control with where it is enforced, because that is where its operating evidence is produced.

**Common control families to draw rows from** (build your own from your control inventory;
each names the book chapter to read, not an obligation):

- Scoped agent/workload identity (its evidence, e.g. identity issuance/rotation logs and access-review minutes, differs from tool-scoping evidence) (Chapter 8)
- Least-privilege tool scoping + HITL gates (Chapter 8)
- MCP / model supply-chain hardening; AI gateway controls (Chapter 8)
- Data-protection controls: minimisation, redaction, tenancy isolation (Chapter 9)
- Guardrails + isolation; build-time AI red-teaming + AI-aware SDLC (Chapter 10)
- Runtime observability + detection; runtime containment / kill-switch (Chapter 11)
- AI incident response; AI resilience design + testing (Chapter 12)
- Governance operating model; AI inventory + internal risk-tiering (Chapter 13)
- Model risk management for generative/agentic AI (Chapter 14)
- Risk quantification consumed for board reporting (Chapter 16)

---

## Section C - Non-determinism note (per control, where relevant)

AI control evidence often shows a *distribution* of behaviour, not a binary pass. A
guardrail that blocks 99% of a red-team suite is not "broken" because of the 1%. Where a
control's evidence is statistical, record the interpretive context beside the raw results so
the evidence is auditable, not merely voluminous.

| Control | Metric / threshold | Eval methodology | Residual-risk acceptance (owner / date) |
|---|---|---|---|
| EX-1 (HITL gate coverage) | 100% of in-scope account actions gated; gate-bypass rate 0% | Monthly replay of sampled transactions against gate policy | Residual accepted by Head of AI Platform Security, _yyyy-mm-dd_ |
| | | | |

---

> Build a board / regulator pack by pairing this map with the book's risk-quantification
> output (Chapter 16). Assemble every external pack *from* the map, never the reverse.

> *Template, provided "as is", not legal or compliance advice. Adapt to your environment and
> obligations; the owning chapter in the book governs.*
