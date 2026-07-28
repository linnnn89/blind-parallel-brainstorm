# CREATE ROOT Manual

Read this file only for `CREATE ROOT`.

## Allowed reads

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- `brainstorm/ROOT_INDEX.md`
- active root reservations, title only

Do not read any file under `ideas/`, `reviews/`, `branch_briefs/`, or `child_indexes/`.

## Procedure

1. Restate the problem internally from `BRIEF.md` without importing outside proposals.
2. Scan root titles only to avoid direct title conflict.
3. Choose one meaningfully distinct direction.
4. Reserve the next three-digit root ID when concurrency is possible.
5. Write exactly one `ideas/NNN.md` from the idea template.
6. Append one title-only row to `ROOT_INDEX.md`.
7. Remove the reservation and stop.

## Distinctness rule

A title conflict exists when the new direction has the same core proposition as an indexed
root, even if phrased differently.

A title similarity alone does not justify reading the existing idea body. Either choose another
direction or report that a comparison requires a separate, explicitly authorized synthesis.

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

Create one idea only. Do not rank roots, compare bodies, verify the new idea, create children,
or update the main project in the same run.
