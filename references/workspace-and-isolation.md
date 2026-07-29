# Workspace and Isolation Manual

Read this file only when initializing, repairing, or handling a schema mismatch or interrupted
operation in a `brainstorm/` workspace.

Current managed workspace schema: `3`.

## Goal

Create a directory that exposes shared constraints while hiding idea bodies from unrelated
operations.

## Initialization sequence

1. Confirm the target project root.
2. Create `brainstorm/` and its subdirectories.
3. Copy the workspace templates from `templates/brainstorm/`, including `BUSTED.md`,
   `EARLY_STOPS.md`, and `EVIDENCE_GATE.md`.
4. Fill `BRIEF.md` from user-approved facts and constraints only.
5. Leave indexes, `BUSTED.md`, and `EARLY_STOPS.md` empty except for their headers and
   instructions.
6. Do not import old proposals, rankings, preferred solutions, or undocumented failures into the
   brief, busted ledger, or early-stop archive.
7. Complete the requested create or verify operation.

## Governance compatibility preflight

The root skill checks the schema marker without loading this manual. Load this section only when
`brainstorm_schema_version` is missing or is not `3`. Then:

- if `AGENTS.md` is absent, create it from the current template;
- if `AGENTS.md` exists, do not overwrite it or change other workspace files yet; report the
  governance diff and require explicit user confirmation for replacement or a user-directed
  merge;
- after creating or confirming `AGENTS.md`, create a missing `EVIDENCE_GATE.md` from the template;
- create a missing `EARLY_STOPS.md` from the template only after the governance update is
  confirmed; do not infer old early stops from chats, logs, or abandoned drafts;
- treat `origin_early_stop` as optional for schema-2 idea files and do not rewrite existing ideas
  merely to add it;
- do not rewrite `BRIEF.md`, idea or review bodies, indexes, branch briefs, or busted history;
- for `VERIFY` or `CREATE CHILD`, inspect only the target ID's review filenames and front matter;
  a workspace-wide legacy inventory requires an explicit repair or audit request;
- treat reviews without `review_status` as history, never as accepted evidence sources;
- hard-block `CREATE CHILD` for an affected ID until a new validated `VERIFY` establishes an
  accepted source.

This compatibility repair is not a primary brainstorm operation. Continue to the requested
operation only after any required confirmation and when the target state is unambiguous.

## Shared context boundary

`BRIEF.md` may contain:

- the exact question or objective;
- confirmed background facts;
- immutable constraints;
- explicit exclusions;
- success criteria;
- evidence or time boundaries.

It must not contain:

- summaries of existing idea files;
- hints about which direction is preferred;
- reviewer scores;
- conclusions copied from the main project unless they are established facts;
- instructions to converge on an existing proposal.

## Index boundary

Indexes expose only:

- stable identifier;
- display label, including `BUSTED.<id>` when applicable;
- short title;
- idea status;
- expansion status;
- optional expansion axis;
- child count.

Do not include abstracts, mechanisms, predictions, review conclusions, or evidence excerpts.

## Busted ledger boundary

`BUSTED.md` exposes only compact negative memory:

- ID and title;
- failure class;
- one-sentence reason;
- short collision signatures;
- applicable scope.

Detailed failure analysis remains in the selected idea's review file. CREATE operations must not
read the ledger before producing their initial candidate draft.

## Early-stop archive boundary

`EARLY_STOPS.md` stores compact pre-creation records:

- archive ID and candidate title;
- concise candidate and parent scope;
- stop stage and dimension;
- evidence basis and locators;
- one-sentence reason, uncertainty, and reopen condition;
- collision signatures and applicable scope.

It is not an idea index or evidence-state source. CREATE operations must draft before targeted
lookup. A full entry is readable only when the user names its ID, a post-draft match needs
adjudication, or an audit is explicitly requested.

## Project-side quarantine

When adding project-level agent instructions, state that `brainstorm/` is non-authoritative and
must not be recursively read during ordinary project work.

A normal project agent may know that the directory exists. It must not treat its contents as
requirements, facts, or accepted design decisions.

## Repair rules

If files are missing:

- recreate structural files from templates;
- do not rewrite existing idea or review bodies;
- rebuild an index only from front matter, titles, and current accepted same-ID reviews;
- rebuild `BUSTED.md` only from reviews with a busted verdict;
- never reconstruct `EARLY_STOPS.md` from reviews, chat history, worker logs, or memory; after an
  approved schema migration, create the empty template and preserve any existing archive entries;
- rebuild a branch brief only from the current accepted review and preserve its source review and
  evidence revision;
- ignore draft and superseded reviews as evidence-state sources;
- treat legacy reviews without `review_status` as history, not implicitly accepted; establish a
  source through a new validated `VERIFY`;
- preserve identifiers and history;
- report ambiguity instead of guessing status.

## Deterministic partial-commit repair

Use these rules only for the interrupted ID:

- idea exists and its index row is missing: rebuild the row from immutable idea front matter,
  title, and any current accepted same-ID review; use the stable ID for `Display`, or
  `BUSTED.<id>` when the accepted verdict is busted;
- index row exists but idea is missing: hard-block; do not invent an idea or remove the row
  without explicit user approval;
- review is `draft`: leave it as draft; it has no state effect;
- an early-stop record exists without an idea or index row: treat that as a valid completed
  archive action, not a partial create;
- one new accepted review has a valid transition and either no predecessor or a valid predecessor
  link: treat it as authoritative; when a predecessor exists, complete its allowed
  `accepted -> superseded` metadata change, then rebuild the index, any existing or permitted
  branch brief, and any required busted-ledger entry from the new accepted review;
- accepted reviews are unlinked, duplicated, or transition-invalid: hard-block branching and
  report the exact ambiguity;
- never demote an accepted review to draft or edit an accepted review body.

## Interrupted-worker cleanup

When coordinating concurrent workers, terminate a worker only for an observable protocol failure:
wrong operation or ID, forbidden reads, locked-scope violation, immutable-file mutation, duplicate
committed work, fabricated or untraceable evidence, or repeated off-task behavior after one
correction. Do not terminate merely because a hypothesis is unconventional, weak, or likely to
freeze; verification and the evidence gate decide that.

Workers do not append `EARLY_STOPS.md` directly. They may return one structured candidate record
with evidence locators. The coordinator validates it, assigns the `ES-*` ID, and appends
serially. Do not archive fabricated evidence, pure protocol failures, or incoherent fragments as
research findings.

After termination, inspect only that worker's reserved ID and operation paths:

- apply the deterministic partial-commit rules above;
- remove its reservation only after both idea and index are consistent, or after confirming that
  neither exists;
- verify that draft reviews did not publish state and that any accepted review has valid
  lifecycle, index, and brief state;
- record one compact termination event in an existing project worklog when present, including the
  operation, reason, written artifacts, and cleanup result.
