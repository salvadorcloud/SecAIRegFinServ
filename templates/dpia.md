# DPIA / data-protection assessment template (AI) (AR-004)
*Owner: Chapter 9 (AI data protection) · obligations owned in Part VI (Chapter 23, GDPR). Not a substitute for your DPO's process.*

## 0. Is a DPIA required? (screening: confirm with your DPO)
Article 35 (obligation owned in Chapter 23) makes a DPIA mandatory for high-risk processing, not merely advisable. Screen first; if any indicator applies, treat a DPIA as required:
- [ ] New or novel technology likely to result in a high risk to individuals (generative or agentic AI on customer data typically qualifies)
- [ ] Automated decisions with legal or similarly significant effect (route to Chapter 23)
- [ ] Large-scale processing of special-category data
- [ ] Systematic monitoring, or any operation on the ICO's high-risk list (UK reference point; the EDPB criteria inform the EU position)

If none clearly applies, record why and confirm the screen with your DPO. The DPIA is a gated onboarding step in the Chapter 13 lifecycle.

## 1. Processing
- Purpose, necessity & proportionality:
- Personal data categories (incl. special category):
- Data subjects & volume:
- Lawful basis (confirm with DPO; obligation owned in Chapter 23):

## 2. AI-specific factors
- Model(s) / providers & data-handling terms (ZDR? see Chapter 15):
- Inputs/outputs minimisation, masking, retention at boundary (Chapter 9):
- Automated decision-making considerations (route to Chapter 23):

## 3. Risks to individuals & measures
| Risk | Likelihood/Severity | Measure | Owning control |
|---|---|---|---|
| *(example)* Indirect prompt injection makes the assistant disclose another customer's personal data | High / High | Output-side PII redaction and per-user retrieval scoping at the gateway | Data-protection controls (Chapter 9); runtime detection (Chapter 11) |

## 4. Outcome
- Residual risk / consultation needed? / sign-off:

> *Template, provided "as is", not legal or compliance advice. Adapt to your environment and obligations; the owning chapter in the book governs.*
