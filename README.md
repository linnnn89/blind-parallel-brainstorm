# Blind Parallel Brainstorm

[中文说明](README.zh-CN.md)

A file-isolated agent skill for generating independent ideas, verifying one numbered idea at a
time, removing clearly failed directions, and developing reviewed ideas into controlled branches
such as `001-01` and `001-02`.

## Why

Ordinary multi-round brainstorming often collapses toward the first plausible ideas because later
generations read and imitate earlier reasoning. This skill reduces that anchoring through strict
context boundaries:

- root creation sees only a shared brief and title-only root index;
- verification reads one selected idea and its own review history;
- child creation reads a reviewed branch brief instead of the parent's raw draft;
- sibling idea bodies remain hidden;
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

A create run writes one idea. A verify run reviews one idea. The skill does not continue in the
background and does not automatically expand uncertainty into brainstorming.

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
  ROOT_INDEX.md
  BUSTED.md
  idea.md
  review.md
  branch-brief.md
  child-index.md
  reservation.md
```

The root skill uses lazy manual loading: an agent reads only the reference required for the current
operation.

## Core safety properties

- No recursive brainstorm-directory reads.
- No sibling-body reads during creation or verification.
- Original ideas are immutable; reviews and busted records are append-only.
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
Continue the brainstorm. If the validation threshold is reached, recommend which IDs to verify
instead of silently adding another root.
```

## Status

This is the first working specification. The workflow intentionally favors isolation, auditable
files, bounded exploration, and explicit user control over maximum automation.

## License

MIT
