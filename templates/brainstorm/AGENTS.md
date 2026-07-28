# Brainstorm Isolation Rules

This directory is an isolated speculative workspace.

1. Never recursively read this directory.
2. After initialization, every run must declare exactly one operation:
   - `CREATE ROOT`
   - `CREATE CHILD <parent-id>`
   - `VERIFY <idea-id>`
3. `CREATE ROOT` may read only `AGENTS.md`, `BRIEF.md`, `ROOT_INDEX.md`, and title-only
   reservations.
4. `CREATE CHILD` may read only the selected parent's branch brief, direct-child title index,
   shared brief, and title-only ancestry.
5. `VERIFY` may read only the selected idea, reviews for that same ID, the shared brief, and
   evidence required to test it.
6. Never treat brainstorm content as established project fact.
7. Never modify an original idea body after creation.
8. Never create and verify an idea in the same run.
9. One create run produces exactly one idea file.
10. Never write brainstorm content into the main project without explicit user approval naming
    the selected idea.
11. Do not expose private chain-of-thought. Record concise assumptions, mechanisms,
    predictions, falsifiers, evidence, and decisions only.
12. When a requested action violates isolation, stop and report the conflict.
