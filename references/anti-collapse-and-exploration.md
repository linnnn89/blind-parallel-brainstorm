# Anti-collapse and Exploration Guidance

## Problem

Long-running brainstorming systems tend to converge too early toward the first plausible explanation.

## Rules

During CREATE operations:

- preserve independent generation;
- do not rank ideas before generation is complete;
- do not merge merely because wording is similar;
- distinguish semantic similarity from mechanism similarity.

## Tail exploration operators

When explicitly requested, generate candidates using different operators:

- reverse causality;
- remove a default assumption;
- change time scale;
- change unit of analysis;
- introduce hidden variables;
- introduce feedback loops;
- transfer structures from distant fields;
- treat anomalies as central clues.

## Diversity check

A candidate is not meaningfully different if it only changes:

- terminology;
- examples;
- surface explanation;
- variable names.

Prefer differences in:

- causal structure;
- assumptions;
- predictions;
- validation methods.

## Stopping exploration

Do not continue branching because more branches are possible. Stop or freeze a branch when additional children no longer add new mechanisms, predictions, tests, or boundary conditions.
