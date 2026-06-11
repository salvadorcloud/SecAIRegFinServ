# Control-to-regulation crosswalk (AR-006)

The **authoritative** control-by-regime crosswalk is **Chapter 18 ("The Control-to-Regulation
Mapping")** in the book, with the per-regime detail in Chapters 19 to 24 (DORA, EU AI Act, FCA/PRA,
PCI DSS, UK/EU GDPR, and NIS2/UK NIS/EU CRA). The book deliberately states each regulatory obligation
**once**, in Part VI, and does not reproduce obligation text elsewhere, so this repository does **not**
duplicate the obligation cells.

`control-to-regulation.template.csv` gives you the catalogue's 28 controls as rows and the six regimes
as columns, ready to populate **from the book's Part VI** for your own register. Fill each cell with the
obligation reference the book maps that control to (e.g. for DORA, the pillar/article and the owning
section), keeping the book as the source of truth and your "as of" date alongside. The `owner` and
`status_gap` columns are for your register: who owns the control in your estate, and whether it is in
place, partial, or a gap.

> *Template, provided "as is", not legal or compliance advice. Adapt to your environment and obligations; the owning chapter in the book governs.*
