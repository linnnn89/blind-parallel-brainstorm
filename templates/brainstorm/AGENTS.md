---
brainstorm_schema_version: 3
---

# Brainstorm Isolation Rules

This directory is an isolated speculative workspace.

1. Treat this directory as speculative quarantine: never recursively read it or present its
   contents as established project fact.
2. After initialization, each worker run declares exactly one operation:
   - `CREATE ROOT`
   - `CREATE CHILD <parent-id>`
   - `VERIFY <idea-id>`
   - `SYNTHESIZE <parent-id>`
3. `CREATE ROOT` initially reads only `AGENTS.md`, `BRIEF.md`, `ROOT_INDEX.md`, and title-only
   reservations.
4. `CREATE CHILD` initially reads only the selected parent's current branch brief, direct-child
   title index, shared brief, title-only ancestry, and allowed reservation fields.
5. `VERIFY` reads one selected idea, its same-ID review history, the shared brief, its index row,
   and evidence required to test it.
6. CREATE drafts before consulting `BUSTED.md` or `EARLY_STOPS.md`. A successful CREATE writes one
   idea; an `ES-*` early stop receives no idea or index row.
7. Creation and verification remain separate worker operations.
8. Original idea bodies and accepted review bodies are immutable. Review lifecycle metadata may
   advance `draft -> accepted -> superseded` while preserving review history.
9. Only the current accepted same-ID review publishes evidence state. Before `CREATE CHILD`, its
   source, revision, state, required metadata, gate, and checkpoint must match the branch brief;
   stale or invalid state blocks creation.
10. Immature evidence, uncertain novelty, or a small evidence pool requires explicit user
    confirmation naming the parent and warning.
11. Early stops remain separate from busted verdicts and evidence state. Only unique, complete,
    source-checked, unresolved records may warn or filter.
12. A busted idea keeps its stable path, is displayed as `BUSTED.<id>`, closes expansion, and
    remains traceable to its accepted review.
13. Validation thresholds create a verification advisory. Generic continuation selects the legal
    operation with the largest information value across verification, reviewed depth, and
    genuinely uncovered breadth.
14. Promotion to the main project requires explicit user approval naming the selected idea.
15. Persist concise assumptions, mechanisms, predictions, falsifiers, evidence, and decisions.
16. An isolation or scope violation stops the operation. Concurrent workers are terminated only
    for observable protocol violations; weak or unconventional hypotheses proceed to review.
17. Preserve incomplete reviews as `draft`. Repair partial commits deterministically while
    preserving accepted evidence and avoiding invented content.
18. Check the schema marker and managed-path existence before every operation. Migration creates
    required paths first and writes the schema marker last.
19. Workers return early-stop findings; the coordinator validates them, assigns IDs, and appends
    complete records serially. Reconsideration adds a resolution event while preserving the
    original record.
20. In a campaign, the main agent owns dispatch, portfolio balance, final evaluation, and
    reporting. Each worker receives one non-overlapping contribution and only its own dispatch
    details; other active reservations remain title-only.
21. Planned fan-out requires a current accepted branchable review and valid open brief. A
    promising lineage receives depth while eligible sibling lineages and uncovered roots retain
    capacity.
22. When the campaign target or boundary is reached, freeze new dispatches, drain compliant
    operations, report, and return control. Synthesis and promotion remain separately authorized.
