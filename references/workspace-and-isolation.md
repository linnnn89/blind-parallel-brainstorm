# Workspace and Isolation Manual

Read this file only when initializing or repairing a `brainstorm/` workspace.

## Goal

Create a directory that exposes shared constraints while hiding idea bodies from unrelated
operations.

## Initialization sequence

1. Confirm the target project root.
2. Create `brainstorm/` and its subdirectories.
3. Copy the workspace templates from `templates/brainstorm/`.
4. Fill `BRIEF.md` from user-approved facts and constraints only.
5. Leave indexes empty except for their headers.
6. Do not import old proposals, rankings, or preferred solutions into the brief.
7. Complete the requested create or verify operation.

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

- identifier;
- short title;
- idea status;
- expansion status;
- optional expansion axis;
- child count.

Do not include abstracts, mechanisms, predictions, review conclusions, or evidence excerpts.

## Project-side quarantine

When adding project-level agent instructions, state that `brainstorm/` is non-authoritative and
must not be recursively read during ordinary project work.

A normal project agent may know that the directory exists. It must not treat its contents as
requirements, facts, or accepted design decisions.

## Repair rules

If files are missing:

- recreate structural files from templates;
- do not rewrite existing idea or review bodies;
- rebuild an index only from front matter and titles, without copying body text;
- preserve identifiers and history;
- report any ambiguity instead of guessing status.
