# Changelog

## Unreleased

### Leader-coordinated campaigns and medical research profile

- add a session-scoped leader campaign over the existing four atomic operations;
- keep every worker on one bounded assignment while the main agent owns dispatch, portfolio
  balance, final evaluation, freeze, drain, and reporting;
- refill capacity when any worker completes instead of waiting for synchronized waves;
- require non-overlapping concurrent directions and preserve verification, reviewed depth, and
  uncovered breadth when allocating the active frontier;
- allow concentrated descendants only after a current accepted branchable review and valid open
  branch brief, without abandoning eligible sibling lineages or new roots;
- add stable `SC-*` success criteria with per-idea coverage and leader-level campaign evaluation;
- add a medical and biomedical profile that routes question types and intended claims to
  applicable decision dimensions and evidence standards;
- keep the profile optional and preserve the general workflow for other research and software
  ideation;
- retain schema 3 and keep campaign fairness state session-local;
- streamline the skill entry point around activation, cross-mode invariants, and reference
  routing, with detailed procedures owned by their operation or profile manuals;
- express adaptable research guidance as positive decision criteria while reserving hard
  prohibitions for isolation, state integrity, and authorization boundaries.

### Early-stop archive

- add schema 3 and an append-only `EARLY_STOPS.md` for coherent candidates stopped before formal
  idea creation;
- separate pre-create `early_stop` records from accepted-review `busted` verdicts;
- require evidence locators, uncertainty, and reopen conditions for source-checked early stops;
- keep unverified worker findings archival and outside collision filtering;
- support explicit user-directed reconsideration through idea provenance and append-only
  resolution events without adding a new primary operation;
- make the schema marker the final migration commit and check required-path existence;
- use final-line record commit markers, ignore incomplete records, and hard-block duplicate IDs;
- append resolution events so reconsidered early stops do not remain active warnings;
- separate research eligibility failures from worker protocol failures.

### Real-run guardrails

- check the managed workspace schema without loading the repair manual on a match, and require
  confirmation before replacing an existing legacy `AGENTS.md`;
- require first-review `Review B` to challenge a decision-critical checkpoint claim;
- add source locators for decisive evidence claims;
- keep review, branch-brief, and index display contracts aligned;
- define narrow worker-termination criteria and deterministic recovery for reservations, drafts,
  linked accepted reviews, and partial create commits.

### Evidence-state control

- make the current accepted review the only evidence-state source;
- add `draft -> accepted -> superseded` review lifecycle metadata while preserving review history;
- enforce one-step evidence transitions from `speculative` through `protocol_ready`;
- block child creation on stale briefs, source mismatch, invalid transitions, or missing metadata;
- require explicit user confirmation for immature evidence, uncertain novelty, or small pools;
- add a lightweight research evidence gate that freezes rather than deletes weak directions;
- stage single-agent verification as source-first review, checkpoint challenge with prior-review
  comparison, and adjudication.

### Validation and busted-memory workflow

- recommend verification after 6 unreviewed roots, 3 unreviewed children under one parent, or 8 active unreviewed ideas;
- prefer information-gaining verification or reviewed development over unlimited root creation,
  without suppressing genuinely uncovered roots;
- replace terminal `rejected` status with `busted`;
- display failed ideas as `BUSTED.<id>` without renaming their stable files;
- add a compact `BUSTED.md` negative-memory ledger;
- generate candidates blind before checking busted collision signatures;
- keep detailed failure reasoning in history-preserving review files.
