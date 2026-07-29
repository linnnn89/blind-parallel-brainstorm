# Minimal Workflow Example

Assume a project asks: "How could a clinical risk model capture information missed by one-time
biomarker measurements?"

## 1. Initialize

Create `brainstorm/` from the templates and place only the stable question, confirmed facts,
constraints, exclusions, and success criteria in `BRIEF.md`.

## 2. Create independent roots

Run `CREATE ROOT` in separate invocations. Each run drafts from the brief and title-only index,
then checks the compact busted ledger before writing.

Possible title-only index:

```markdown
| ID | Display | Title | Idea status | Expansion status | Child count |
|---:|---|---|---|---|---:|
| 001 | 001 | Model biomarker variability rather than a single level | unreviewed | closed | 0 |
| 002 | 002 | Treat the observed association as visit-selection bias | unreviewed | closed | 0 |
| 003 | 003 | Replace individual measurements with latent state transitions | unreviewed | closed | 0 |
```

The agents that created 002 and 003 did not read 001's body.

## 3. Switch to verification before the pool becomes cluttered

When the default threshold is reached, the skill recommends `VERIFY` rather than silently adding
more roots. The user still controls whether to follow that advice.

Run:

```text
VERIFY 001
```

The verifier completes a source-first Review A before reading prior review bodies, then performs a
bounded Review B challenge and adjudication. Even on the first review, Review B records the
challenged claim, disconfirming check, result, and verdict or gate impact. It starts the new review
as `draft`. Only an `accepted` review may publish the next one-step evidence state and generate
`branch_briefs/001.md`.

## 4. Record a busted direction without renaming its file

Suppose `VERIFY 002` finds that the idea merely duplicates a known selection model and adds no
new prediction. The original path remains:

```text
ideas/002.md
```

The index becomes:

```markdown
| 002 | BUSTED.002 | Treat the observed association as visit-selection bias | busted | closed | 0 |
```

A compact record is appended to `BUSTED.md`; the detailed reasoning remains in
`reviews/002/review-001.md`.

## 5. Develop a surviving branch vertically

Run:

```text
CREATE CHILD 001
```

Before drafting, the child creator compares the branch brief with the current accepted review.
For example, if `review-002.md` is accepted but the brief still cites `review-001.md`, it stops
without writing:

```text
HARD BLOCK: SOURCE_REVIEW_MISMATCH
```

If the source ID matches but a checkpoint value differs, it stops with
`STALE_BRANCH_BRIEF`.

After the brief is regenerated from the accepted review, `screened` evidence or uncertain novelty
produces one grouped warning. The user must explicitly confirm parent `001` and the warning codes.
The child creator then reads the validated brief and child title index, but not `001.md` or sibling
bodies. It may create:

```text
001-01  Variability as repeated metabolic stress
```

A later invocation may create:

```text
001-02  Variability as feedback-control instability
```

If three direct children remain unreviewed, the skill recommends verifying them before adding a
fourth.

## 6. Verify children independently

Run `VERIFY 001-01` and `VERIFY 001-02` separately. Each verifier remains blind to the other child
body.

## 7. Stop conceptual expansion when evidence is needed

Mark a branch `saturated` when further children add no new prediction or when the next useful step
is a longitudinal dataset, simulation, implementation test, or experiment.

## 8. Promote only by explicit user choice

An idea reaches `synthesis_ready` and then `protocol_ready` only through one-step transitions in
accepted reviews. It enters the main project only after the user names its ID and approves
promotion. The exported text remains labeled as a hypothesis or proposal unless external evidence
supports stronger wording.
