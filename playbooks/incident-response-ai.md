# AI incident-response playbook (skeleton)
*Owner: C12-S1 (IR control design) · C12-S2 (resilience/testing). A delta on your existing IR process, not a replacement.*

## Trigger / taxonomy (AI-specific)
- Prompt-injection / tool-abuse event · agent loop / excessive autonomy · poisoned RAG/model · connector/MCP outage or exfiltration · denial-of-wallet.

## Steps
1. **Detect & classify** — from telemetry (C11-S2); classify impact against your criteria (feeds DORA Art. 18-style classification — obligation owned in C19).
2. **Contain** — invoke runtime containment (C11-S3): kill switch / circuit breaker, scoped to connector or service; poisoned-component branch → service-level safe-stop regardless of observed harm.
3. **Reporting clock** — if a major incident, start the regulatory reporting sequence (deadlines owned in Part VI / C19); record initial / intermediate / final.
4. **Forensics** — replay is corroborative, not conclusive (non-determinism); preserve gateway prompt/response + tamper-evident audit (C08-S4).
5. **Recover & learn** — restore within impact tolerance; post-incident review; update threat model & controls.

## Roles / contacts
- IR lead · named accountable senior (SMF) · DPO · comms · provider contacts.

> *Template, provided "as is", not legal or compliance advice. Adapt to your environment and obligations; the owning chapter in the book governs.*
