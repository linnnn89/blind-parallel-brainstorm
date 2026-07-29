# Early Stop Archive

This append-only file preserves coherent candidates stopped before formal idea creation. An early
stop is not a `busted` verdict, accepted review, idea status, or evidence-state source.

CREATE operations must draft before consulting this archive. Target only headings/IDs, titles,
parent and scope, evidence basis, recorded date, record status, collision signatures, reopen
conditions, and matching resolution events. Read reasons and evidence locators only when the user
names an `ES-*` ID, a post-draft match needs adjudication, or an audit is explicitly requested.

Only a unique `source-checked` entry with every required field and a final
`Record status: complete` may warn. A complete resolution event makes the entry historical-only.
For a source-checked entry, `Evidence locators` must include at least one traceable,
non-`unresolved` locator. A resolution suppresses only the archive-derived warning; the current
gate still applies. Warnings never automatically bust a candidate. Unverified, incomplete,
malformed, duplicate, or resolved entries never filter.

When concurrent workers are used, workers return structured findings and the coordinator assigns
IDs and appends records serially. Do not archive fabricated evidence, pure protocol failures, or
incoherent fragments.

Build each entry in working memory and append it once, with `Record status` as the final line and
commit marker. Every `ES-*` or `ER-*` heading consumes its ID even if the append is incomplete;
within each prefix and project date, use the next unused two-digit sequence for `NN`. Duplicate
IDs or malformed complete records block further archive writes until repaired.

---

## ES-YYYYMMDD-NN

- Title: [Short candidate title.]
- Candidate scope: [One concise proposition, question, or PICOS-like scope.]
- Parent: `null|NNN|NNN-01`
- Stop stage: `pre-create-gate|terminated-worker`
- Stop dimension: `quantity|quality|novelty|feasibility|eligibility|scope|other`
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
- Record status: `complete`

---

## ER-YYYYMMDD-NN

- Early stop: `ES-YYYYMMDD-NN`
- Resolution: `reconsidered_as`
- Idea ID: `NNN|NNN-01`
- Reason: [Why the recorded reopen condition may now be satisfied.]
- Recorded at: YYYY-MM-DD
- Record status: `complete`
