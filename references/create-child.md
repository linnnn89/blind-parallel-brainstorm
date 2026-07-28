# CREATE CHILD Manual

Read this file only for `CREATE CHILD <parent-id>`.

## Preconditions

Proceed only when:

- `branch_briefs/<parent-id>.md` exists;
- parent idea status is `survives` or `weakened`;
- expansion status is `open`;
- child depth and count remain within configured limits.

## Allowed reads

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- `brainstorm/branch_briefs/<parent-id>.md`
- `brainstorm/child_indexes/<parent-id>.md`
- title-only ancestry needed to understand scope
- active reservations under the parent, title only

Do not read the parent's raw idea, sibling bodies, sibling reviews, or unrelated branches.

## Procedure

1. Read the parent's controlled branch brief.
2. Select one unresolved expansion question or allowed axis.
3. Scan direct-child titles to avoid a duplicate proposition.
4. Confirm that the proposed child preserves the parent's core proposition.
5. Reserve the next child ID when concurrency is possible.
6. Write exactly one `ideas/<child-id>.md`.
7. Append one title-only row to `child_indexes/<parent-id>.md`.
8. Remove the reservation and stop.

## Valid child relationships

A child may:

- explain a more specific mechanism;
- operationalize or implement the parent;
- define a boundary condition;
- propose a discriminating validation route;
- repair a weakness identified during verification;
- derive an extreme or counterintuitive prediction.

A child must add at least one new mechanism, prediction, test, boundary, implementation, or
repair. More detail alone is not enough.

## New-root rule

If the proposed idea denies the parent's core proposition, changes the primary objective, or
requires abandoning inherited assumptions, do not create it as a child. Route it to `CREATE
ROOT` in a later run.

## Weakened parent rule

Children of a `weakened` parent should normally be repair branches. The child must name the
specific weakness it addresses and explain why the repair could escape the earlier criticism.

## Output limit

Create one child only. Do not verify it, compare sibling bodies, synthesize the branch, or
promote it in the same run.
