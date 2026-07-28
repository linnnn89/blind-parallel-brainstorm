---
name: blind-parallel-brainstorm
description: >
  Generate and develop independent ideas inside a file-isolated brainstorm workspace.
  Use when the user explicitly requests parallel brainstorming, alternative hypotheses,
  unconventional directions, or continued development of a numbered idea. Root ideas are
  created without reading sibling idea bodies; verification reads only one selected idea;
  child ideas inherit only a controlled branch brief. Do not use for ordinary search,
  evidence summaries, rewriting, or tasks where the user did not request divergence.
---

# Blind Parallel Brainstorm

## Purpose

Create independent, auditable idea branches without allowing existing idea bodies to anchor
or homogenize later generations.

The skill uses file-level context isolation:

- root ideas see the common problem brief and title-only index, but not other idea bodies;
- verification reads one numbered idea at a time;
- child ideas inherit a reviewed branch brief, not the parent's raw draft;
- speculative content remains quarantined from the main project until the user explicitly
  promotes it.

Do not expose or store private chain-of-thought. Store only concise hypotheses, assumptions,
mechanisms, predictions, falsifiers, evidence, and decisions.

## Use this skill when

Use only when the user explicitly requests one or more of the following:

- brainstorming or divergent exploration;
- independent alternative directions;
- unconventional, contrarian, or tail possibilities;
- creation of numbered idea files;
- verification of a selected numbered idea;
- development of an accepted idea into `001-01`, `001-02`, and deeper branches;
- resuming an existing isolated brainstorm workspace.

## Do not use this skill when

Do not activate for:

- ordinary web search or literature retrieval;
- routine evidence summaries;
- fact checking without a request for new hypotheses;
- rewriting, translation, or polishing;
- standard project implementation with an already selected direction;
- automatic expansion merely because evidence is uncertain or contradictory.

Uncertainty does not authorize brainstorming. Activation belongs to the user.

## Core invariants

These rules are non-negotiable.

1. Treat `brainstorm/` as a speculative quarantine, not project truth.
2. Never recursively read the entire `brainstorm/` directory.
3. After workspace initialization, each run must perform exactly one primary operation:
   - `CREATE ROOT`
   - `CREATE CHILD <parent-id>`
   - `VERIFY <idea-id>`
4. A create run produces exactly one new idea file.
5. A verify run reviews exactly one numbered idea.
6. `CREATE ROOT` must not read any idea or review body.
7. `CREATE CHILD` must not read sibling idea bodies or the parent's raw idea file.
8. `VERIFY` must not read other idea bodies unless the user explicitly requests a later
   synthesis operation outside the normal workflow.
9. Original idea files are immutable after creation. Corrections belong in review files or
   new child ideas.
10. An idea cannot be marked supported merely because it is coherent, novel, or confidently
    written.
11. No brainstorm content may enter the main project without explicit user approval.
12. Do not create background tasks or continue expanding without a new user invocation.

## Workspace layout

Initialize this structure inside the target project:

```text
brainstorm/
├── AGENTS.md
├── BRIEF.md
├── ROOT_INDEX.md
├── ideas/
│   ├── 001.md
│   ├── 001-01.md
│   └── 001-01-01.md
├── reviews/
│   ├── 001/
│   │   └── review-001.md
│   └── 001-01/
├── branch_briefs/
│   ├── 001.md
│   └── 001-01.md
├── child_indexes/
│   ├── 001.md
│   └── 001-01.md
└── reservations/
```

Use the templates in `templates/brainstorm/` when creating the workspace.

## Lazy reference loading

Do not load every manual on every run.

- For workspace creation, read `references/workspace-and-isolation.md`.
- For `CREATE ROOT`, read `references/create-root.md` only.
- For `VERIFY`, read `references/verify-idea.md` only.
- For `CREATE CHILD`, read `references/create-child.md` only.
- For status transitions, branching limits, or promotion questions, read
  `references/lifecycle-and-governance.md`.

The root skill and the operation-specific manual should normally be sufficient.

## One-time initialization

If `brainstorm/` does not exist, initialize it before the first operation.

Initialization may create the workspace files and then continue with the one requested
operation. It must not import existing project speculation into `BRIEF.md` without the user's
approval.

`BRIEF.md` contains only stable shared context:

- problem or objective;
- confirmed facts supplied by the user or main project;
- fixed constraints;
- explicit exclusions;
- success criteria;
- optional evidence boundary.

It must not contain prior brainstorm ideas, preferred solutions, rankings, or hidden summaries
of idea bodies.

## Operation routing

Infer the smallest matching operation from the user's explicit request.

### CREATE ROOT

Use when the user asks for a new independent direction without selecting a parent.

Allowed context:

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- `brainstorm/ROOT_INDEX.md`
- active root reservations, title only

Forbidden context:

- `brainstorm/ideas/**`
- `brainstorm/reviews/**`
- `brainstorm/branch_briefs/**`
- idea summaries hidden in other files

Output exactly one new root idea such as `ideas/001.md`, then append only its title and status
to `ROOT_INDEX.md`.

### VERIFY <idea-id>

Use when the user names an idea number or asks to assess a selected branch.

Allowed context:

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- the selected `ideas/<idea-id>.md`
- earlier reviews under `reviews/<idea-id>/`, if any
- project files and external evidence strictly needed to test that idea

Forbidden context:

- sibling idea bodies;
- unrelated branch briefs;
- other reviews;
- title-based assumptions about other ideas.

Write a new append-only review under `reviews/<idea-id>/review-NNN.md`.

If the idea survives and has meaningful unresolved dimensions, the verifier may also create or
replace a controlled `branch_briefs/<idea-id>.md` and open its child index. This is part of
verification, not a separate brainstorm generation.

### CREATE CHILD <parent-id>

Use only when the parent has a branch brief and its expansion status is open.

Allowed context:

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- `brainstorm/branch_briefs/<parent-id>.md`
- `brainstorm/child_indexes/<parent-id>.md`
- title-only ancestry needed to preserve scope

Forbidden context:

- the parent's raw idea file;
- sibling idea bodies;
- unrelated branches and reviews.

Create exactly one child such as `001-01.md`. A child must refine, implement, bound, test, or
repair the parent. If it negates the parent's core proposition, create a new root instead.

## Identifier rules

Use zero-padded hierarchical identifiers:

- roots: `001`, `002`, `003`;
- children: `001-01`, `001-02`;
- grandchildren: `001-01-01`.

Identifiers encode logical inheritance, not merely topical grouping.

When concurrent creation is possible, reserve the identifier in `reservations/` before writing.
A reservation may expose only the ID, parent, expansion axis, and working title.

## Idea admission requirements

Every new idea must include:

- one clear core proposition;
- the default assumption it changes or extends;
- a plausible mechanism or implementation path;
- at least one distinctive consequence or prediction;
- visible weaknesses;
- concrete questions for later verification.

Reject a proposed child before writing if it only restates the parent or an existing title.
Do not require an idea to be proven during creation.

## Verification requirements

Verification must distinguish:

- internal coherence;
- consistency with confirmed facts;
- supporting evidence;
- counterevidence;
- simpler alternative explanations;
- differentiating predictions;
- falsification conditions;
- feasible next tests.

Allowed verdicts:

- `survives`
- `weakened`
- `rejected`
- `blocked`

`survives` means worth retaining after the current review. It does not mean confirmed.

## Development and branching

A verified idea may be expanded only when:

- its status is `survives` or `weakened`;
- its core proposition can be stated clearly;
- unresolved questions remain;
- a child can add new information;
- its expansion status is `open`.

Children may develop one primary axis:

- mechanism;
- implementation or operationalization;
- boundary condition;
- validation route;
- defect repair;
- extreme or differentiating prediction.

Do not mix several axes into one oversized child unless they are inseparable.

Default limits:

```yaml
max_depth: 3
max_children_per_node: 5
max_active_nodes_per_root: 12
max_unreviewed_children_per_node: 3
```

Mark expansion `saturated` when further creation produces only repetitions, all major axes are
covered, or the next useful step requires external data rather than more speculation.

## Main-project isolation and promotion

Project agents should normally see only that a `brainstorm/` workspace exists. They must not
recursively ingest it.

An idea may be promoted only when:

1. it has at least one independent review;
2. its current status is `survives` or explicitly qualified `weakened`;
3. the user names the idea and approves promotion;
4. the promoted text remains labeled as a proposal, hypothesis, or pending validation unless
   external evidence supports a stronger statement.

Promotion should copy a concise reviewed summary into the main project. Do not link the main
project to the entire brainstorm tree.

## Output contract

After each operation, report only:

- operation performed;
- file created or reviewed;
- resulting status, when applicable;
- whether expansion is open, closed, frozen, or saturated;
- the next available user-directed action.

Do not dump hidden idea bodies from other branches. Do not claim that isolation proves novelty
or correctness.

## Failure handling

Stop and report the blocker when:

- the requested idea ID does not exist;
- a child is requested but no valid branch brief exists;
- the parent is rejected or expansion is closed;
- required project evidence is inaccessible;
- identifier reservation conflicts cannot be resolved safely;
- reading the requested files would violate isolation rules.

Never bypass isolation merely to be helpful.
