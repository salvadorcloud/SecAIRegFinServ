# Kill-switch / containment decision aid (fillable) (AR-003)

**Purpose.** A decision tree for choosing *which* containment control to invoke and at *what
scope* during an AI incident, so the responder follows a pre-agreed path rather than a
judgement call made under pressure. It maps a classified incident and its confirmed blast
radius onto the right runtime control. The core rule throughout: **contain at the confirmed
blast radius, no wider**, because over-broad containment (killing the whole service for a
single-session leak) is its own availability incident.

**When to use.**
- During an AI incident, immediately after Phase 1 to 2 triage in `incident-response-ai.md`
  (this folder) has classified the incident and confirmed the blast radius.
- As a tabletop artefact: walk the tree against a scenario, and fill the "pre-agreed criteria"
  table *before* an incident so the decisions are rehearsed, not improvised (Chapter 12).

The containment controls this tree invokes (per-action and aggregate rate/spend limits,
circuit breakers, the kill switch and safe-stop, graceful degradation) are owned in
**Chapter 11**. The decision logic and the "stop on confirmed compromise, at the scope it
reaches" rule are synced to **Chapter 12** (containment sequencing and the kill-switch
decision tree). A decision tree improvised during an incident is not a control: agree and
rehearse the criteria first.

---

## Pre-agreed criteria (fill in before an incident)

Agree these with the model owners, IR, legal, and the kill-switch authoriser at a tabletop
(Chapter 12). They are the inputs the tree assumes.

| Criterion | Your agreed definition |
|---|---|
| What counts as "actively leaking" regulated data | |
| What blast radius justifies a full service safe-stop | |
| Who is authorised to pull the kill switch (named role) | |
| Whether the runtime supports *dynamic* autonomy reduction, or autonomy is fixed at design time | |
| Where the safe-stop lands the system (the safe state) | |
| How containment is verified to have held | |

> **Worked example:** "Actively leaking" = any response that surfaces a PAN, personal data, or
> MNPI to a principal outside its entitlement, confirmed in the trace. Full service safe-stop =
> blast radius reaches a shared model or core runtime, or more than one tenant. Kill-switch
> authority = IR lead, or duty SRE if the IR lead is unreachable. Autonomy = dynamic for the
> supplier-payment agent (can drop to draft-for-approval at runtime). Safe state = no in-flight
> money movement; the agent halts between tool calls, not mid-transaction.

---

## Decision tree

Read top to bottom. Each numbered node asks one question; follow the YES or NO arm to the next
node or to a terminal action. Every action node names a Chapter 11 control. Every arm ends at
exactly one action, and every action flows to A-END.

```
Observed or suspected AI incident (classified and blast-radius-confirmed in triage)
        |
        v
Q1: Poisoned or compromised model or connector confirmed? (category 4)
   |
   |-- YES --> Q1a: Is the poisoned component a single connector,
   |            not a shared model or core runtime?
   |              |
   |              |-- YES --> A1: SAFE-STOP the poisoned CONNECTOR on confirmed
   |              |            compromise, even before harm. Rest of service may
   |              |            keep running. (Chapter 11: kill switch / safe-stop,
   |              |            connector-scoped)
   |              |
   |              |-- NO  --> A2: SAFE-STOP the SERVICE; invoke the kill switch.
   |                           A poisoned shared model or core runtime is
   |                           whole-service by construction. (Chapter 11: kill
   |                           switch / safe-stop, service-scoped)
   |
   |-- NO  --> Q2: Regulated data actively leaking, OR agent actively
                taking harmful action?
                  |
                  |-- NO  --> A4: DEGRADE GRACEFULLY. Tighten guardrails, lower
                  |            autonomy (if dynamic), restrict connectors, raise
                  |            human-in-the-loop. Monitor and investigate.
                  |            (Chapter 11: graceful degradation)
                  |
                  |-- YES --> Q2a: Is the harm bounded to one session or principal?
                                |
                                |-- YES --> A3a: CIRCUIT-BREAK, rate-limit, or
                                |            isolate the session. (Chapter 11:
                                |            circuit breaker / rate limit, session-scoped)
                                |
                                |-- NO  --> A3b: SAFE-STOP the service or invoke
                                             the kill switch. Widen containment to
                                             tenant, connector, or service per the
                                             CONFIRMED blast radius, no wider.
                                             (Chapter 11: kill switch / safe-stop)
        |
        v
A-END: Record the action and time (feeds the reporting clock and the standing fact
       set, Part VI). Confirm the trace and model + connector state are preserved.
       Verify containment held in test before relying on it.
```

**Three design rules (Chapter 12):**
1. The criteria above are agreed and rehearsed *before* an incident; improvised, they are not a
   control.
2. Containing and preserving evidence are not in tension: the trace is captured continuously,
   so a safe-stop freezes a record that already exists.
3. Even the category-4 "stop on suspicion" branch obeys blast-radius scoping. A poisoned
   *connector* is contained connector-scoped (A1); only a poisoned *shared model or core
   runtime* justifies a whole-service safe-stop (A2). "Stop before observed harm" means act on
   confirmed compromise, *at the scope the compromise actually reaches*, not licence to
   over-contain. (Note: A4's "lower autonomy" presupposes a runtime that supports dynamic
   autonomy reduction; where autonomy is fixed at design time, the levers are
   restrict-connectors, human-queue, or safe-stop.)

---

## Decision record (fill in during the incident)

| Field | Entry |
|---|---|
| Incident ID | *match `incident-response-ai.md`* |
| Category (1 to 4) | |
| Confirmed blast radius | *session / principal / tenant / connector / service* |
| Node reached | *Q1 / Q1a / Q2 / Q2a* |
| Action taken | *A1 / A2 / A3a / A3b / A4* |
| Control invoked (Chapter 11) | |
| Authorised by (named) | |
| Time actioned (UTC) | |
| Evidence preserved? | *trace + model/connector state frozen* |
| Containment verified held? | *yes/no, in test* |

> **Worked example:** INC-2026-0042 · category 3 (rogue agent action) · confirmed blast radius
> one session · Q1 = NO, Q2 = YES (agent actively issuing outbound payments), Q2a = YES (bounded
> to one session) · action **A3a** · control = circuit-break + session isolation at the agent
> runtime · authorised by IR lead R. Vasquez · actioned 14:21 UTC · evidence preserved = yes
> (TRACE-INC-0042) · verified held = yes. Service stayed up for every other session.

---

> *This artifact is provided "as is", not legal or compliance advice. Adapt it to your own
> environment and obligations before relying on it. The owning chapters in the book (Chapter 11
> for the containment controls; Chapter 12 for the decision-tree logic) govern, and Part VI owns
> every reporting obligation; where this aid and a chapter ever diverge, the book governs.*
