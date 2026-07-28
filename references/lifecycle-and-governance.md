# Lifecycle and Governance Manual

Read this file only when changing status, deciding whether to branch, repairing indexes,
handling busted memory, or promoting an idea.

## Idea status

- `unreviewed`: created but not independently assessed;
- `survives`: worth retaining after the current review;
- `weakened`: partially viable, usually requiring repair or narrower scope;
- `blocked`: cannot be judged with currently accessible evidence or tools;
- `busted`: core proposition should not be developed further under current evidence.

## Expansion status

- `closed`: branching is not permitted;
- `open`: one child may be created per invocation within limits;
- `frozen`: wait for new evidence, data, or user input;
- `saturated`: further ideation is yielding no material increment.

Status and expansion status are independent. A viable idea can be saturated; a blocked idea is
normally frozen.

## Default transitions

```text
unreviewed + closed
  -> VERIFY
  -> survives + open|saturated
  -> weakened + open|frozen
  -> blocked + frozen
  -> busted + closed

open
  -> repeated low-increment children
  -> saturated
```

Do not reopen `busted` or `saturated` branches without a stated reason such as new evidence, a
changed brief, or explicit user instruction. Reopening a busted branch also requires explaining
why its recorded failure signature no longer applies.

## Validation advisory

Recommend verification when any condition is reached:

```yaml
unreviewed_root_ideas: 6
unreviewed_children_per_parent: 3
total_unreviewed_active_ideas: 8
```

Recommend verification earlier when at least three meaningfully different mechanisms or analysis
axes are already represented.

The advisory is not a hard block. When the user says only "continue" or "keep brainstorming,"
use this priority:

1. advise `VERIFY` when thresholds are reached;
2. otherwise prefer `CREATE CHILD` on `survives` or qualified `weakened` nodes with open
   expansion;
3. recommend another `CREATE ROOT` only for an uncovered direction or explicit request.

Name at most three suggested IDs so the user retains control without receiving a long queue.

## Busted memory

A busted idea keeps its stable file path. Do not rename `ideas/<id>.md`.

Update its owning index row to:

- display label: `BUSTED.<id>`;
- idea status: `busted`;
- expansion status: `closed`.

Append one concise record to `BUSTED.md`. The ledger is negative memory for collision checking,
not a substitute for the detailed review.

Recommended failure classes:

- `contradicts-facts`
- `duplicate`
- `no-new-information`
- `non-falsifiable`
- `unsupported-causal-leap`
- `scope-violation`
- `implementation-impossible`

Collision signatures should be short structural descriptions, not prose essays. Examples:

- `cross-sectional association -> claims feedback causality`
- `same mechanism and prediction as root 002`
- `cannot produce a discriminating test`

Use scope to avoid overgeneralizing one failed branch:

- `global`
- `root:<root-id>`
- `parent:<parent-id>`

## Branching limits

Default limits:

```yaml
max_depth: 3
max_children_per_node: 5
max_active_nodes_per_root: 12
max_unreviewed_children_per_node: 3
```

A child is active unless busted, blocked, or explicitly archived.

## Saturation checks

Mark a node `saturated` when one or more conditions hold:

- all allowed expansion axes have been covered;
- all important open questions have corresponding children;
- two consecutive attempts produce only duplicate titles or busted collisions;
- no proposed child creates a new prediction, test, mechanism, boundary, implementation, or
  repair;
- the next useful step requires evidence rather than further ideation.

## Immutability

- idea bodies are immutable;
- reviews are append-only;
- indexes may update label and status fields but may not gain body summaries;
- `BUSTED.md` is append-only except to correct a factual clerical error;
- branch briefs may be replaced by later verification while preserving neutral scope;
- promotion creates a new reviewed summary outside `brainstorm/`; it does not move or rewrite
  the source idea.

## Promotion gate

Promotion requires explicit user approval naming the idea ID.

Before promotion, verify:

1. at least one review exists;
2. status is `survives` or qualified `weakened`;
3. important counterevidence is visible;
4. the destination labels the content appropriately;
5. only the selected idea is exported.

The promoted summary contains the proposition, evidence state, remaining uncertainty, and
recommended next test. It must not silently become a project requirement or established fact.

## Synthesis boundary

Cross-idea synthesis is outside ordinary create and verify runs. It requires explicit user
instruction naming the roots or children to compare.

When synthesis is authorized, read only selected reviewed nodes, not the entire forest. Do not
read busted branches unless the user explicitly requests failure analysis. Preserve original
files and write a separate synthesis artifact.
