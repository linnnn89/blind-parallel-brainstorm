# VERIFY Manual

Read this file only for `VERIFY <idea-id>`.

## Allowed reads

- `brainstorm/AGENTS.md`
- `brainstorm/BRIEF.md`
- `brainstorm/ideas/<idea-id>.md`
- existing reviews for the same ID
- the title-only index row that owns the selected ID
- project files or external sources needed to test this idea

Do not read sibling or cousin idea bodies, unrelated reviews, or unrelated branch briefs.
Read `BUSTED.md` only after reaching a provisional verdict, and only when the verdict may be
`busted` or when checking whether the same failure is already recorded.

## Review sequence

1. Confirm that the requested ID exists.
2. Read the idea neutrally and separate its core proposition from persuasive wording.
3. Identify required assumptions and logical dependencies.
4. Check compatibility with confirmed facts in the brief.
5. Seek evidence that supports the idea.
6. Deliberately seek counterevidence and simpler explanations.
7. Derive at least one prediction that differs from the baseline explanation.
8. State a result that would weaken or falsify the idea.
9. Recommend the lowest-cost, highest-information next test.
10. Assign one provisional verdict.
11. Write one append-only review file.
12. Update only the selected row's label, idea status, and expansion status in `ROOT_INDEX.md` or
    the appropriate parent `child_indexes/<parent-id>.md`.
13. If the verdict is `busted`, append one compact failure record to `BUSTED.md`.

Do not modify the original idea front matter. The immutable idea records creation-time state;
the index and latest review record current state.

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

- verdict is `survives` or `weakened`;
- the core proposition can be stated without advocacy;
- unresolved dimensions are concrete;
- further conceptual branching can add information.

The branch brief contains only:

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

Do not reward confidence, eloquence, length, or novelty claims. Internal consistency may improve
coherence assessment, but only external evidence may improve evidence support.
