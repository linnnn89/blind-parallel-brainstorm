# CREATE ROOT Manual

Read this file only for `CREATE ROOT`.

## Allowed reads before drafting

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- `brainstorm/ROOT_INDEX.md`
- active root reservations, title only

Do not read any file under `ideas/`, `reviews/`, `branch_briefs/`, or `child_indexes/`.
Do not read `BUSTED.md` or `EARLY_STOPS.md` before producing the initial candidate draft.

Exception: when the user explicitly asks to reconsider one named `ES-*` record, read only that
entry before drafting. State which blocker may no longer apply or will be directly retested. Do
not read other early-stop entries.

## Procedure

1. Restate the problem internally from `BRIEF.md` without importing outside proposals.
2. Scan root titles only to avoid direct title conflict.
3. Choose one meaningfully distinct direction.
4. Draft the candidate without reading prior failed-idea records, except for the one explicitly
   named early-stop record in a user-directed reconsideration.
5. Read the compact entries in `BUSTED.md` and compare the draft against their failure
   signatures.
6. Target only early-stop titles, signatures, and reopen conditions. Source-checked matches warn;
   confirm the blocker still applies before discarding. Unverified entries never filter.
7. Run one bounded post-draft screen only for a hard gate defined by the user or `BRIEF.md`.
   Archive a clear, traceable failure as `ES-YYYYMMDD-NN` before discarding; do not duplicate a
   matching record. Formalize ambiguity for later `VERIFY`.
8. Retry at most twice across all discarded attempts.
9. Reserve the next three-digit root ID when concurrency is possible.
10. Write exactly one `ideas/NNN.md` from the idea template. Set `origin_early_stop` only when the
    user explicitly named the originating `ES-*` record.
11. Append one title-only row to `ROOT_INDEX.md` with `Display` equal to the stable ID,
    `unreviewed` idea status, and `closed` expansion status.
12. Remove the reservation and stop.

If all three drafts are discarded, write no idea and report the busted collisions, existing
early-stop IDs, and new early-stop IDs that caused the stop.

## Distinctness rule

A title conflict exists when the new direction has the same core proposition as an indexed root,
even if phrased differently.

A candidate is also a duplicate when its mechanism, differentiating prediction, and practical
validation route are materially the same as an indexed direction.

Title similarity alone does not justify reading an existing idea body. Choose another direction
or report that comparison requires an explicitly authorized synthesis.

## Validation advisory

After creating the root, inspect title-only lifecycle counts. Recommend `VERIFY` when any default
threshold is reached:

- 6 unreviewed roots;
- 8 total active unreviewed ideas;
- at least 3 meaningfully different mechanisms or analysis axes already exist.

The advisory does not block an explicitly requested new root.

## Generation guidance

Prefer structural changes over cosmetic variations. Useful root directions may:

- reverse a causal assumption;
- replace the unit of analysis;
- introduce a hidden state or feedback loop;
- reinterpret an anomaly as central evidence;
- import a distant-domain mechanism;
- treat the observed effect as bias, artifact, or selection;
- redefine the objective or success metric.

Do not force novelty by making the idea incoherent. The file must still state a plausible route,
a distinctive consequence, weaknesses, and verification questions.

## Output limit

Create at most one idea and three early-stop records. Early stops get no idea or index row. Do not
rank roots, compare bodies, verify, create children, or update the main project in the same run.
