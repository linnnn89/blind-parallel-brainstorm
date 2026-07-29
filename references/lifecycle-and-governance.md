# Lifecycle and Governance Manual

Read this file only when changing status, deciding whether to branch, repairing indexes,
handling busted memory, or promoting an idea.

## Idea status

- `unreviewed`: created but not assessed;
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

## Review lifecycle and current-state source

Review lifecycle is:

```text
draft -> accepted -> superseded
draft ------------> superseded
```

- `draft` may be completed or corrected but cannot update current evidence state, indexes, or a
  branch brief.
- `accepted` has passed the review, transition, and evidence-gate checks.
- `superseded` remains as history but cannot publish current state.

The current evidence-state source is the highest numbered same-ID review whose
`review_status` is `accepted`. Its `review_id` must be unique and monotonically increasing. When a
new review is accepted, set the previous accepted review's lifecycle metadata to `superseded` and
link the two with `supersedes_review` and `superseded_by`. Review bodies become immutable once
accepted; only these lifecycle fields may change afterward.

If no accepted review exists, the immutable idea front matter is the source and its evidence state
is `speculative`. Draft and superseded reviews never override it. Multiple unlinked accepted
reviews, duplicate review IDs, or an accepted review whose predecessor is not identified are
invalid lifecycle metadata and block branching.

If interruption leaves a valid new accepted review and its linked predecessor both marked
`accepted`, validate the new transition and link, then finish the predecessor's permitted
`accepted -> superseded` metadata change. Do not use this repair for unlinked or invalid reviews.

## Evidence state

Evidence state records maturity, not whether the idea is favorable:

```text
speculative -> screened -> verified -> synthesis_ready -> protocol_ready
```

Upgrades may advance only one step per accepted review. Synthesis or user approval may satisfy a
transition condition but cannot publish state by itself. Do not infer or skip an intermediate
state even when one review appears comprehensive.

Minimum conditions:

### `speculative -> screened`

- the question and evidence boundary are explicit;
- a targeted eligibility and novelty screen has been performed;
- supporting evidence, counterevidence, unknowns, and blockers are recorded;
- quantity, quality, novelty, and feasibility each have a concise gate assessment;
- a compact evidence checkpoint identifies every claim allowed into a branch brief.

### `screened -> verified`

- state-bearing claims have been checked against primary, full-text, registry, dataset, or other
  authoritative sources appropriate to the domain;
- eligibility, extractability, duplicates, and material contradictions have been resolved or
  explicitly marked unresolved;
- the evidence checkpoint supplies source references and confidence for each inherited claim;
- the evidence gate and required review metadata are complete.

Verification may show that an idea should freeze or be busted. Evidence maturity does not imply a
positive verdict.

### `verified -> synthesis_ready`

- an authorized synthesis has been completed for the selected scope;
- the idea is `survives` or explicitly qualified `weakened`;
- the research gate decision is `continue`;
- decisive evidence, counterevidence, uncertainty, and alternatives are current;
- no unresolved blocking issue prevents comparison or synthesis;
- further useful work is synthesis rather than more exploratory children.

### `synthesis_ready -> protocol_ready`

- the user explicitly approves the named idea for protocol preparation;
- the synthesis has fixed the research scope, primary question, evidence boundary, and
  major feasibility assumptions;
- remaining uncertainties and reopen conditions are visible;
- the research gate remains `continue` and the promotion boundary is satisfied.

A same-state accepted review is a refresh and must increment `evidence_revision`. An accepted
review may downgrade evidence state when new evidence invalidates earlier support, but it must name
the new evidence and reason. `protocol_ready` is never automatic.

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

## Research kill gate

Use `EVIDENCE_GATE.md` to assess quantity, quality, novelty, feasibility, and blockers without a
weighted score. A stop-level `fail` should freeze expansion, not delete or automatically bust the
idea. Record `blocking_issue` and `reopen_condition`; only a new accepted review may publish a
reopened state.

## CREATE CHILD state-integrity gate

Apply the hard blocks and soft warnings defined in `create-child.md`. Hard state-integrity blocks
are not user-overridable. Soft warnings require one explicit confirmation naming the parent and
warning codes and do not mutate lifecycle state.

## Early-stop archive

An early stop is a coherent candidate terminated before formal idea creation by an explicit
pre-create hard gate or a bounded worker termination. It is not an idea status, accepted review,
evidence state, or busted verdict.

Assign a stable `ES-YYYYMMDD-NN` archive ID and append a compact record to `EARLY_STOPS.md`.
Early-stop records have no idea file, index row, review, branch brief, or expansion status:

- `source-checked` requires traceable locators and may produce a later post-draft collision
  warning;
- `unverified` preserves a candidate for possible reconsideration but cannot filter later work;
- every record names uncertainty and an observable reopen condition;
- a matching record never automatically busts or publishes state for a new candidate.

Use the current project date and next unused two-digit sequence for `NN`. When workers are used,
the coordinator assigns IDs and appends records serially.

Do not convert a retained backup into an early stop merely because it is `unreviewed + closed`.
That node is already a formal idea and remains governed by normal verification.

Reconsideration requires explicit user instruction naming one `ES-*` record. Read only that
record, explain why the old blocker may no longer apply, run a normal CREATE operation, and set
the new idea's optional `origin_early_stop` field. The archive record remains unchanged.

## Busted memory

A busted idea keeps its stable file path. Do not rename `ideas/<id>.md`.

Update its owning index row to:

- display label: `BUSTED.<id>`;
- idea status: `busted`;
- expansion status: `closed`.

Append one concise record to `BUSTED.md`. The ledger is negative memory for collision checking,
not a substitute for the detailed review.

Do not store pre-create early stops in `BUSTED.md`. Every busted record must remain traceable to a
formal idea and current accepted review with verdict `busted`.

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
- review bodies are editable only while `draft` and immutable after acceptance;
- accepted review lifecycle metadata may change only from `accepted` to `superseded`, with a
  forward link to the replacing review;
- indexes may update label and status fields but may not gain body summaries;
- `BUSTED.md` is append-only except to correct a factual clerical error;
- `EARLY_STOPS.md` is append-only except to correct a factual clerical error;
- branch briefs may be replaced only from the current accepted review while preserving neutral
  scope and provenance;
- promotion creates a new reviewed summary outside `brainstorm/`; it does not move or rewrite
  the source idea.

## Promotion gate

Promotion requires explicit user approval naming the idea ID.

Before promotion, verify:

1. a current accepted review exists;
2. status is `survives` or qualified `weakened`;
3. evidence state is `synthesis_ready` or `protocol_ready`;
4. important counterevidence is visible;
5. the destination labels the content appropriately;
6. only the selected idea is exported.

The promoted summary contains the proposition, evidence state, remaining uncertainty, and
recommended next test. It must not silently become a project requirement or established fact.

## Synthesis boundary

Cross-idea synthesis is outside ordinary create and verify runs. It requires explicit user
instruction naming the roots or children to compare.

When synthesis is authorized, read only selected reviewed nodes, not the entire forest. Do not
read busted branches unless the user explicitly requests failure analysis. Preserve original
files and write a separate synthesis artifact.
