# SDE Analysis System

## Purpose

The SDE Analysis System is the structured evaluation and refinement layer for the Structured Discovery Engine (SDE).

Its purpose is to measure SDE behavior across repeated runs so execution-lens refinement can be based on inspectable evidence rather than single-run impression.

The analysis system exists to determine whether SDE outputs are:

- structurally consistent
- semantically complete
- bounded in variability
- suitable for controlled execution-lens refinement

## Scope

This analysis system applies specifically to SDE.

It does not define a DesignLogic-wide analysis framework.
It is the first product-specific implementation of a broader product analysis pattern that may later be generalized.

## Problem

LLM-enabled workflows can produce outputs that are:

- structurally stable in some respects
- variable in other respects
- difficult to evaluate correctly from one run alone

Without a formal analysis layer, it is difficult to determine:

- whether variability is acceptable
- whether output behavior is improving
- which parts of the execution lens need refinement
- whether repeated-run behavior is bounded or unstable

## Solution

The SDE Analysis System introduces:

- structured run capture
- group-level coverage tracking
- question-level analysis
- derived layer metrics
- a repeatable execution-lens refinement loop

This makes SDE behavior measurable across repeated runs of the same input.

## Success Model

SDE is not evaluated on exact output identity.

Success is defined as:

- stable structure
- consistent semantic coverage
- bounded variability

### Stable structure
The output should preserve a repeatable structural shell across runs.

For SDE, this includes:
- stable group structure
- stable schema adherence
- controlled question-count range

### Consistent semantic coverage
The output should continue to cover the intended semantic domains across runs, even if phrasing varies.

For SDE, this means:
- expected groups remain present
- important semantic areas do not disappear unpredictably
- output remains aligned to the discovery task

### Bounded variability
Runs may differ, but the differences should remain inspectable and controlled.

Variability is acceptable when it does not cause:
- structural drift
- coverage loss
- unstable priority behavior
- degraded usefulness

## Analysis Architecture

The system is organized into three layers:

### 1. Evidence Tables
These tables store raw or near-raw execution evidence.

- `sde_runs`
- `sde_group_presence`
- `sde_questions`

### 2. Layer Metric Tables
These tables store deterministic derived metrics for execution-lens analysis.

- `availability_metrics`
- `direction_metrics`
- `stabilization_metrics`

### 3. Combined Layer Metrics
This table provides a cross-layer metric rollup.

- `sde_layer_metrics`

## Evidence Model

### `sde_runs`
Stores run-level output metrics.

Purpose:
- compare repeated runs
- track aggregate output behavior
- support early detection of variability

### `sde_group_presence`
Stores group-level presence records.

Purpose:
- measure semantic coverage consistency
- determine which groups appear or disappear across runs

### `sde_questions`
Stores question-level records.

Purpose:
- analyze question content variance
- support availability-level analysis
- support specificity, redundancy, and contextuality analysis

## Layer Metric Model

### Availability
Availability measures whether the model is using admitted context effectively rather than defaulting to generic discovery behavior.

Availability metrics are intended to evaluate:
- contextual specificity
- generic question rate
- context-anchor usage
- cross-run contextual consistency

### Direction
Direction measures whether the model is consistently performing the intended task.

Direction metrics are intended to evaluate:
- group-count stability
- question-count variance
- priority-distribution variance
- required-group presence
- group-presence stability

### Stabilization
Stabilization measures structural boundedness and repeatability.

Stabilization metrics are intended to evaluate:
- schema consistency
- group-count stability
- total-question band width
- priority band width
- missing-group incidents

## Refinement Logic

The SDE Analysis System supports the following loop:

1. run SDE repeatedly with the same input and execution lens
2. capture run-level, group-level, and question-level evidence
3. compute deterministic layer metrics
4. identify layer-specific instability or weakness
5. adjust the execution lens
6. rerun and compare against the prior lens version

Refinement is based on:
- repeated-run behavior
- metric patterns
- inspectable evidence

Refinement is not based on:
- single-run preference
- rhetorical fluency
- isolated impressions

## Current Role in SDE

Within SDE, the analysis system serves four functions:

1. make repeated-run behavior visible
2. distinguish acceptable variability from destabilizing variability
3. identify which execution-lens layer is the likely tuning target
4. provide a documented basis for refinement decisions

## Non-Goals

The SDE Analysis System does not:

- guarantee correctness
- eliminate all variability
- replace human review entirely
- define a universal DesignLogic product analysis framework

## Notes

SDE is the first implemented case of this analysis pattern.

The analysis system should be treated as:
- product-specific
- measurable
- extensible
- compatible with future generalization

But it should not be presented as product-agnostic until additional DesignLogic products implement the same pattern.