# AI incident-response runbook (fillable) (AR-003)

**Purpose.** A fillable runbook for responding to an AI-specific incident (an injected
agent action, a copilot data leak, a rogue agent, a poisoned model or connector) across the
full lifecycle: detect, triage, contain, eradicate, recover, learn. It is a *delta* on the
incident-response (IR) process your firm already runs, adding the AI-specific steps a
conventional runbook omits. It does not replace that process.

**When to use.**
- During a live or suspected AI incident: work top to bottom, filling each table as you go.
- As a tabletop script: run it against a scenario (see Chapter 12) before you need it for real.
- After go-live and after any material change to a model, provider, or autonomy level: confirm
  the runbook still maps to your estate.

This runbook pairs with `kill-switch-decision.md` (the containment decision tree) in this
folder. It is synced to **Chapter 11** (runtime detection and containment controls) and
**Chapter 12** (IR control design, resilience, and the AI tabletop / BC / DR exercise
practice). The **reporting obligations** an incident may trigger (for example DORA's ICT
incident reporting, or the FCA/PRA operational-resilience regime) are owned in Part VI of the
book and are *not* stated here: this runbook only ensures the assessment can be made fast and
on good evidence.

---

## How to fill this in

Open a single incident record. Stamp it with an ID and the times below, then work each phase
table in order. Italic cells are guidance; replace them with your facts. One incident, one
record.

| Field | Value |
|---|---|
| Incident ID | *your tracker reference* |
| First detected (UTC) | *time the signal fired* |
| First effect (UTC, if different) | *time the harmful action or leak began* |
| Declared by / role | *named responder* |
| IR lead | *named* |
| Current phase | *Detect / Triage / Contain / Eradicate / Recover / Learn* |
| Severity | *your scale* |

> **Worked example header (illustrative):** INC-2026-0042 · first detected 2026-06-09 14:12 UTC ·
> first effect 2026-06-09 14:03 UTC · declared by SOC analyst (J. Okoro) · IR lead R. Vasquez ·
> phase Contain · severity High.

---

## Phase 1: detect and classify

Detection signals come from runtime telemetry (Chapter 11). The output of this phase is a
*classified* incident: one of the four AI categories below, plus a first-cut blast radius.

**AI incident taxonomy (classify into exactly one; see Chapter 12).**

| Category | What it is | Defining question |
|---|---|---|
| 1. Injection-driven action | Direct or indirect prompt injection causes a wrong action or wrong emission | *What did the system do as a result, not just what was injected?* |
| 2. Data leak via copilot | A copilot surfaces regulated data (personal data, PAN, MNPI) to a principal not entitled to it | *One response, or systematic over-retrieval across sessions?* |
| 3. Rogue agent action | An agent takes unintended, repeated, or runaway actions (duplicate transactions, a budget-draining loop, scope escalation) | *What is the action and its downstream effect?* |
| 4. Poisoned model or connector | A model, fine-tune, retrieval corpus, or MCP connector is tampered with upstream, so it behaves adversarially by construction | *Which component, and does it affect every session?* |

**Detection and classification record.**

| Field | Entry |
|---|---|
| Triggering signal | *e.g. anomalous tool-call alert, guardrail-bypass alert, over-retrieval spike, denial-of-wallet spend alarm, behavioural-baseline drift / off-task deviation, customer report* |
| Source layer | *gateway / agent-runtime / MCP / endpoint (Chapter 11 placement)* |
| Category (1 to 4) | |
| First-cut blast radius | *one session / one principal / one tenant / one connector / whole service* |
| Affected service(s) | *name the AI-supported business service* |
| Preliminary severity | |

> **Worked example:** Triggering signal = anomalous tool-call alert (a run of three
> outbound-payment calls in one agent session). Source layer = agent-runtime. Category = 3
> (rogue agent action), with a category-1 suspicion (an indirect injection in a retrieved
> invoice PDF may have driven it). First-cut blast radius = one session. Affected service =
> supplier-payment agent. Preliminary severity = High (money movement).

---

## Phase 2: triage checklist

Triage decides scope, ownership, and the regulatory handoff before you contain. Work the
checklist; do not skip the handoff line even if you are unsure it is reportable.

- [ ] Category confirmed (1 to 4) and recorded.
- [ ] Blast radius confirmed by evidence (the interaction trace), not assumed. Scope is one
  session / principal / tenant / connector / service.
- [ ] Affected AI-supported business service(s) named.
- [ ] IR lead and a named accountable senior (the relevant senior manager) assigned.
- [ ] **Regulatory handoff started.** Route the classified incident to the function that owns
  the reporting assessment (Part VI), and hand them the standing fact set below. Do this in
  parallel with containment, not after it.
- [ ] Evidence-preservation switched on (Phase 3 trace and state capture confirmed running).
- [ ] Model owner engaged where the question is "is this a compromise or expected
  non-deterministic variation?" (only they can answer it; see Chapter 12).
- [ ] DPO / privacy engaged if a regulated-data leak (category 2) is in scope.

**Standing fact set for the regulatory handoff (capture once, hand over):**

| Fact | Entry |
|---|---|
| Incident classification (category) | |
| Confirmed blast radius | |
| Time of first detection | |
| Time of first effect (if different) | |
| Categories of data or actions involved | |
| Reference to the preserved trace | |

> **Worked example:** Category 3 with category-1 root-cause suspicion; blast radius confirmed
> one session (the trace shows no other sessions hit the poisoned invoice); first detection
> 14:12 UTC, first effect 14:03 UTC; actions involved = two outbound supplier payments
> (one settled, one held); trace reference = TRACE-INC-0042 in the gateway audit store.

---

## Phase 3: contain

Containment is sized to the *confirmed* blast radius. Over-broad containment (killing the
whole service for a single-session leak) is itself an availability incident. Use the
companion `kill-switch-decision.md` tree to pick the action; the underlying controls
(per-action and aggregate rate/spend limits, circuit breakers, the kill switch and safe-stop,
graceful degradation) are owned in **Chapter 11**.

**Before you contain, confirm evidence capture is live** (a safe-stop should freeze a record
that already exists, not destroy one):

- [ ] Full interaction trace being captured: system prompt and version, user turn, every span
  of retrieved or tool-sourced content with provenance, model ID and parameters, every
  tool/connector call with arguments and results, final output.
- [ ] Model and connector state frozen: pinned model version, system-prompt version, guardrail
  ruleset, retrieval-corpus snapshot, connector manifest.

**Containment action record.**

| Field | Entry |
|---|---|
| Decision-tree outcome | *A1 connector safe-stop / A2 service safe-stop / A3a session circuit-break / A3b widen to confirmed radius / A4 degrade gracefully* |
| Control invoked (Chapter 11) | *kill switch, circuit breaker, rate/spend limit, graceful degradation* |
| Scope of action | *session / principal / tenant / connector / service* |
| Authorised by | *named; kill-switch authority is pre-agreed* |
| Time actioned (UTC) | |
| Containment verified held | *yes/no; confirm in test before relying on it* |

> **Worked example:** Decision-tree outcome = A3a (harm bounded to one session). Control =
> circuit-break + isolate the session at the agent runtime; the held second payment cancelled
> before settlement. Scope = one session. Authorised by IR lead R. Vasquez. Actioned 14:21 UTC.
> Verified held = yes (no further tool calls from the isolated session). Service kept running
> for all other sessions.

---

## Phase 4: eradicate

Remove the cause so the incident cannot immediately recur. The AI-specific work is identifying
*which* artefact carried the abuse, using the frozen state.

| Field | Entry |
|---|---|
| Root cause identified | *e.g. indirect injection in a specific retrieved document; a poisoned fine-tune; a compromised connector* |
| Poisoned/abused artefact | *name and version: model, corpus snapshot, connector manifest, guardrail rule* |
| Removal / replacement action | *purge the document, roll back to a known-good pinned version, rotate the connector credential, tighten the guardrail* |
| Verified clean | *how you confirmed the artefact is gone or replaced* |
| For category 4: stop-on-suspicion honoured | *removal happened on confirmed compromise, at the scope the compromise reached, not after observed harm* |

> **Worked example:** Root cause = an indirect prompt injection embedded in a supplier invoice
> PDF in the retrieval corpus. Artefact = corpus snapshot RAG-2026-06-09a, document
> INV-88231. Action = purged the document, requeued corpus re-index, added an input-sanitisation
> rule for retrieved PDFs. Verified clean = replay of the captured trace no longer produces the
> extra payment call (corroborative only; see Phase 6).

---

## Phase 5: recover

Restore the service within its impact tolerance (a Part VI concept; the *tolerance* itself is
owned in Chapters 20 and 22, not here). For AI, restoring **availability is not the same as
restoring correct behaviour**: re-run the behavioural and guardrail checks before the restored
path carries live traffic (DR-for-AI discipline, Chapter 12).

| Field | Entry |
|---|---|
| Restore action | *un-isolate the session / lift the safe-stop / fail over to a substitute model or provider* |
| Behavioural checks re-run | *the fallback or restored path passes behavioural + guardrail assertions, not just "the service answers"* |
| Within impact tolerance | *yes/no; confirm the service is back inside the business tolerance* |
| Time restored (UTC) | |
| Residual monitoring | *heightened detection on the affected path for an agreed window* |

> **Worked example:** Restore = lifted the session isolation after the corpus was clean and
> the guardrail rule deployed. Behavioural checks = re-ran the supplier-payment behavioural
> suite (counterparty allowlist, per-action value cap), passed. Within tolerance = yes.
> Restored 15:40 UTC. Residual monitoring = 7-day heightened alerting on outbound-payment
> tool calls for that agent.

---

## Phase 6: learn (post-incident review)

The review closes the loop back into the controls. Two AI-specific cautions: replay is
corroborative, not conclusive (non-determinism means failing to reproduce does not mean it did
not happen); and the exercise/review output is evidence the controls operate, feeding the
assurance and evidence map (Chapter 17), not a separate deliverable to invent.

| Field | Entry |
|---|---|
| What happened (timeline) | *detect, triage, contain, eradicate, recover, with times* |
| Why the existing controls did not prevent it | *which guardrail/limit was bypassed or absent* |
| Replay finding | *what re-running the trace showed; note it is corroborative only* |
| Threat-model updates | *new or revised abuse case (feeds the threat-model template)* |
| Control changes | *new per-action cap, tightened guardrail, added severance test, etc.* |
| Tabletop/exercise follow-up | *scenario to add to the next AI tabletop (Chapter 12)* |
| Assurance evidence produced | *what this incident contributes to the evidence map (Chapter 17)* |

> **Worked example:** Lesson = retrieved PDFs were not input-sanitised before reaching the
> agent's context, so an indirect injection drove a tool call. Control changes = mandatory
> sanitisation of retrieved documents; a per-session cap of one outbound payment pending
> review; a new tabletop scenario "indirect injection via supplier document drives a rogue
> payment." Replay finding: the original prompt reproduced the behaviour 3 times in 5 runs,
> non-deterministic, consistent with the trace.

---

## Roles and contacts

| Role | Named owner | Contact | Notes |
|---|---|---|---|
| IR lead | | | runs the runbook |
| Accountable senior (senior manager) | | | named, per your governance |
| Model owner(s) | | | compromise vs. expected variation call (Chapter 12) |
| SOC / detection | | | owns Phase 1 signals (Chapter 11) |
| DPO / privacy | | | engage on any regulated-data leak |
| Legal / compliance | | | owns the Part VI reporting assessment |
| Comms | | | an AI incident is a reputational event |
| Provider / vendor contacts | | | model and connector escalation paths |
| Kill-switch authoriser | | | pre-agreed; see Chapter 12 |

---

> *This artifact is provided "as is", not legal or compliance advice. Adapt it to your own
> environment and obligations before relying on it. The owning chapters in the book (Chapter 11
> for containment controls; Chapter 12 for IR, resilience, and exercising) govern, and Part VI
> owns every reporting obligation; where this runbook and a chapter ever diverge, the book
> governs.*
