# Securing AI in Regulated Financial Services — Companion Pack

Reusable, **additive tooling** for the book *Securing AI in Regulated Financial Services: Defending
LLMs, Agents, MCP, and Copilots in Banks and Fintechs under DORA, the EU AI Act, the FCA, and PCI
DSS* by Giovanni Salvador (Salvador Cloud Ltd).

This pack is a **faithful distillation of the book, and nothing more**. It restates no regulatory
obligation: Part VI of the book (Chapters 18–23) owns every obligation, and the master
control-×-regime crosswalk (**CL-044, Chapter 18**) is the single authoritative mapping. Where any
artefact here and its owning chapter ever appear to diverge, **the book governs**.

> These materials are provided **"as is", without warranty of any kind**, and are practitioner aids —
> **not legal or compliance advice**. Review and adapt each to your own environment and obligations
> before you rely on it.

## What's here

| Path | What it is | Owning chapter(s) |
|---|---|---|
| `control-catalogue/` | The 28-row consolidated control catalogue (Markdown + CSV) for import into your register | Appendix B / C18 |
| `crosswalk/` | A control-to-regulation crosswalk **template** to populate from the book's Part VI | C18 (CL-044) |
| `checklists/` | The four lifecycle checklists (threat-model, secure design, runtime/IR, governance) | Appendix B |
| `templates/` | Threat-model, DPIA, risk-tiering, assurance/evidence map, use-case inventory, provider checklist | C04, C09, C13, C17, C15 |
| `playbooks/` | AI incident-response and kill-switch/containment decision skeletons | C12, C11 |

## How to use

- **Scope a new system:** run `checklists/01` → `02` → `03` → `04` in lifecycle order; each unchecked box names the chapter to read.
- **Audit an estate:** work `control-catalogue` row by row — confirm each control exists, is owned, and is evidenced (assurance map), then trace it into the book's crosswalk.
- **Build a board/regulator pack:** pair the catalogue with the FAIR quantification (C16) and the assurance map (C17).

## Licence — ACTION NEEDED (reconcile before launch)

The book's back matter states the companion is dual-licensed: **code, configuration, and data
(catalogue/crosswalk CSVs) under the MIT License**, and **templates, checklists, playbooks, and
documentation under CC BY 4.0**, with attribution to **Salvador Cloud Ltd**. This repository currently
ships an **Apache-2.0 `LICENSE`** instead. **Pick one and make the book and repo agree** before
launch — either replace `LICENSE` with `LICENSE-MIT` + `LICENSE-CC-BY-4.0`, or change the book's
back-matter wording to Apache-2.0.

© 2026 Salvador Cloud Ltd.
