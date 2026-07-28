# Minimal Workflow Example

Assume a project asks: "How could a clinical risk model capture information missed by one-time
biomarker measurements?"

## 1. Initialize

Create `brainstorm/` from the templates and place only the stable question, confirmed facts,
constraints, exclusions, and success criteria in `BRIEF.md`.

## 2. Create independent roots

Run `CREATE ROOT` several times in separate invocations. Each run reads only the brief and the
root title index.

Possible title-only index:

```markdown
| ID | Title | Idea status | Expansion status | Child count |
|---:|---|---|---|---:|
| 001 | Model biomarker variability rather than a single level | unreviewed | closed | 0 |
| 002 | Treat the observed association as visit-selection bias | unreviewed | closed | 0 |
| 003 | Replace individual measurements with latent state transitions | unreviewed | closed | 0 |
```

The agents that created 002 and 003 did not read 001's body.

## 3. Verify one root

Run:

```text
VERIFY 001
```

The verifier reads only `001.md`, its own review history, the common brief, and relevant external
evidence. If the idea survives, the verifier creates a neutral `branch_briefs/001.md`.

## 4. Develop one branch

Run:

```text
CREATE CHILD 001
```

The child creator reads the branch brief and child title index, but not `001.md` or sibling
bodies. It may create:

```text
001-01  Variability as repeated metabolic stress
```

A later invocation may create:

```text
001-02  Variability as feedback-control instability
```

## 5. Verify children independently

Run `VERIFY 001-01` and `VERIFY 001-02` separately. Each verifier remains blind to the other
child body.

## 6. Stop conceptual expansion when evidence is needed

Mark a branch `saturated` when further children add no new prediction or when the next useful
step is a longitudinal dataset, simulation, implementation test, or experiment.

## 7. Promote only by explicit user choice

A reviewed idea enters the main project only after the user names its ID and approves promotion.
The exported text remains labeled as a hypothesis or proposal unless external evidence supports
stronger wording.
