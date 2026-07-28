# CREATE CHILD Manual

Read this file only for `CREATE CHILD <parent-id>`.

## Preconditions

Proceed only when:

- `branch_briefs/<parent-id>.md` exists;
- parent idea status is `survives` or `weakened`;
- expansion status is `open`;
- child depth and count remain within configured limits;
- the parent has fewer than 3 unreviewed direct children, unless the user explicitly overrides
  the validation advisory.

## Allowed reads before drafting

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- `brainstorm/branch_briefs/<parent-id>.md`
- `brainstorm/child_indexes/<parent-id>.md`
- title-only ancestry needed to understand scope
- active reservations under the parent, title only

Do not read the parent's raw idea, sibling bodies, sibling reviews, or unrelated branches.
Do not read `BUSTED.md` before producing the initial child draft.

## Procedure

1. Read the parent's controlled branch brief.
2. Select one unresolved expansion question or allowed axis.
3. Scan direct-child titles to avoid a duplicate proposition.
4. Confirm that the proposed child preserves the parent's core proposition.
5. Draft one candidate child.
6. Read compact `BUSTED.md` entries whose scope is global or applies to this root or parent.
7. Compare the draft against busted propositions, mechanisms, predictions, and failure
   signatures. Discard and retry at most twice on collision.
8. Reserve the next child ID when concurrency is possible.
9. Write exactly one `ideas/<child-id>.md`.
10. Append one title-only row to `child_indexes/<parent-id>.md` with an empty label,
    `unreviewed` idea status, and `closed` expansion status.
11. Remove the reservation and stop.

If all three drafts collide with busted signatures, write no child and report the collision.

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

## Vertical-development priority

After a useful root pool exists, prefer developing `survives` or qualified `weakened` nodes over
adding more roots. Within one parent, however, recommend verification when 3 direct children are
still unreviewed. Do not let a vertical branch become another pile of untested files.

## New-root rule

If the proposed idea denies the parent's core proposition, changes the primary objective, or
requires abandoning inherited assumptions, do not create it as a child. Route it to `CREATE
ROOT` in a later run.

## Weakened parent rule

Children of a `weakened` parent should normally be repair or scope-narrowing branches. The child
must name the specific weakness it addresses and explain why the repair could escape the earlier
criticism.

## Output limit

Create one child only. Do not verify it, compare sibling bodies, synthesize the branch, or
promote it in the same run.
