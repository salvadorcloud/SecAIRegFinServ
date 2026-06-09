# Kill-switch / containment decision aid (skeleton)
*Owner: C11-S3 (containment) · C12-S1 (IR). Decide scope deliberately; over-broad containment is its own availability incident.*

```
Observed or suspected AI incident
        |
        v
Is a model/data component poisoned or compromised?
   yes -> SERVICE-level safe-stop of the affected capability
          regardless of observed harm (do not wait for impact)
   no  -> Is harm bounded to one connector / tool path?
            yes -> CONNECTOR-scoped halt (least-disruptive)
            no  -> escalate scope stepwise to service, then estate,
                   sizing each step to blast radius
        |
        v
Record action + time (feeds the reporting clock, Part VI / C19)
Confirm containment held in test before relying on it
```

> *Template, provided "as is", not legal or compliance advice. Adapt to your environment and obligations; the owning chapter in the book governs.*
