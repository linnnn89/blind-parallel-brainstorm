# Changelog

## Unreleased

### Evidence-state control

- make the current accepted review the only evidence-state source;
- add `draft -> accepted -> superseded` review lifecycle metadata while preserving review history;
- enforce one-step evidence transitions from `speculative` through `protocol_ready`;
- block child creation on stale briefs, source mismatch, invalid transitions, or missing metadata;
- require explicit user confirmation for immature evidence, uncertain novelty, or small pools;
- add a lightweight research evidence gate that freezes rather than deletes weak directions;
- stage single-agent verification as source-first review, prior-review challenge, and adjudication.

### Validation and busted-memory workflow

- recommend verification after 6 unreviewed roots, 3 unreviewed children under one parent, or 8 active unreviewed ideas;
- prefer vertical development of reviewed viable nodes over unlimited root creation;
- replace terminal `rejected` status with `busted`;
- display failed ideas as `BUSTED.<id>` without renaming their stable files;
- add a compact `BUSTED.md` negative-memory ledger;
- generate candidates blind before checking busted collision signatures;
- keep detailed failure reasoning in history-preserving review files.
