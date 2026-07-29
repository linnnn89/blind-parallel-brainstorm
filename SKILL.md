---
name: blind-parallel-brainstorm
description: >
  Generate, verify, and deepen independent ideas inside a file-isolated brainstorm workspace.
  Use only when the user explicitly requests divergent exploration, alternative hypotheses,
  numbered idea files, validation of a selected idea, or development of reviewed branches such
  as 001-01. Root ideas do not read sibling bodies; verification reads one selected idea; child
  ideas inherit a controlled branch brief. Do not use for ordinary search, evidence summaries,
  rewriting, or tasks where the user did not request brainstorming.
---

# Blind Parallel Brainstorm

## Purpose

Create an auditable forest of independent ideas, remove clearly failed directions, and deepen
only the branches that survive review without allowing sibling reasoning to homogenize later
work.

The skill uses file-level context isolation:

- root ideas see a shared brief and title-only index, not other idea bodies;
- verification reads one numbered idea at a time;
- child ideas inherit a state-checked branch brief, not the parent's raw draft;
- clearly invalid ideas are labeled `BUSTED.<id>` in indexes while their file paths remain stable;
- speculative content stays quarantined until the user explicitly promotes it.

Do not expose or store private chain-of-thought. Store concise propositions, assumptions,
mechanisms, predictions, falsifiers, evidence, and decisions.

## Activation boundary

Use only when the user explicitly requests:

- brainstorming or divergent exploration;
- independent, unconventional, contrarian, or tail directions;
- creation of numbered idea files;
- verification of a selected numbered idea;
- development of a reviewed idea into child branches;
- synthesis or promotion of selected reviewed branches;
- resumption of an existing isolated brainstorm workspace.

Do not activate for ordinary retrieval, routine summaries, fact checking without hypothesis
generation, rewriting, or implementation of an already selected direction.

Uncertainty does not authorize brainstorming. Activation belongs to the user.

## Core invariants

1. Treat `brainstorm/` as speculative quarantine, not project truth.
2. Never recursively read the entire `brainstorm/` directory.
3. Before a primary operation, verify the managed workspace schema in `brainstorm/AGENTS.md`.
   Repair missing or legacy governance first; never promote a legacy review implicitly.
4. After initialization, perform exactly one primary operation per run:
   - `CREATE ROOT`
   - `VERIFY <idea-id>`
   - `CREATE CHILD <parent-id>`
   - `SYNTHESIZE <parent-id>`
5. A create run writes exactly one idea file.
6. A verify run reviews exactly one idea.
7. `CREATE ROOT` must not read idea or review bodies before drafting its candidate.
8. `CREATE CHILD` must not read the parent's raw idea, sibling bodies, or unrelated branches.
9. `VERIFY` must not read other idea bodies.
10. Original idea files are immutable. Accepted review bodies are immutable; only review lifecycle
   metadata may move `draft -> accepted -> superseded`.
11. Coherence, novelty, or confident language cannot establish truth.
12. No brainstorm content enters the main project without explicit user approval naming the ID.
13. Do not continue expanding in the background or without a new user invocation.
14. Only the current accepted review may publish evidence state; never branch from a stale or
    source-mismatched brief.
15. When coordinating concurrent workers, stop one only for a clear scope or protocol violation,
    not because its hypothesis looks weak. Clean up its reservation and preserve partial reviews
    as non-publishing drafts.

## Workspace layout

```text
brainstorm/
├── AGENTS.md
├── BRIEF.md
├── EVIDENCE_GATE.md
├── ROOT_INDEX.md
├── BUSTED.md
├── ideas/
├── reviews/
├── branch_briefs/
├── child_indexes/
└── reservations/
```

Use `templates/brainstorm/` when initializing a project.

`BRIEF.md` contains only stable shared context: the problem, confirmed facts, constraints,
exclusions, success criteria, and optional evidence boundary. It must not contain prior ideas,
rankings, preferred solutions, or hidden body summaries.

## Lazy reference loading

Do not load every manual on every run.

- Initialization, schema preflight, or interrupted-worker repair:
  `references/workspace-and-isolation.md`
- `CREATE ROOT`: `references/create-root.md`
- `VERIFY`: `references/verify-idea.md`
- `CREATE CHILD`: `references/create-child.md`
- Status, thresholds, branching, and repair: `references/lifecycle-and-governance.md`
- Optional exploration operators: `references/anti-collapse-and-exploration.md`
- Explicit convergence or promotion: `references/synthesis-and-promotion.md`

The root skill plus the current operation manual should normally be sufficient.

## Operation routing

### CREATE ROOT

Use for one new independent direction with no selected parent.

Initial allowed context:

- `AGENTS.md`
- `BRIEF.md`
- `ROOT_INDEX.md`
- title-only active reservations

Do not read `ideas/**`, `reviews/**`, or branch bodies.

Draft one candidate first. Only after the candidate exists in working memory, read the compact
failure ledger in `BUSTED.md` and run a collision check. If the candidate repeats a busted core
proposition, mechanism, prediction, or failure signature, discard it and retry at most twice.
Write only a candidate that passes this check.

### VERIFY <idea-id>

Assess the idea and evidence before reading prior review bodies, record the provisional
checkpoint, then always challenge its most decision-critical claim. Prior same-ID reviews are an
additional challenge input, not a prerequisite for Review B.

Start the review as `draft`. Only a validated `accepted` review may supersede the prior source and
update current state.

Allowed verdicts:

- `survives`
- `weakened`
- `blocked`
- `busted`

A busted idea keeps its stable file path, but its index display becomes `BUSTED.<idea-id>`, its
expansion closes, and a compact failure record is appended to `BUSTED.md`.

### CREATE CHILD <parent-id>

Use only when the parent is `survives` or `weakened`, has a controlled branch brief, and has
expansion status `open`.

Before drafting, compare the brief with the accepted review. Stop on stale state, source mismatch,
invalid transition, or missing metadata. Immature evidence, uncertain novelty, or a small pool
requires explicit user confirmation.

After this preflight, read only the shared brief, branch brief, direct-child title index,
title-only ancestry, and reservations. Do not read the parent's raw idea or sibling bodies.

Draft one child first, then compare it with compact busted signatures and existing child titles.
Retry at most twice on collision. The child must add a mechanism, prediction, test, boundary,
implementation, or repair. If it negates the parent, route it to a later `CREATE ROOT` run.

### SYNTHESIZE <parent-id>

Run only on explicit user request. Read only selected reviewed nodes and their reviews. Write a
separate synthesis artifact; do not rewrite original ideas or treat agreement as proof.

## Validation advisory

Brainstorming should not accumulate an indefinitely growing pile of unreviewed files.

Recommend switching to verification when any default threshold is reached:

```yaml
unreviewed_root_ideas: 6
unreviewed_children_per_parent: 3
total_unreviewed_active_ideas: 8
```

Also recommend verification earlier when the current pool already covers at least three
meaningfully different mechanisms or analysis axes.

This is an advisory, not a hard block. If the user explicitly requests another root, create it.
For a generic request such as "continue brainstorming," use this priority:

1. if the advisory threshold is reached, suggest `VERIFY` and name up to three unreviewed IDs;
2. otherwise, if viable open nodes exist, prefer vertical `CREATE CHILD` development;
3. create another root only for an uncovered direction or explicit user request.

## Busted idea memory

`BUSTED.md` is a compact negative-memory ledger, not a full archive. Detailed reasoning stays in
the idea's review file.

Each entry contains only:

- stable ID and title;
- failure class;
- one-sentence reason;
- compact collision signatures;
- scope: global, root, or parent-specific.

Recommended failure classes:

- `contradicts-facts`
- `duplicate`
- `no-new-information`
- `non-falsifiable`
- `unsupported-causal-leap`
- `scope-violation`
- `implementation-impossible`

Do not load this ledger before the initial creative draft. Use it after drafting as a negative
collision filter so previous failures are remembered without becoming the starting context.

## Identifier and lifecycle rules

Use zero-padded hierarchical identifiers:

- roots: `001`, `002`;
- children: `001-01`, `001-02`;
- grandchildren: `001-01-01`.

IDs encode logical inheritance. Do not rename files when status changes.

Idea status:

- `unreviewed`
- `survives`
- `weakened`
- `blocked`
- `busted`

Expansion status:

- `closed`
- `open`
- `frozen`
- `saturated`

Evidence state:

```text
speculative -> screened -> verified -> synthesis_ready -> protocol_ready
```

Evidence state is independent of idea and expansion status. Only an accepted review may publish a
one-step transition; synthesis or user approval may satisfy transition conditions but cannot
change state by itself. See `references/lifecycle-and-governance.md` for minimum conditions,
refreshes, and evidence-driven downgrades.

Only `survives` and qualified `weakened` nodes may open vertical branches. `blocked` nodes freeze;
`busted` nodes close permanently under the current evidence. Mark a branch saturated when
further children add no new mechanism, prediction, test, boundary, implementation, or repair.

Default limits:

```yaml
max_depth: 3
max_children_per_node: 5
max_active_nodes_per_root: 12
max_unreviewed_children_per_node: 3
```

## Promotion boundary

Promotion requires:

1. a current accepted review;
2. status `survives` or explicitly qualified `weakened`;
3. evidence state `synthesis_ready` or `protocol_ready`;
4. explicit user approval naming the ID;
5. visible uncertainty and counterevidence;
6. a concise copy into the main project, still labeled as hypothesis or proposal unless external
   evidence supports a stronger statement.

Never link the main project to the entire brainstorm forest.

## Output contract

After each operation, report only:

- operation performed;
- file created or reviewed;
- resulting idea, evidence, and expansion status, when applicable;
- whether a validation advisory was triggered;
- the next user-directed action.

Do not dump hidden sibling bodies. Do not claim that isolation proves novelty or correctness.

## Failure handling

Stop and report the blocker when:

- the requested ID does not exist;
- a child lacks a valid branch brief;
- the parent is busted, blocked, saturated, or otherwise closed;
- a candidate collides with busted signatures after two retries;
- required evidence is inaccessible;
- identifier reservation conflicts cannot be resolved safely;
- an interrupted operation left an idea/index mismatch or another ambiguous partial commit;
- the requested reads would violate isolation.

Never bypass isolation merely to be helpful.
