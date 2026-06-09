# Checklist 1 — AI threat-model readiness (Part II)

Run this before any AI or agentic capability is designed in earnest. It mirrors the threat-modelling spine of Part II; work it top to bottom.

- [ ] **AI threat-model template** run against the proposed system using the named frameworks — owner **Chapter 4**. *Done when:* a completed template exists naming each framework applied.
- [ ] System placed on the **autonomy spectrum and agent topology mapped** before threat-modelling — owner **Chapter 2**. *Done when:* an assigned autonomy level and a documented topology diagram exist.
- [ ] Relevant **FS abuse cases** (fraud, market abuse, mis-selling, exfiltration-for-gain) walked — owner **Chapter 4**. *Done when:* each applicable abuse case is recorded in-scope or ruled out with a reason.
- [ ] **Direct and indirect prompt injection** assessed against every untrusted input path incl. retrieved content — owner **Chapter 5**. *Done when:* every untrusted path is listed with a mitigation or accepted-risk note.
- [ ] **Excessive autonomy and tool abuse** assessed per callable tool — owner **Chapter 5**. *Done when:* each tool has an abuse assessment and an authority boundary.
- [ ] **MCP / connector supply-chain threat** assessed for every connector and server — owner **Chapter 6**. *Done when:* each in-scope connector/server has a provenance and trust verdict.
- [ ] **Data-exfiltration paths** enumerated end to end — owner **Chapter 6**. *Done when:* a path inventory exists, each path controlled or accepted.
- [ ] **Model and data poisoning, and provenance** assessed for any fine-tuning, RAG corpus, or third-party model — owner **Chapter 7**. *Done when:* each source/model has a provenance and poisoning-risk verdict.

> *Practitioner aid, not a compliance position. Each item names its **owning section** in the book;
> where a line and its owning chapter diverge, the chapter governs.*
