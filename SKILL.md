---
name: blind-parallel-brainstorm
description: >
  Generate, verify, and deepen independent ideas in a file-isolated brainstorm workspace, either
  as one atomic operation or a leader-coordinated asynchronous campaign. Use when the user
  explicitly requests divergent ideation, numbered hypotheses, verification, or reviewed branch
  development, especially for medical and biomedical research. Also supports other research and
  software ideation; ordinary retrieval, summaries, and rewriting remain outside scope.
---

# Blind Parallel Brainstorm

## Purpose

Create an auditable forest of independent ideas, test one numbered idea at a time, and deepen
reviewed branches without allowing sibling reasoning to homogenize later work. File-level
isolation preserves these boundaries:

- root ideas see a shared brief and title-only index, not other idea bodies;
- verification reads one numbered idea at a time;
- child ideas inherit a state-checked branch brief, not the parent's raw draft;
- candidates stopped before formal creation receive separate `ES-*` archive records;
- clearly invalid ideas are labeled `BUSTED.<id>` in indexes while their file paths remain stable;
- speculative content stays quarantined until the user explicitly promotes it.

Persist concise propositions, assumptions, mechanisms, predictions, falsifiers, evidence, and
decisions.

## Activation boundary

Activate only when the user explicitly requests:

- brainstorming or divergent exploration;
- independent, unconventional, contrarian, or tail directions;
- creation of numbered idea files;
- verification of a selected numbered idea;
- development of a reviewed idea into child branches;
- synthesis or promotion of selected reviewed branches;
- a bounded asynchronous campaign of independent roots, reviews, or reviewed descendants;
- resumption of an existing isolated brainstorm workspace.

Ordinary retrieval, routine summaries, fact checking without hypothesis generation, rewriting,
and implementation of an already selected direction remain outside this skill.

## Core invariants

1. Treat `brainstorm/` as speculative quarantine rather than project truth, and never recursively
   read it.
2. Before each primary operation, check the schema marker and required-path existence exactly as
   defined in `references/workspace-and-isolation.md`. The current schema is `3`; a mismatch,
   missing path, or interrupted commit routes to that manual before other work.
3. Each worker invocation performs exactly one primary operation:
   - `CREATE ROOT`
   - `VERIFY <idea-id>`
   - `CREATE CHILD <parent-id>`
   - `SYNTHESIZE <parent-id>`
   A user-authorized campaign may coordinate several such invocations without changing this
   worker boundary.
4. Apply the operation-specific read boundary:
   - root creation uses the shared brief, root title index, and title-only reservations;
   - verification uses one idea, its own review history, and evidence needed to test it;
   - child creation uses a current state-checked branch brief and title-only ancestry or indexes;
   - synthesis uses only explicitly selected reviewed nodes.
5. A successful CREATE writes one idea. A VERIFY reviews one idea. Creation and verification
   remain separate operations.
6. Original idea bodies and accepted review bodies are immutable. Only the current accepted
   review publishes evidence state; branch creation requires a matching current brief.
7. `early_stop` records remain outside the idea tree. `busted` is a verdict for a formal idea and
   closes that idea while preserving its stable path.
8. Base verdicts and evidence states on observable support, counterevidence, and uncertainty;
   coherence or confident wording is not evidence.
9. Promotion requires explicit user approval naming the selected idea. Synthesis remains a
   separately authorized operation.
10. In a campaign, the main agent owns dispatch, portfolio balance, final evaluation, and
    reporting. Workers stay within their assignment and return after one operation.
11. Concurrent creative assignments need distinct primary contributions. Concentrated fan-out
    requires a current accepted branchable review and valid open brief, while eligible sibling
    lineages and uncovered root directions retain capacity.
12. When a campaign reaches its goal or boundary, freeze new dispatches, drain compliant in-flight
    operations, report the portfolio, and return control to the user.

## Workspace layout

```text
brainstorm/
├── AGENTS.md
├── BRIEF.md
├── EVIDENCE_GATE.md
├── ROOT_INDEX.md
├── BUSTED.md
├── EARLY_STOPS.md
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

## Reference routing

Load only the reference required by the current operation and active mode or domain.

| Situation | Reference |
|---|---|
| Initialization, schema mismatch, or interrupted work | `references/workspace-and-isolation.md` |
| `CREATE ROOT` | `references/create-root.md` |
| `VERIFY <idea-id>` | `references/verify-idea.md` |
| `CREATE CHILD <parent-id>` | `references/create-child.md` |
| Asynchronous or multi-agent campaign | `references/leader-campaign.md` |
| Medical, biomedical, clinical, epidemiological, or public-health work | `references/medical-research-profile.md` |
| State, thresholds, branching, archive records, or repair | `references/lifecycle-and-governance.md` |
| Tail-exploration operators | `references/anti-collapse-and-exploration.md` |
| Explicit synthesis or promotion | `references/synthesis-and-promotion.md` |

The root skill, current operation manual, and any activated campaign or domain profile should
normally be sufficient.

## Operation and mode selection

- `CREATE ROOT` creates one independent direction without a selected parent.
- `VERIFY <idea-id>` tests one idea and publishes state only through a valid accepted review.
- `CREATE CHILD <parent-id>` develops one reviewed, branchable parent through its controlled brief.
- `SYNTHESIZE <parent-id>` compares explicitly selected reviewed nodes on user request.

For a user-authorized campaign, load `references/leader-campaign.md` before dispatch. The main
agent fixes stable `SC-*` criteria, schedules non-overlapping atomic work as capacity becomes
available, balances verification with breadth and reviewed depth, and judges completion.

For medical work, also load `references/medical-research-profile.md`. Route the question by its
scientific or clinical function, activate only decision-relevant dimensions, and keep association,
prediction, mechanism, intervention effect, and clinical recommendation as distinct claims.

## Lifecycle authority

Use `references/lifecycle-and-governance.md` as the authority for identifiers, review and evidence
transitions, validation thresholds, branching limits, saturation, `BUSTED.md`, `EARLY_STOPS.md`,
and state repair. Operation manuals own their read boundaries and commit procedures;
`references/synthesis-and-promotion.md` owns convergence and promotion requirements.

For a generic request to continue, select the legal operation with the largest unresolved
information value: verify an important claim, develop a reviewed open branch, or add a genuinely
uncovered root direction. Validation thresholds create review pressure rather than a universal
depth-first queue. Campaign scheduling follows the balanced frontier in
`references/leader-campaign.md`.

## Output contract

After an atomic operation, report:

- operation performed;
- file created or reviewed;
- resulting idea, evidence, and expansion state when applicable;
- any archive, resolution, validation, or blocker event;
- the next user-directed action.

After a campaign, provide a compact leader view:

- whether each success criterion is met, unmet, or blocked;
- completed operations and retained high-potential IDs with their current states;
- breadth, depth, and verification coverage;
- unresolved blockers, important uncertainty, and the next user decision.

Keep hidden sibling bodies outside the report. Isolation supports independence; accepted evidence
and review state determine what conclusions are justified.

## Failure handling

Stop the current operation and report when the target is missing or ineligible, the requested read
would violate isolation, required state or evidence is unavailable, or a reservation, commit, or
repair cannot complete safely. Load the workspace or lifecycle manual for deterministic recovery.

When a campaign reaches an agreed boundary before its criteria are met, freeze new dispatches,
drain compliant work, and report the target as unmet with the blocking condition and next user
decision.
