# Securing AI in Regulated Financial Services: Companion Pack

Reusable, **additive tooling** for the book *Securing AI in Regulated Financial Services: Defending
LLMs, Agents, MCP, and Copilots in Banks and Fintechs under DORA, the EU AI Act, the FCA, and PCI
DSS* by Giovanni Salvador (Salvador Cloud Ltd).

This pack is a **faithful distillation of the book, and nothing more**. It restates no regulatory
obligation: Part VI of the book (Chapters 19 to 24) owns every obligation, and the master
control-by-regime crosswalk in **Chapter 19** is the single authoritative mapping. Where any
artefact here and its owning chapter ever appear to diverge, **the book governs**.

> These materials are provided **"as is", without warranty of any kind**, and are practitioner aids,
> **not legal or compliance advice**. Review and adapt each to your own environment and obligations
> before you rely on it. For any regulatory question, the owning chapter in the book governs.

## Artifact index

Each artifact carries a stable pack id (AR-NNN) so you can cite it. The "Owning chapter(s)" column
points to where the book governs the topic; read your obligations there, never off this pack.

| Artifact | Pack id | Path | What it is | Owning chapter(s) |
|---|---|---|---|---|
| Threat-model template | AR-001 | `templates/threat-model.md` | A fillable AI threat-model worksheet (system, autonomy, abuse cases, mitigations) | Chapter 4 (method); Chapter 2 (attack surface) |
| AI gateway policy-as-code pack | AR-002 | `gateway/` | Vendor-neutral, illustrative gateway/control-plane policy sketches plus a capability checklist | Chapter 8 |
| AI incident-response playbooks | AR-003 | `playbooks/` | AI incident-response and kill-switch / containment decision skeletons | Chapter 12 (IR); Chapter 11 (runtime) |
| DPIA + risk-tiering templates | AR-004 | `templates/dpia.md`, `templates/risk-tiering.md`, `templates/use-case-inventory.md` | A DPIA / data-protection worksheet and a use-case risk-tiering and inventory set | Chapter 9 (DPIA); Chapter 13 (tiering and inventory) |
| Assurance evidence pack | AR-005 | `templates/assurance-evidence-map.md`, `templates/assurance-evidence-register.md`, `templates/audit-readiness-checklist.md` | The control-to-evidence map, evidence register, and audit-readiness checklist | Chapter 17 |
| Control-to-regulation crosswalk | AR-006 | `crosswalk/` | A crosswalk **template** to populate from the book's Part VI | Chapter 19 |
| AI-security control catalogue | AR-007 | `control-catalogue/` | The consolidated control catalogue (Markdown + CSV) for import into your register | Appendix B (Chapter 29); Chapter 19 |

Two further fillable sets ship alongside the indexed artifacts:

| Set | Path | What it is | Owning chapter(s) |
|---|---|---|---|
| Lifecycle checklists | `checklists/` | The four lifecycle checklists (threat-model, secure design, runtime/IR, governance) | Appendix B (Chapter 29) |
| Provider data-handling checklist | `templates/ai-provider-data-handling-checklist.md` | A contract checklist for every external model or connector provider | Chapter 15 |

## How to use

- **Scope a new system:** run `checklists/01` to `04` in lifecycle order; each unchecked box names the
  chapter to read. Start the design with **AR-001** (threat model) and **AR-004** (DPIA + tiering).
- **Stand up the chokepoint:** adapt **AR-002** (gateway pack) into your own policy tooling, then
  confirm coverage against the capability checklist it ships with.
- **Audit an estate:** work **AR-007** (control catalogue) row by row, confirm each control exists,
  is owned, and is evidenced via **AR-005** (assurance pack), then trace it into **AR-006** (crosswalk).
- **Prepare for an incident:** rehearse **AR-003** (IR + kill-switch playbooks) as a tabletop before
  you need them for real.
- **Build a board or regulator pack:** pair **AR-007** with the FAIR quantification (Chapter 16) and
  the assurance map in **AR-005** (Chapter 17).

## Licence

All companion materials are © 2026 Salvador Cloud Ltd and are released under the **MIT License**
(see `LICENSE`), free to use, copy, modify, and distribute, provided the copyright and licence
notice (attribution to Salvador Cloud Ltd) is kept with any copy or adaptation.

© 2026 Salvador Cloud Ltd.
