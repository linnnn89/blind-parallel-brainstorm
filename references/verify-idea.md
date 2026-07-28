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
10. Write one append-only review file.
11. Update only the selected row's idea and expansion status in `ROOT_INDEX.md` or the
    appropriate parent `child_indexes/<parent-id>.md`.

Do not modify the original idea front matter to represent current status. The immutable idea
records creation-time state; the index and latest review record current state.

## Verdict rules

### survives

Use when the core proposition remains coherent and worth further testing after counterevidence
and alternatives are considered.

### weakened

Use when an important part fails, but a narrower or repaired form may retain value.

### rejected

Use when the core proposition contradicts established facts, collapses into a simpler existing
explanation, has no differentiating prediction, or cannot be repaired without becoming a new
root idea.

### blocked

Use when a decision depends on inaccessible evidence, missing data, unavailable tooling, or a
real-world experiment.

None of these verdicts means confirmed truth.

## Branch brief generation

Create or update `branch_briefs/<idea-id>.md` only when:

- verdict is `survives` or `weakened`;
- the core proposition can be stated without advocacy;
- unresolved dimensions are concrete;
- further conceptual branching can add information.

The branch brief must contain only:

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
an idea's coherence assessment, but only external evidence may improve evidence support.
