---
idea_id: "NNN"
review_id: "001"
review_status: draft|accepted|superseded
supersedes_review: null
superseded_by: null
verdict: survives|weakened|blocked|busted
reviewed_at: YYYY-MM-DD
review_scope: internal|evidence|implementation|mixed
previous_evidence_state: speculative|screened|verified|synthesis_ready|protocol_ready
evidence_state: speculative|screened|verified|synthesis_ready|protocol_ready
evidence_revision: 1
confidence: low|medium|high
last_verified: YYYY-MM-DD|null
gate_decision: continue|freeze
blocking_issue: null
reopen_condition: null
---

# Review A — source-first assessment

## Neutral restatement

[Restate the idea without strengthening its claims.]

## Internal coherence

[Assess assumptions, dependencies, causal or implementation logic, and contradictions.]

## Relationship to confirmed facts

### Supporting evidence

- [Evidence or fact, with source reference when available.]

### Counterevidence

- [Evidence or fact that weakens the idea.]

### Unknown or untested

- [Claims not resolved by available evidence.]

## Simpler alternative explanations

- [Alternative explanation or implementation that could produce the same result.]

## Differentiating predictions

- [Observable result that separates this idea from the baseline or alternatives.]

## Falsification or failure conditions

- [Result that would clearly weaken or bust the idea.]

## Provisional evidence checkpoint

Complete before reading prior review bodies. Include only branch-inheritable claims.

| Claim key | Current value | Confidence | Source |
|---|---|---|---|
| [stable_key] | [concise value] | low|medium|high | [source or unresolved] |

## Provisional evidence gate

| Dimension | Result | Basis |
|---|---|---|
| Quantity | pass|concern|fail|unknown | [One line.] |
| Quality | pass|concern|fail|unknown | [One line.] |
| Novelty | pass|concern|fail|unknown | [One line.] |
| Feasibility | pass|concern|fail|unknown | [One line.] |
| Blockers | pass|concern|fail|unknown | [One line.] |

# Review B — prior-review challenge

[Compare prior same-ID reviews. Record disagreements, unsupported inheritance, changed evidence,
and only necessary follow-up checks.]

# Adjudication

- Retained claims: [What remains supported?]
- Corrected claims: [What changed from prior reviews?]
- Unresolved claims: [What remains uncertain?]
- Transition check: [Valid one-step upgrade, refresh, or evidence-driven downgrade.]

# Highest-information next test

[Recommend one concrete next action, including required data or tooling.]

# Verdict

- Decision: `survives|weakened|blocked|busted`
- Reason: [Concise reason.]
- Expansion recommendation: `open|closed|frozen|saturated`
- Remaining uncertainty: [What is still unresolved?]
- Branch brief action: `create|replace|freeze|none`

## Busted ledger metadata

Complete this section only when the verdict is `busted`.

- Failure class: `contradicts-facts|duplicate|no-new-information|non-falsifiable|unsupported-causal-leap|scope-violation|implementation-impossible`
- Collision signatures:
  - [Short structural signature.]
- Scope: `global|root:NNN|parent:NNN-01`

---

Only an accepted review with valid transition and gate metadata may update current state.
`survives` means worth retaining, not confirmed truth. `BUSTED.md` receives only compact metadata.
