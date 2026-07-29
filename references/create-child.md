# CREATE CHILD Manual

Read this file only for `CREATE CHILD <parent-id>`.

## Preconditions

Proceed only when:

- `branch_briefs/<parent-id>.md` exists;
- parent idea status is `survives` or `weakened`;
- expansion status is `open`;
- a current accepted review exists;
- evidence state is `screened` or `verified`;
- child depth and count remain within configured limits;
- the parent has fewer than 3 unreviewed direct children, unless the user explicitly overrides
  the validation advisory.

## State-integrity preflight

Before drafting, read only:

- same-ID review filenames and front matter;
- the current accepted review's compact evidence checkpoint and evidence-gate table;
- `brainstorm/branch_briefs/<parent-id>.md`;
- the owning title-only index row.

Resolve the current accepted review as defined in the lifecycle manual. Compare it with the branch
brief.

Hard blocks stop without writing and cannot be overridden:

| Code | Trigger |
|---|---|
| `STALE_BRANCH_BRIEF` | Revision, time, gate, or checkpoint is stale |
| `SOURCE_REVIEW_MISMATCH` | Brief does not cite the current accepted review |
| `INVALID_STATE_TRANSITION` | Evidence/review lifecycle is invalid or not branchable |
| `MISSING_REQUIRED_METADATA` | Required state, source, confidence, date, gate, blocker, or reopen field is absent |

Soft warnings:

| Code | Trigger |
|---|---|
| `EVIDENCE_IMMATURE` | Evidence state is `screened` |
| `NOVELTY_UNCERTAIN` | Novelty is `concern` or `unknown` |
| `EVIDENCE_POOL_SMALL` | Evidence quantity is `concern` |

Group soft warnings into one `USER_CONFIRMATION_REQUIRED`. Proceed only when the user explicitly
confirms the parent ID and warning codes, including when confirmation is already in the request.

## Allowed reads after preflight

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- `brainstorm/branch_briefs/<parent-id>.md`
- `brainstorm/child_indexes/<parent-id>.md`
- title-only ancestry needed to understand scope
- active reservations under the parent, title only

Do not read the parent's raw idea, sibling bodies, sibling reviews, or unrelated branches.
Do not read `BUSTED.md` or `EARLY_STOPS.md` before producing the initial child draft.

Exception: when the user explicitly asks to reconsider one named `ES-*` record under this parent,
read only that entry after the state-integrity preflight. Its parent and scope must match, and the
child must still preserve the parent's accepted core proposition.

## Procedure

1. Complete the state-integrity preflight and any required soft-warning confirmation.
2. Read the parent's controlled branch brief.
3. Select one unresolved expansion question or allowed axis.
4. Scan direct-child titles to avoid a duplicate proposition.
5. Confirm that the proposed child preserves the parent's core proposition.
6. Draft one candidate child.
7. Read compact `BUSTED.md` entries whose scope is global or applies to this root or parent.
8. Compare the draft against busted propositions, mechanisms, predictions, and failure
   signatures.
9. Target only applicable early-stop titles, signatures, and reopen conditions. Source-checked
   matches warn; confirm the blocker still applies before discarding. Unverified entries never
   filter.
10. Run one bounded post-draft screen only for a hard gate defined by the user or controlled
    brief. Archive a clear, traceable failure as `ES-YYYYMMDD-NN` before discarding; do not
    duplicate a match. Formalize ambiguity for later `VERIFY`.
11. Retry at most twice across all discarded attempts.
12. Reserve the next child ID when concurrency is possible.
13. Write exactly one `ideas/<child-id>.md` with evidence state `speculative` and revision `0`.
    Set `origin_early_stop` only for an explicitly named originating `ES-*` record.
14. Append one title-only row to `child_indexes/<parent-id>.md` with `Display` equal to the stable
    ID, `unreviewed` idea status, and `closed` expansion status.
15. Remove the reservation and stop.

If all three drafts are discarded, write no child and report the busted collisions, existing
early-stop IDs, and new early-stop IDs that caused the stop.

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

Create at most one child and three early-stop records. Early stops get no idea or index row. Do
not verify, compare sibling bodies, synthesize, or promote in the same run.
