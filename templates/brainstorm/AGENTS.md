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
9. Never create and verify an idea in the same run.
10. One create run produces exactly one idea file.
11. A busted idea keeps its stable path, is displayed as `BUSTED.<id>` in its index, and cannot
    branch under current evidence.
12. When validation thresholds are reached, recommend verification; do not silently continue
    horizontal expansion on a generic request.
13. Prefer vertical development of `survives` or qualified `weakened` nodes once viable roots
    exist.
14. Never write brainstorm content into the main project without explicit user approval naming
    the selected idea.
15. Do not expose private chain-of-thought. Record concise assumptions, mechanisms, predictions,
    falsifiers, evidence, and decisions only.
16. When a requested action violates isolation, stop and report the conflict.
