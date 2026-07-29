# Early Stop Archive

This append-only file preserves coherent candidates stopped before formal idea creation. An early
stop is not a `busted` verdict, accepted review, idea status, or evidence-state source.

CREATE operations must draft before consulting this archive. Use targeted lookup of titles,
collision signatures, and reopen conditions. Read a full entry only when the user names its
`ES-*` ID, a post-draft match needs adjudication, or an audit is explicitly requested.

Only `source-checked` entries may produce a later collision warning, and a warning never
automatically busts a candidate. `unverified` entries are archival only.

When concurrent workers are used, workers return structured findings and the coordinator assigns
IDs and appends records serially. Do not archive fabricated evidence, pure protocol failures, or
incoherent fragments.

Use the current project date and next unused two-digit sequence for `NN`.

---

## ES-YYYYMMDD-NN

- Title: [Short candidate title.]
- Candidate scope: [One concise proposition, question, or PICOS-like scope.]
- Parent: `null|NNN|NNN-01`
- Stop stage: `pre-create-gate|terminated-worker`
- Stop dimension: `quantity|quality|novelty|feasibility|scope|protocol|other`
- Evidence basis: `source-checked|unverified`
- Reason: [One sentence.]
- Evidence locators:
  - [Stable identifier, registry field, table, page, query plus date, or unresolved.]
- Uncertainty: [What the bounded screen did not establish.]
- Reopen condition: [Observable change that justifies reconsideration.]
- Collision signatures:
  - [Short structural signature.]
- Scope: `global|root|root:NNN|parent:NNN-01`
- Recorded at: YYYY-MM-DD
