# Leader-Coordinated Campaign

Read this file only when the user explicitly requests asynchronous or multi-agent exploration,
asks the agent to continue until a stated target is reached, or assigns the main agent a research
lead or project-leader role.

## Campaign boundary

A campaign is a session-scoped orchestration layer over the four existing primary operations.
It preserves the one-operation worker boundary, and each worker invocation performs exactly one
of:

- `CREATE ROOT`;
- `VERIFY <idea-id>`;
- `CREATE CHILD <parent-id>`;
- `SYNTHESIZE <parent-id>`, only when synthesis is explicitly authorized.

Before dispatching, the leader fixes or confirms:

- the campaign objective;
- stable success-criterion IDs from `BRIEF.md`;
- exclusions and facts that workers may not redefine;
- evidence, permission, time, cost, and tool boundaries;
- the condition for stopping new dispatches.

If a missing choice would materially change the research objective, evidence boundary, or
resource use, ask the user before dispatch. Begin a campaign only after its objective and stopping
condition are bounded.

Campaign scheduling is session-local. Returning the final report ends the campaign until the user
invokes it again.

## Roles

### Main agent: research lead

The main agent:

- protects the user-approved objective and success criteria;
- assigns non-overlapping work;
- maintains breadth, verification, and promising-branch depth as a portfolio;
- evaluates current accepted review metadata and valid branch briefs;
- refills an available slot when any worker finishes;
- decides whether the campaign target has been reached;
- freezes, drains, and reports.

Accepted reviews remain the source of evidence state, and promotion still requires the user's
approval. The leader may use current accepted review front matter for routing; formal comparison
of idea bodies remains a separately authorized synthesis.

### Worker: isolated contributor

Each worker receives one bounded dispatch and performs one primary operation. A worker:

- follows the operation-specific allowed-read boundary;
- receives only its own dispatch details and the title-only context allowed by its operation;
- leaves recruitment, scheduling, and cross-worker coordination to the leader;
- returns the normal atomic-operation output to the leader;
- stops after committing or safely failing that operation.

Logical descendants can reach the configured depth even though their worker runs remain centrally
dispatched.

## Dispatch envelope

Give each worker only the minimum information needed for its operation:

```yaml
operation: CREATE_ROOT|VERIFY|CREATE_CHILD|SYNTHESIZE
target_id: null
parent_id: null
lineage_id: new|NNN
primary_direction: concise non-overlapping contribution
success_criterion: SC-NN|null
overlap_exclusion: concise boundary against active assignments
stop_condition: operation-specific completion or blocker
```

The envelope is a scope contract rather than a preferred conclusion. `primary_direction` may
identify a mechanism, boundary, population, test, implementation, alternative explanation, or
another domain-appropriate axis while leaving the conclusion open to the worker.

For concurrent CREATE operations, the leader writes the same concise direction fields into that
worker's reservation. Other workers may see only the reservation title as allowed by their
operation manual, not its direction fields.

Every active dispatch needs a distinct combination of lineage, operation, and primary
contribution. Concurrent VERIFY runs also target different idea IDs.

## Event-driven scheduling

Fill available capacity with eligible, non-overlapping atomic operations, then respond to the
first completion event:

1. inspect the operation result and current lifecycle metadata;
2. update the in-memory portfolio view;
3. test the campaign success and stop conditions;
4. if dispatch remains authorized, fill the newly available slot immediately;
5. leave other compliant workers running.

Schedule the next eligible operation as soon as capacity opens, without waiting for a complete
wave. Wait on completion or attention events rather than repeatedly polling unchanged work.

## Balanced frontier

Treat the active forest as a research portfolio, not a depth-first tree. Consider three kinds of
work whenever they are legal and relevant to an unmet success criterion:

- **verification**: test unreviewed or stale nodes and reduce speculative debt;
- **depth**: create distinct descendants of reviewed viable nodes;
- **breadth**: maintain other lineages or open a genuinely uncovered root direction.

Apply these invariants:

1. A CREATE result alone is not a high-potential signal. A lineage becomes eligible for planned
   vertical expansion only through a current accepted review and valid open branch brief.
2. Several descendants of one promising parent may run concurrently only when their primary
   contributions are distinct.
3. When capacity is at least two and an eligible task exists outside the leading lineage, keep at
   least one active or next-dispatch position outside that lineage. Roughly half of active
   generation capacity is the default upper share for one lineage; adjust to actual capacity and
   remain work-conserving when no alternative task is legal.
4. Validation thresholds are backlog controls, not permission for verification from one lineage
   to consume every protected breadth position. Stop adding children to a node whose configured
   unreviewed-child advisory is already reached until that debt is reduced or the user explicitly
   overrides it.
5. Prefer an eligible direction that has been least recently served when information gain and
   lifecycle readiness are otherwise comparable. This fairness state is session-local and needs
   no persistent queue ledger.
6. A promising lineage receives priority within its protected share while live sibling roots and
   uncovered success criteria remain represented in the portfolio.

If capacity is one, alternate among the highest-information legal operations over successive
completions. If no legal breadth or sibling task exists, allow the leading lineage to use idle
capacity rather than reserving an empty slot.

### Example

After accepted verification makes root `010` viable, the leader may assign distinct descendants
such as a mechanism, a boundary condition, and a discriminating test while continuing work on
`011`, `012`, and uncovered roots `013` or `014`. The exact number running at once depends on
available capacity. Protected directions remain eligible when queued; they are not discarded
because `010` is currently strongest.

## Success evaluation

Only the main agent evaluates campaign completion. Use:

- the stable criteria in `BRIEF.md`;
- current accepted review front matter, including criterion coverage when present;
- current idea, evidence, gate, and expansion states;
- explicit blockers and remaining uncertainty.

A review may state that one idea supports, addresses, or blocks a criterion. It does not declare
the campaign globally complete. The leader must judge the portfolio against the user's stated
target without reading unrelated bodies merely to obtain a preference ranking.

Synthesis and promotion remain separately authorized after the target appears met.

## Freeze, drain, and report

Stop issuing new work when:

- the user-approved success criteria are clearly met;
- further candidates add no meaningful mechanism, prediction, test, boundary, implementation,
  repair, or coverage of an unmet criterion;
- the next useful step requires user judgment, inaccessible evidence, new tools, more resources,
  or expanded permission;
- an agreed resource boundary is reached;
- the user stops the campaign.

Then:

1. **Freeze** new dispatches immediately.
2. **Drain** already running, compliant single-operation workers normally.
3. Interrupt only for the existing protocol-violation or stalled-operation rules, not merely
   because the campaign has reached its target.
4. Repair any partial commits using the existing deterministic rules.
5. Report criterion status, completed operations, high-potential IDs and states, breadth and depth
   coverage, blockers, uncertainty, and the next user decision.

If a boundary or blocker is reached before success, state that the target remains unmet and report
bounded progress as partial. All campaign work is drained or otherwise resolved before the final
report returns control.

## Schema compatibility

Campaign coordination adds no managed workspace path and does not change schema `3`. Stable
facts and success criteria remain in `BRIEF.md`; ideas, accepted reviews, indexes, and
reservations remain the workspace state sources. Session scheduling order is transient, so a
resumed campaign rebuilds structural readiness from allowed metadata and begins a new fairness
window.
