# Lifecycle and Governance Manual

Read this file only when changing status, deciding whether to branch, repairing indexes, or
promoting an idea.

## Idea status

- `unreviewed`: created but not independently assessed;
- `survives`: worth retaining after the current review;
- `weakened`: partially viable, usually requiring repair or narrower scope;
- `rejected`: core proposition should not be developed further under current evidence;
- `blocked`: cannot be judged with currently accessible evidence or tools.

## Expansion status

- `closed`: branching is not permitted;
- `open`: one child may be created per invocation within limits;
- `frozen`: wait for new evidence, data, or user input;
- `saturated`: further ideation is yielding no material increment.

Status and expansion status are independent. A viable idea can be saturated; a blocked idea can
be frozen.

## Default transitions

```text
unreviewed + closed
  -> VERIFY
  -> survives + open
  -> weakened + open|frozen
  -> rejected + closed
  -> blocked + frozen

open
  -> repeated low-increment children
  -> saturated
```

Do not reopen `rejected` or `saturated` branches without a stated reason such as new evidence,
a changed brief, or explicit user instruction.

## Branching limits

Default limits:

```yaml
max_depth: 3
max_children_per_node: 5
max_active_nodes_per_root: 12
max_unreviewed_children_per_node: 3
```

A child is active unless rejected, blocked, or explicitly archived.

## Saturation checks

Mark a node `saturated` when one or more conditions hold:

- all allowed expansion axes have been covered;
- all important open questions have corresponding children;
- two consecutive attempts produce only duplicate titles or restatements;
- no proposed child creates a new prediction, test, mechanism, boundary, implementation, or
  repair;
- the next useful step requires evidence rather than further ideation.

## Immutability

- idea bodies are immutable;
- reviews are append-only;
- indexes may update status fields but may not gain body summaries;
- branch briefs may be replaced by later verification, while preserving neutral scope;
- promotion creates a new reviewed summary outside `brainstorm/`; it does not move or rewrite
  the source idea.

## Promotion gate

Promotion requires explicit user approval naming the idea ID.

Before promotion, verify:

1. at least one review exists;
2. status is `survives` or qualified `weakened`;
3. important counterevidence is visible;
4. the destination document labels the content appropriately;
5. only the selected idea is exported.

The promoted summary should contain the proposition, evidence state, remaining uncertainty,
and recommended next test. It must not silently become a project requirement or established
fact.

## Synthesis boundary

Cross-idea synthesis is outside ordinary create and verify runs. It requires explicit user
instruction naming the roots or children to compare.

When synthesis is authorized, read only the selected reviewed nodes, not the entire forest.
Preserve original files and write a separate synthesis artifact.
