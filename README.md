# Blind Parallel Brainstorm

[中文说明](README.zh-CN.md)

A file-isolated agent skill for generating independent ideas, verifying one numbered idea at a
time, removing clearly failed directions, and developing reviewed ideas into controlled branches
such as `001-01` and `001-02`, while archiving coherent candidates stopped before formal creation.

## Why

Ordinary multi-round brainstorming often collapses toward the first plausible ideas because later
generations read and imitate earlier reasoning. This skill reduces that anchoring through strict
context boundaries:

- root creation sees only a shared brief and title-only root index;
- verification reads one selected idea and its own review history;
- child creation reads a state-checked branch brief instead of the parent's raw draft;
- sibling idea bodies remain hidden;
- pre-create gate failures receive separate `ES-*` archive records without entering the idea tree;
- failed structures are remembered through compact busted signatures, not full failed narratives;
- brainstorm content stays outside the main project until explicit promotion.

Isolation improves independence. It does not prove novelty or correctness.

## Operations

After one-time workspace initialization, a run performs exactly one primary operation:

```text
CREATE ROOT
VERIFY 001
CREATE CHILD 001
SYNTHESIZE 001
```

A successful create run writes one idea. A bounded failed attempt may append early-stop records
but creates no idea or index rows for those candidates. A verify run reviews one idea. The skill
does not continue in the background and does not automatically expand uncertainty into
brainstorming.

## Development cadence

```text
limited horizontal roots
  -> validation advisory
  -> VERIFY individual ideas
  -> survives / weakened / blocked / busted
  -> vertical children only from viable reviewed nodes
  -> explicit synthesis and promotion
```

Default validation advice is triggered at 6 unreviewed roots, 3 unreviewed children under one
parent, or 8 active unreviewed ideas in total. The advice is not a hard block: explicit user
instructions still control the next operation.

Once viable roots exist, generic continuation should prefer vertical development over endlessly
adding more roots.

## Evidence-state control

Evidence maturity advances without skipping:

```text
speculative -> screened -> verified -> synthesis_ready -> protocol_ready
```

Only the current accepted review publishes evidence state. A branch brief records that review and
revision; `CREATE CHILD` stops on stale or mismatched state. Immature evidence, uncertain novelty,
or a small evidence pool produces a user-confirmable warning rather than an automatic rejection.
The research evidence gate can freeze a branch without deleting it.

Review B always challenges one decision-critical Review A claim, including on the first review,
and records the check's effect on the verdict or gate.

## Early-stop archive

`EARLY_STOPS.md` preserves coherent candidates terminated before formal creation by an explicit
pre-create hard gate. Each `ES-YYYYMMDD-NN` record stores the candidate scope, stop reason,
evidence locators, uncertainty, reopen condition, and compact collision signatures.

Early stops are not idea statuses, accepted reviews, or busted verdicts. They do not enter
indexes or branches. Only unique, complete, source-checked, unresolved records may warn;
unverified or incomplete records are archival. Reconsideration requires the user to name one
`ES-*` record, explain the changed blocker, and append a complete `ER-*` resolution event after
the new idea and index commit.

## Busted ideas

A clearly invalid idea keeps its stable file path but is displayed in indexes as
`BUSTED.<idea-id>`. Its expansion closes and a compact entry is appended to `BUSTED.md` with:

- failure class;
- one-sentence reason;
- short collision signatures;
- applicable scope.

CREATE operations first draft independently, then check the compact ledger. This remembers failed
structures without making them the starting context for new creativity.

## Repository structure

```text
SKILL.md
references/
  workspace-and-isolation.md
  create-root.md
  verify-idea.md
  create-child.md
  lifecycle-and-governance.md
  anti-collapse-and-exploration.md
  synthesis-and-promotion.md
templates/brainstorm/
  AGENTS.md
  BRIEF.md
  EVIDENCE_GATE.md
  ROOT_INDEX.md
  BUSTED.md
  EARLY_STOPS.md
  idea.md
  review.md
  branch-brief.md
  child-index.md
  reservation.md
```

The root skill checks the `AGENTS.md` schema marker plus managed-path existence without reading
file contents. It loads the repair manual only for initialization, mismatch, missing structure, or
interrupted work. Migration creates required paths first and writes the schema marker last; an
existing mismatched `AGENTS.md` is never replaced without explicit user confirmation.

## Core safety properties

- No recursive brainstorm-directory reads.
- No sibling-body reads during creation or verification.
- Original ideas are immutable; accepted review bodies and busted records preserve history.
- Early-stop records remain outside idea indexes and cannot publish evidence state.
- Incomplete, duplicate, unverified, or resolved early stops cannot filter later candidates.
- Draft and superseded reviews cannot publish evidence state.
- Stale or source-mismatched branch briefs cannot create children.
- Busted labels never rename the underlying idea files.
- Coherence and confident language are not evidence.
- `survives` means worth retaining, not confirmed.
- No promotion to the main project without explicit user approval naming the idea.
- No automatic brainstorming for ordinary research or summaries.

## Typical prompts

```text
Use blind-parallel-brainstorm to initialize this project and create one independent root idea.
```

```text
Verify brainstorm idea 003. Do not read other idea bodies.
```

```text
Create one child under 003 using its branch brief only.
```

```text
Reconsider early-stop record ES-20260729-01 as one new root because its reopen condition may now
be satisfied.
```

```text
Continue the brainstorm. If the validation threshold is reached, recommend which IDs to verify
instead of silently adding another root.
```

## Status

This is the first working specification. The workflow intentionally favors isolation, auditable
files, bounded exploration, and explicit user control over maximum automation.

## License

MIT
