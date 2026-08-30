# Blind Parallel Brainstorm

[中文说明](README.zh-CN.md)

A file-isolated agent skill for generating independent ideas, verifying one numbered idea at a
time, removing clearly failed directions, and developing reviewed ideas into controlled branches
such as `001-01` and `001-02`, while archiving coherent candidates stopped before formal creation.
It can also run a bounded, leader-coordinated asynchronous campaign over those same atomic
operations. Its first domain profile is medical and biomedical research, while the core workflow
remains usable for other research and software ideation.

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

After one-time workspace initialization, each worker run performs exactly one primary operation:

```text
CREATE ROOT
VERIFY 001
CREATE CHILD 001
SYNTHESIZE 001
```

A successful create run writes one idea. A bounded failed attempt may append early-stop records
but creates no idea or index rows for those candidates. A verify run reviews one idea. One
explicit user request may authorize a session-scoped campaign containing several independent
worker runs. Returning the final campaign report ends that session and returns control to the
user.

## Leader-coordinated campaigns

In campaign mode, the main agent acts as the research lead: it fixes the objective and stable
success criteria, assigns non-overlapping directions, evaluates accepted verification metadata,
balances the portfolio, and decides whether the target has been met. Workers remain isolated and
perform one bounded atomic operation each under the lead's central scheduling.

Scheduling is event-driven rather than wave-based. When any worker finishes, the lead reviews that
result and can refill the available slot without waiting for every other worker. The active
frontier preserves three kinds of work when they are useful:

- verification of decision-critical claims;
- depth under reviewed viable branches;
- breadth through uncovered roots or sibling lineages.

A CREATE result alone cannot justify concentrated fan-out. A promising branch first needs a
current accepted branchable review (`survives` or qualified `weakened`) and a valid open branch
brief. It may then receive distinct descendants such as `010-01`, `010-02`, and `010-03`, while
work on `011`, `012`, or new roots such as `013` and `014` continues when those directions remain
eligible. The lead freezes new dispatches when the target is met or a real boundary is reached,
drains compliant in-flight work, reports the state, and waits for the user. Synthesis and
promotion remain separate user decisions.

## Development cadence

```text
independent roots
  -> targeted VERIFY
  -> survives / weakened / blocked / busted
  -> balanced breadth + reviewed depth + verification
  -> explicit synthesis and promotion
```

Default validation advice is triggered at 6 unreviewed roots, 3 unreviewed children under one
parent, or 8 active unreviewed ideas in total. The advice is not a hard block: explicit user
instructions still control the next operation.

Once viable roots exist, generic continuation should choose the highest-information next action:
verify an unresolved claim, deepen a reviewed branch, or add a genuinely uncovered root. A
promising lineage receives priority within a balanced frontier, not ownership of the whole
portfolio.

## Medical research profile

For medical and biomedical work, the lead first identifies the question type, then selects only
the decision dimensions relevant to it. Examples include causal validity for etiologic questions,
discrimination and clinical utility for diagnostic or prediction questions, treatment contrast
and safety for interventions, and biological linkage plus translational distance for mechanism
work. Public-health, implementation, secondary-data, omics, and methods questions receive their
own applicable dimensions.

Question structure and evidence standards follow the question type and intended claim. PICO is
used when it clarifies a structured clinical question; other questions use dimensions suited to
their scientific function. Reviews distinguish direct support, indirect support, plausibility,
analogy, and counterevidence; preserve the boundary between association, causation, mechanism,
and clinical recommendation; and record which stable `SC-*` success criteria each idea addresses,
supports, or leaves blocked. The main agent judges whether the campaign as a whole has met the
user's target.

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
  leader-campaign.md
  medical-research-profile.md
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

```text
Run a bounded medical-research campaign on this question. Act as the PI, give each worker one
non-overlapping atomic assignment, refill slots as workers finish, and preserve breadth while
deepening only branches that have an accepted branchable review. Stop dispatching when the agreed
SC-* criteria are met, drain in-flight work, then report for my decision.
```

## Status

This is a working specification. The workflow intentionally favors isolation, auditable files,
bounded asynchronous exploration, balanced depth and breadth, and explicit user control over
automation and promotion.

## License

MIT
