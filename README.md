# Blind Parallel Brainstorm

[中文说明](README.zh-CN.md)

A file-isolated agent skill for generating independent ideas, verifying one numbered idea at a
time, and developing reviewed directions into controlled branches such as `001-01` and
`001-02`.

## Why

Ordinary multi-round brainstorming often collapses toward the first plausible ideas because
later generations read and imitate earlier reasoning. This skill reduces that anchoring through
strict context boundaries:

- root creation sees only a shared brief and title-only root index;
- verification reads one selected idea and its own review history;
- child creation reads a reviewed branch brief instead of the parent's raw draft;
- sibling idea bodies remain hidden;
- brainstorm content stays outside the main project until explicit promotion.

Isolation improves independence. It does not prove novelty or correctness.

## Operations

After one-time workspace initialization, a run performs exactly one primary operation:

```text
CREATE ROOT
VERIFY 001
CREATE CHILD 001
```

A create run writes one idea. A verify run reviews one idea. The skill does not continue in the
background and does not automatically expand uncertainty into brainstorming.

## Development model

```text
001 root idea
  -> VERIFY 001
  -> branch brief
  -> 001-01 / 001-02
  -> verify children independently
  -> deeper branches only when reviewed and still informative
```

Root ideas form an isolated forest first. Cross-branch synthesis happens only when the user
explicitly selects reviewed nodes for comparison.

## Repository structure

```text
SKILL.md
references/
  workspace-and-isolation.md
  create-root.md
  verify-idea.md
  create-child.md
  lifecycle-and-governance.md
templates/brainstorm/
  AGENTS.md
  BRIEF.md
  ROOT_INDEX.md
  idea.md
  review.md
  branch-brief.md
  child-index.md
  reservation.md
```

The root skill uses lazy manual loading: an agent reads only the reference required for the
current operation.

## Core safety properties

- No recursive brainstorm-directory reads.
- No sibling-body reads during creation or verification.
- Original ideas are immutable; reviews are append-only.
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

## Status

This is the first working specification. The workflow is intentionally conservative: strong
isolation and auditable files take priority over maximum automation.

## License

MIT
