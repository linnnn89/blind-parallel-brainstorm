# Workspace and Isolation Manual

Read this file only when initializing or repairing a `brainstorm/` workspace.

Current managed workspace schema: `2`.

## Goal

Create a directory that exposes shared constraints while hiding idea bodies from unrelated
operations.

## Initialization sequence

1. Confirm the target project root.
2. Create `brainstorm/` and its subdirectories.
3. Copy the workspace templates from `templates/brainstorm/`, including `BUSTED.md` and
   `EVIDENCE_GATE.md`.
4. Fill `BRIEF.md` from user-approved facts and constraints only.
5. Leave indexes and `BUSTED.md` empty except for their headers and instructions.
6. Do not import old proposals, rankings, preferred solutions, or undocumented failures into the
   brief or busted ledger.
7. Complete the requested create or verify operation.

## Governance compatibility preflight

Before every primary operation, read only the schema marker in `brainstorm/AGENTS.md` and the
names of required structural files. If `brainstorm_schema_version` is missing or is not `2`:

- replace `AGENTS.md` from the current template only when the file is a known managed legacy
  template with no project-local additions; otherwise stop and report the governance diff;
- create a missing `EVIDENCE_GATE.md` from the template;
- do not rewrite `BRIEF.md`, idea or review bodies, indexes, branch briefs, or busted history;
- inspect review filenames and front matter only to identify legacy state;
- treat reviews without `review_status` as history, never as accepted evidence sources;
- hard-block `CREATE CHILD` for an affected ID until a new validated `VERIFY` establishes an
  accepted source.

This compatibility preflight is not a primary brainstorm operation. Continue to the requested
operation only when the target state is unambiguous after repair.

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
- rebuild a branch brief only from the current accepted review and preserve its source review and
  evidence revision;
- ignore draft and superseded reviews as evidence-state sources;
- treat legacy reviews without `review_status` as history, not implicitly accepted; establish a
  source through a new validated `VERIFY`;
- preserve identifiers and history;
- report ambiguity instead of guessing status.

## Interrupted-worker cleanup

When coordinating concurrent workers, terminate a worker only for an observable protocol failure:
wrong operation or ID, forbidden reads, locked-scope violation, immutable-file mutation, duplicate
committed work, fabricated or untraceable evidence, or repeated off-task behavior after one
correction. Do not terminate merely because a hypothesis is unconventional, weak, or likely to
freeze; verification and the evidence gate decide that.

After termination, inspect only that worker's reserved ID and operation paths:

- remove its reservation when no idea/index commit was completed;
- leave an incomplete review as `draft`; it cannot update an index, brief, or evidence state;
- if an idea exists without its index row, or an index row exists without its idea, stop with a
  repair block instead of guessing which artifact is authoritative;
- verify that no accepted review, branch brief, or index state was published from partial work;
- record one compact termination event in an existing project worklog when present, including the
  operation, reason, written artifacts, and cleanup result.
