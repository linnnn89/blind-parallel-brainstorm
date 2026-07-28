# Busted Idea Ledger

This file stores compact negative memory only. Detailed failure analysis remains in the matching
review file. CREATE operations must draft before reading this ledger.

Do not rename or move original idea files. Display busted ideas as `BUSTED.<id>` in indexes while
keeping their stable path `ideas/<id>.md`.

---

## BUSTED.NNN

- Title: [Short title]
- Failure class: `contradicts-facts|duplicate|no-new-information|non-falsifiable|unsupported-causal-leap|scope-violation|implementation-impossible`
- Reason: [One sentence only.]
- Collision signatures:
  - [Short structural signature.]
- Scope: `global|root:NNN|parent:NNN-01`
- Review: `reviews/NNN/review-NNN.md`
