# Evidence register template

**Purpose.** A standing log of evidence items and evidence *gaps* across the AI control
estate: what evidence exists, where it lives, when it was last verified, and which controls
have no evidence, stale evidence, or evidence past its retention window. The register is the
working ledger behind the assurance map (sibling file `assurance-evidence-map.md`): the map
indexes evidence at a point in time; the register tracks each item's lifecycle and turns
every missing or stale item into a logged finding you close *before* an auditor opens it.

**When to use.** Maintain continuously. A gap found here before the external assessor or the
supervisor finds it is the difference between a managed programme and a surprised one. See
**Chapter 17** of the book for the standing-gap-register discipline and the design /
operating / oversight evidence model; see **Chapter 18** for the obligation mapping this
register does not restate.

**How it fits.** Rows here feed the assurance map's "Where it lives" and "Last verified"
columns and the audit-readiness checklist's gap items. Tie evidence depth to the use case's
risk tier (from your inventory and risk-tiering templates) so you are not chasing evidence
for trivial use cases.

---

## How to fill this in

1. **One row per evidence item.** For each control instance in the assurance map, register
   its design, operating, and oversight evidence as separate rows so each has its own owner,
   location, retention window, and verification date.
2. **Classify the type and the source.** Type is design / operating / oversight. Source is
   machine-generated (preferred) or human-authored. Machine-generated evidence is harder to
   fake and cheaper to keep current.
3. **Record status honestly.** Present / Gap / Stale / Past-retention. A missing or expired
   item is a finding, not a footnote: set a remediation owner and target date.
4. **Verify on cadence.** Continuous for machine-generated evidence; periodic (quarterly, or
   on material change) for design and oversight. Update "Last verified" each cycle.

---

## Section A - Register header

| Field | Value |
|---|---|
| Firm / entity | |
| Estate / scope covered | |
| Register owner (named, accountable) | |
| Linked assurance map | `assurance-evidence-map.md` |
| Last review | |

---

## Section B - Evidence items

*The retention windows in the sample rows below (18 months, 6 years) are illustrative placeholders, not recommended defaults. Set each window from your own obligations and retention schedule.*

| # | Use case (tier) | Control (placement) | Evidence type (design / operating / oversight) | Source (machine / human) | Where it lives (system) | Retention window | Status (Present / Gap / Stale / Past-retention) | Last verified | Remediation owner / target date |
|---|---|---|---|---|---|---|---|---|---|
| EX-1 | Customer-facing servicing copilot (Tier 1 / high) | HITL gates on account actions (agent runtime) | Operating | Machine | SIEM `agent-actions` index | 18 months | Present | _yyyy-mm-dd_ | n/a |
| EX-2 | Customer-facing servicing copilot (Tier 1 / high) | HITL gates on account actions (agent runtime) | Oversight | Human | Governance minutes register | 6 years | Stale (last review > 1 quarter) | _yyyy-mm-dd_ | Chair, AI Oversight Cmte / _yyyy-mm-dd_ |
| | | | | | | | | | |
| | | | | | | | | | |

---

## Section C - Open gap summary

A rolled-up view of every row above whose status is not "Present". This is the standing gap
register an internal-audit function works down.

| Gap # | Use case | Missing / stale evidence | Why it matters (testability / traceability) | Owner | Target close date |
|---|---|---|---|---|---|
| G-1 | Customer-facing servicing copilot | Quarterly oversight-review minutes overdue (EX-2 above) | Breaks oversight evidence: cannot show an accountable reviewer governed the control over the period | Chair, AI Oversight Cmte | _yyyy-mm-dd_ |
| | | | | | |

---

> *Template, provided "as is", not legal or compliance advice. Adapt to your environment and
> obligations; the owning chapter in the book governs.*
