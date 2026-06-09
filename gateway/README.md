# AI gateway policy-as-code pack (AR-002)

**Purpose.** A vendor-neutral, worked **starting point** for the policies you put on the AI
gateway (control plane) that brokers every LLM, agent, MCP, and copilot egress in your estate.
It turns the gateway capabilities described in **Chapter 8** of the book into illustrative
policy-as-code so a team can stand the chokepoint up without re-deriving the policy model from
scratch.

**When to use this.**

- You are designing or reviewing the AI gateway for a bank or fintech and want a concrete
  policy skeleton to adapt, not a blank page.
- You need a checklist of the capabilities the gateway should enforce, each tied back to the
  chapter that owns the design.
- You want the honest map of which OWASP Top 10 for LLM Apps 2025 risks a gateway helps with
  versus which it **cannot resolve alone**, to scope the gateway correctly in an architecture
  review or a board conversation.

**What this is not.**

- It is **not** a product configuration. The examples are written as commented pseudo-policy /
  OPA-style rego-like sketches that are **clearly illustrative**. They will not run as-is on any
  gateway, proxy, policy engine, or SDK. Translate the intent into your own tooling.
- It is **not** the obligation source. The gateway *helps evidence* obligations; it does not
  discharge them. The gateway-configuration-to-obligations crosswalk is owned in **Chapter 18**,
  which references the Part VI obligation claims; read your obligations there, never off this pack.
- It does **not** replace the surrounding controls. See "Necessary, but not sufficient" below.

> Provided **"as is"**, without warranty of any kind. These are practitioner aids, **not legal or
> compliance advice**. The owning chapter in the book governs: where this pack and **Chapter 8**
> (or, for obligations, **Chapter 18** / Part VI) ever appear to diverge, **the book governs**.
> Review and adapt every policy to your own environment and obligations before you rely on it.

## What's in the pack

| File | What it is |
|---|---|
| `README.md` | This guide: purpose, the capability checklist, the OWASP map, and the necessary-but-not-sufficient framing. |
| `gateway-policies.rego.md` | The worked, vendor-neutral policy set: one illustrative policy sketch per gateway capability, each with a worked example for a financial-services AI use case and inline guidance notes. |

## How to use it

1. Read the gateway section of **Chapter 8** first. That section owns the design; this pack only
   restates it as policy skeletons.
2. Walk `gateway-policies.rego.md` capability by capability. For each, confirm: is this
   capability enforced at *your* gateway, is the policy owned by a named team, and is its decision
   logged to the audit trail?
3. Cross off the capabilities the gateway genuinely covers, then use the **OWASP map** below to
   write down, explicitly, the risks the gateway does **not** cover and confirm each is owned by
   its real control (identity and least privilege, supply-chain hardening, guardrail design,
   runtime defence).
4. Use the **Chapter 18** crosswalk to map the gateway's evidence (logging, residency routing,
   redaction, audit) to obligations. Do not read any obligation off this pack.

## The capabilities the gateway centralises (Chapter 8)

Configured once at the chokepoint, each applies uniformly to every application behind it. The
worked policy for each lives in `gateway-policies.rego.md`.

| # | Capability | What the policy does at the boundary | Design owned in |
|---|---|---|---|
| 1 | **Authentication & authorization** | Authenticate every call; coarse-authorize which principal/agent may reach which model and egress target. | Chapter 8 |
| 2 | **Model allow-listing** | Only approved models are reachable; block silent routing to an unvetted model. | Chapter 8 |
| 3 | **Prompt & response logging** | A consistent record of what was sent and returned, feeding detection and auditability. | Chapter 8 (telemetry); detection design Chapter 11 |
| 4 | **PII / CHD redaction** | Detect and redact/tokenise regulated data at the boundary. | Enforcement point for Chapter 9 |
| 5 | **Prompt-injection & output-guardrail enforcement** | Run the guardrail policy at the boundary. The gateway *enforces*; it does not *define* the guardrail. | Enforcement of Chapter 10 design |
| 6 | **Rate & cost limits** | Per-principal and aggregate throttles on calls and spend. | Chapter 8 |
| 7 | **Data-residency routing** | Route inference to the region/provider that satisfies residency. | Chapter 8 (routes to satisfy obligations owned in Part VI) |
| 8 | **Audit trail** | A tamper-evident record of policy decisions and egress. | Chapter 8 (raw material for assurance, Chapter 17) |

## Necessary, but not sufficient (Chapter 8)

State this plainly, because the failure mode is treating the gateway as a perimeter that subsumes
everything else. **The gateway is necessary but not sufficient: it is one enforcement layer among
several, not a perimeter that makes the other controls optional.** By construction it cannot
govern, alone:

- **Agent internal planning, tool execution, and autonomy** (least privilege and HITL placement;
  runtime containment, Chapter 11).
- **MCP server hardening** (the supply-chain hardening in Chapter 8; the gateway can deny MCP
  egress but does not vet the connector itself).
- **The model supply chain** (provenance, SBOM, signing, vetting; Chapter 7 and the supply-chain
  hardening in Chapter 8, before and around the gateway).
- **Build-time SDLC** (evaluation, red-teaming, prompt/version control, release gates; Chapter 10).
- **Workload identity** (scoped, short-lived workload identity established below the gateway; the
  gateway authorizes against identities it does not create).

Present the gateway as exactly this: the consistent enforcement chokepoint that makes estate-wide
policy possible, sitting **on top of, never instead of**, identity, supply-chain hardening,
build-time assurance, and runtime defence.

## OWASP Top 10 for LLM Apps 2025 → gateway-capability map

Which OWASP 2025 categories a gateway capability genuinely **helps with**, and which it **cannot
resolve alone**, with a pointer to the control that actually owns each gap. The "cannot resolve
alone" column is the operational form of the necessary-but-not-sufficient limit: for every gap,
there is a named control elsewhere that does own it. The full OWASP coverage map (each category to
its threat-model home and control home) is owned in **Chapter 4** and tabulated in **Appendix B**;
this is the narrower, gateway-specific cut.

| OWASP 2025 category | Gateway capability that touches it | Verdict |
|---|---|---|
| **LLM01 Prompt injection** | Guardrail enforcement (#5) at the boundary. | **Helps, does not resolve.** Injection is systemic (Chapter 5); guardrail enforcement is one layer, paired with least privilege and runtime defence (Chapter 11). |
| **LLM02 Sensitive information disclosure** | PII/CHD redaction (#4) + egress logging (#3). | **Helps.** Data-protection *design* owned in Chapter 9; the gateway enforces it. |
| **LLM05 Improper output handling** | Output-guardrail enforcement (#5) at egress. | **Helps.** Safe handling in the downstream application is the application's job. |
| **LLM07 System-prompt leakage** | Response logging (#3) + redaction (#4) can catch some leakage. | **Helps, partially.** The fix is not putting secrets in the system prompt, which the gateway cannot enforce upstream. |
| **LLM10 Unbounded consumption** | Rate & cost limits (#6). | **Helps, strongest fit.** The category the chokepoint addresses most directly. |
| **LLM03 Supply chain** | Model allow-listing (#2) can deny a non-approved connector/model, nothing more. | **Cannot resolve alone: supply-chain hardening (Chapter 8).** Provenance, pinning, SBOM, signing, vetting happen before and around the gateway. |
| **LLM04 Data and model poisoning** | Not in the gateway's reach. | **Cannot resolve alone: Chapter 7.** A provenance and lifecycle problem (model supply chain). |
| **LLM06 Excessive agency** | The gateway sees egress, not the planner's reasoning or tool-call chaining. | **Cannot resolve alone: Chapter 5 / least privilege.** Bounded by least privilege, per-action mediation, HITL, SoD (Chapter 8), and runtime containment (Chapter 11). |
| **LLM08 Vector and embedding weaknesses** | The retrieval layer and embedding store sit below the gateway. | **Cannot resolve alone: Chapter 9.** Retrieval authorization and data-protection design own this. |

> **LLM09 Misinformation** sits outside the gateway's enforcement reach and is governed by output
> handling and model-risk controls; it is mapped in the **Chapter 4** coverage map, not here.

A gateway that claimed any of the four "cannot resolve alone" rows would be over-claiming, which is
exactly the failure mode the necessary-but-not-sufficient framing warns against.

## Licence

© 2026 Salvador Cloud Ltd. Released under the **MIT License** (see `../LICENSE`).
