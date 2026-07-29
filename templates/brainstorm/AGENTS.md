---
brainstorm_schema_version: 2
---

# Brainstorm Isolation Rules

This directory is an isolated speculative workspace.

1. Never recursively read this directory.
2. After initialization, every run must declare exactly one operation:
   - `CREATE ROOT`
   - `CREATE CHILD <parent-id>`
   - `VERIFY <idea-id>`
   - `SYNTHESIZE <parent-id>`
3. `CREATE ROOT` may initially read only `AGENTS.md`, `BRIEF.md`, `ROOT_INDEX.md`, and
   title-only reservations.
4. `CREATE CHILD` may initially read only the selected parent's branch brief, direct-child title
   index, shared brief, title-only ancestry, and reservations.
5. CREATE operations must draft before reading `BUSTED.md`; the ledger is used only for a
   post-draft collision check.
6. `VERIFY` may read only the selected idea, reviews for that same ID, the shared brief, its index
   row, and evidence required to test it.
7. Never treat brainstorm content as established project fact.
8. Never modify an original idea body after creation.
9. Only the current accepted same-ID review may publish evidence state. Draft and superseded
   reviews are history.
10. Accepted review bodies are immutable. Only lifecycle metadata may move
    `draft -> accepted -> superseded`.
11. Before `CREATE CHILD`, compare the branch brief with the current accepted review's source,
    evidence revision, state, required metadata, and compact evidence checkpoint.
12. Stale state, source mismatch, invalid transition, or missing metadata is a hard block.
13. Immature evidence, uncertain novelty, or a small evidence pool requires explicit user
    confirmation naming the parent and warnings.
14. Never create and verify an idea in the same run.
15. One create run produces exactly one idea file.
16. A busted idea keeps its stable path, is displayed as `BUSTED.<id>` in its index, and cannot
    branch under current evidence.
17. When validation thresholds are reached, recommend verification; do not silently continue
    horizontal expansion on a generic request.
18. Prefer vertical development of `survives` or qualified `weakened` nodes once viable roots
    exist.
19. Never write brainstorm content into the main project without explicit user approval naming
    the selected idea.
20. Do not expose private chain-of-thought. Record concise assumptions, mechanisms, predictions,
    falsifiers, evidence, and decisions only.
21. When a requested action violates isolation, stop and report the conflict.
22. A concurrent worker may be terminated for a clear scope or protocol violation, not merely for
    a weak or unconventional hypothesis. Preserve incomplete reviews as `draft`; if create or
    accepted-review artifacts are partially published, use the deterministic repair rules and
    never demote accepted evidence or guess missing content.
