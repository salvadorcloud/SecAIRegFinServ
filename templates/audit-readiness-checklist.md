# Audit-readiness checklist template

**Purpose.** Confirm the AI control estate can withstand scrutiny: internal audit (third
line), external assurance (SOC 2 examination, ISO/IEC 42001 certification audit, customer
due diligence), and a supervisor's pointed query. Each item is a yes/no gate backed by the
assurance map and evidence register: if you cannot tick it, you have a finding to log, not a
box to fudge. Assemble every external pack *from* the assurance map, never the reverse.

**When to use.** Run before an internal-audit cycle, a SOC 2 / ISO 42001 readiness
assessment, a major enterprise due-diligence questionnaire, or whenever a supervisory
examination is foreseeable. See **Chapter 17** of the book for internal-audit readiness,
the external-assurance evidence pack, and regulator-query readiness; see **Chapter 18** for
the obligation mapping this checklist points to but does not restate.

**How it fits.** This checklist sits on top of the assurance map
(`assurance-evidence-map.md`) and evidence register (`assurance-evidence-register.md`):
unchecked items become rows in the register's open-gap summary.

---

## Section A - Foundations (the map exists and is current)

| # | Check | Done? | Evidence / location | Notes |
|---|---|---|---|---|
| F-1 | Assurance map seeded from the current use-case inventory; every in-scope use case is a row-set | [ ] | | |
| F-2 | Evidence depth tied to each use case's risk tier (no gold-plating, no under-evidencing of high tiers) | [ ] | | |
| F-3 | Every control carries all three evidence types: design, operating, oversight | [ ] | | |
| F-4 | Each control tagged with enforcement placement (gateway / agent runtime / MCP server/connector / endpoint) | [ ] | | |
| F-5 | Map points at evidence locations; it does not copy evidence in | [ ] | | |
| F-6 | Refresh cadence set and met: continuous (machine) + quarterly/on-change (design + oversight) | [ ] | | |

---

## Section B - Internal-audit readiness

| # | Check | Done? | Evidence / location | Notes |
|---|---|---|---|---|
| IA-1 | **Testability**: an auditor can independently sample each control's evidence (pull the logs / approval records themselves) | [ ] | | |
| IA-2 | **Traceability**: one can walk from a high-risk use case, through its controls and evidence, to the oversight that governs it, and back | [ ] | | |
| IA-3 | **Standing gap register** maintained: controls with no evidence, evidence past retention, use cases that bypassed onboarding | [ ] | | |
| IA-4 | **Non-determinism briefed**: statistical control evidence carries metric, eval methodology, threshold, and residual-risk acceptance beside raw results | [ ] | | |

---

## Section C - External-assurance pack (built from the map)

| # | Check | Done? | Evidence / location | Notes |
|---|---|---|---|---|
| EA-1 | SOC 2: control rows mapped to the Trust Services Criteria in scope; design + operating + oversight evidence locations handed to the assessor | [ ] | | Framework named at Chapter 17 level; criteria not restated here |
| EA-2 | ISO/IEC 42001: governance, inventory, tiering, MRM, and oversight rows assembled as AI-management-system evidence | [ ] | | |
| EA-3 | Enterprise questionnaire answerable by pointing at the same evidence (plus external report once held) | [ ] | | |
| EA-4 | Pack is a curated *view* of the map, scoped to the assessor's framework, not a separate binder | [ ] | | |

---

## Section D - Regulator-query readiness

| # | Check | Done? | Evidence / location | Notes |
|---|---|---|---|---|
| RQ-1 | Every regulatory thread resolves to Part VI: evidence half from the map, obligation half from the Chapter 18 crosswalk; no obligation paraphrased from memory | [ ] | | |
| RQ-2 | Gateway leads, then deeper: gateway evidence answers first-round questions; placement tags lead into agent-runtime / connector / endpoint evidence when the query goes past the chokepoint | [ ] | | Gateway is necessary, not sufficient (Chapter 8) |
| RQ-3 | Board-level residual-risk context ready: quantified loss-exposure ranges referenced, not re-derived (Chapter 16) | [ ] | | |

---

## Worked example (one item, filled in)

| # | Check | Done? | Evidence / location | Notes |
|---|---|---|---|---|
| IA-1 | Testability of HITL gates on the customer-facing servicing copilot (Tier 1) | [x] | Auditor pulls HITL approval/decline records directly from SIEM `agent-actions` index; tool-call authorization logs in same index; mapped in `assurance-evidence-map.md` row EX-1 | Gate-bypass rate confirmed 0% over the period; residual accepted by Head of AI Platform Security |

---

> *Template, provided "as is", not legal or compliance advice. Adapt to your environment and
> obligations; the owning chapter in the book governs.*
