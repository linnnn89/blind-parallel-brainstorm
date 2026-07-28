# Synthesis and Promotion Manual

Read this manual only when the user explicitly requests convergence, comparison, or promotion.

## Purpose

Blind generation and validation intentionally avoid cross-contamination. A separate synthesis phase is required before combining surviving branches.

## Allowed operation

`SYNTHESIZE <parent-id>`

This is not CREATE and not VERIFY.

## Allowed reads

- BRIEF.md
- ROOT_INDEX.md
- the selected parent branch brief
- direct child indexes
- reviews of selected surviving or weakened nodes

Do not read rejected branches unless the user explicitly requests failure analysis.

## Synthesis goals

The synthesizer may:

- identify complementary surviving branches;
- identify genuine conflicts;
- propose combinations;
- identify the highest-information next test;
- recommend promotion candidates.

It must not:

- rewrite history of the original ideas;
- treat agreement between branches as proof;
- promote speculation into facts.

## Promotion gate

A branch may enter the main project only after:

1. user explicitly selects the ID;
2. review history is available;
3. uncertainty and limitations remain visible;
4. promoted text is labeled as hypothesis, proposal, or validated conclusion according to evidence level.
