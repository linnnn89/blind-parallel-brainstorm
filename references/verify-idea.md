# VERIFY Manual

Read this file only for `VERIFY <idea-id>`.

## Allowed reads

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- `brainstorm/ideas/<idea-id>.md`
- the title-only index row that owns the selected ID
- project files or external sources needed to test this idea

Before the source-first assessment, inspect same-ID review filenames and front matter only to
resolve the current accepted review and evidence state. Do not read prior review bodies until the
Review A checkpoint has been recorded in the new draft.

After Review A, read prior same-ID review bodies for a bounded challenge pass. Do not read sibling
or cousin idea bodies, unrelated reviews, or unrelated branch briefs.
Read `BUSTED.md` only after reaching a provisional verdict, and only when the verdict may be
`busted` or when checking whether the same failure is already recorded.

## Review sequence

1. Confirm that the requested ID exists.
2. Resolve the current accepted review from same-ID review front matter. Ignore drafts and
   superseded reviews as state sources.
3. Create the next review as `draft`; it cannot update any current-state artifact.
4. Review A, source-first:
   - restate the idea neutrally;
   - identify assumptions and logical dependencies;
   - seek supporting evidence, counterevidence, and simpler explanations;
   - complete a compact evidence checkpoint and provisional gate assessment;
   - record a provisional verdict without reading prior review bodies.
5. Review B, challenge pass:
   - read prior same-ID reviews;
   - inspect disagreements, unsupported inherited claims, and changed evidence;
   - run only necessary follow-up checks.
6. Adjudicate retained, corrected, and unresolved claims. Select a one-step upgrade, same-state
   refresh, or evidence-driven downgrade.
7. Complete and validate all transition, provenance, confidence, gate, blocker, and reopen
   metadata.
8. If valid, accept the new review, link it to the previous accepted review, and mark the previous
   review `superseded` by changing lifecycle metadata only.
9. Update the selected index row. For a viable branch, regenerate the whole brief from the
   accepted review and compare source, revision, state, gate, and evidence checkpoint.
10. For `busted`, append one compact failure record to `BUSTED.md`.

Do not modify the original idea front matter. The immutable idea records creation-time state;
the index records lifecycle display state and the current accepted review records evidence state.

If interrupted before acceptance, leave the new review as `draft`; it has no state effect. If
state artifacts do not agree after acceptance, report a hard validation block and do not permit
branching.

## Verdict rules

### survives

Use when the core proposition remains coherent and worth further testing after counterevidence
and alternatives are considered.

Default expansion recommendation: `open` when meaningful unresolved dimensions remain,
otherwise `saturated`.

### weakened

Use when an important part fails, but a narrower, repaired, or better-bounded form may retain
value.

Default expansion recommendation: `open` only for repair or scope-narrowing branches;
otherwise `frozen`.

### busted

Use when the core proposition:

- contradicts established facts;
- duplicates an existing mechanism and prediction without new information;
- has no falsifiable or differentiating consequence;
- relies on an unsupported causal leap that cannot be repaired in place;
- violates the locked scope;
- or is infeasible under non-negotiable implementation constraints.

A busted idea is displayed as `BUSTED.<idea-id>` in its owning index, retains the stable path
`ideas/<idea-id>.md`, and receives expansion status `closed`.

Append a compact entry to `BUSTED.md` containing:

- stable ID and title;
- one failure class;
- one-sentence reason;
- 1-4 short collision signatures;
- scope: `global`, `root:<root-id>`, or `parent:<parent-id>`.

Do not copy the full review narrative into the ledger.

### blocked

Use when a decision depends on inaccessible evidence, missing data, unavailable tooling, or a
real-world experiment.

Default expansion recommendation: `frozen`.

None of these verdicts means confirmed truth.

## Branch brief generation

Create or update `branch_briefs/<idea-id>.md` only when:

- the new review is `accepted`;
- verdict is `survives` or `weakened`;
- the core proposition can be stated without advocacy;
- unresolved dimensions are concrete;
- further conceptual branching can add information.

Replace the whole branch brief from the accepted review. It contains only:

- source review path and evidence revision;
- current evidence state, confidence, verification date, gate decision, and blocker;
- the accepted review's compact evidence checkpoint;
- neutral core proposition;
- inherited assumptions allowed for child work;
- known weaknesses;
- open expansion questions;
- non-negotiable boundaries;
- allowed expansion axes;
- current expansion status.

Do not copy the full idea or review narrative.

If expansion opens for the first time, create `child_indexes/<idea-id>.md` from the child-index
template. If the verdict closes or freezes expansion, reflect that state in the owning title-only
index.

## Review independence

Review A and Review B are sequential passes by one agent, not independent reviewers. This reduces
anchoring but does not establish blindness. Do not claim multi-agent or independent replication.

Do not reward confidence, eloquence, length, or novelty claims. Internal consistency may improve
coherence assessment, but only external evidence may improve evidence support.
