# Synthesis and Promotion Manual

Read this manual only when the user explicitly requests convergence, comparison, or promotion.

## Purpose

Blind generation and single-target verification intentionally avoid cross-contamination. A
separate synthesis phase combines only selected reviewed branches.

## Allowed operation

`SYNTHESIZE <parent-id>`

This is not CREATE and not VERIFY.

Selected nodes must have a current accepted review and evidence state `verified`. Otherwise stop
and route the node through the missing one-step verification transition first.

## Allowed reads

- `BRIEF.md`
- the relevant title-only indexes
- the selected parent branch brief
- selected idea files with status `survives` or qualified `weakened`
- current accepted reviews belonging to those selected ideas

Do not read busted branches unless the user explicitly requests failure analysis. Do not read the
entire forest merely because synthesis is authorized.

## Synthesis goals

The synthesizer may:

- identify complementary surviving branches;
- identify genuine conflicts;
- propose combinations without erasing provenance;
- identify the highest-information next test;
- recommend promotion candidates.

It must not:

- rewrite the history of original ideas;
- treat agreement between branches as proof;
- revive a busted idea without explaining why its failure signature no longer applies;
- promote speculation into facts.

## Evidence-state boundary

Synthesis may satisfy part of the `verified -> synthesis_ready` minimum conditions, but the
synthesis artifact is not an evidence-state source. Only a later accepted review may publish that
one-step transition. User approval likewise does not directly set `protocol_ready`; an accepted
review must record that the transition conditions are met.

## Promotion gate

A branch may enter the main project only after:

1. the user explicitly selects the ID;
2. a current accepted review is available;
3. current status is `survives` or explicitly qualified `weakened`;
4. evidence state is `synthesis_ready` or `protocol_ready`;
5. uncertainty and limitations remain visible;
6. promoted text is labeled as hypothesis, proposal, or validated conclusion according to the
   evidence level.
