# SDE Experiment Design

## Purpose

This file defines how repeated-run experiments are structured for SDE.

The purpose of the experiment design is to ensure that execution-lens refinement is based on controlled repeated-run evidence rather than uncontrolled or mixed conditions.

## Experiment Unit

An SDE experiment is defined as:

- one fixed source input
- one fixed execution lens version
- multiple repeated runs
- one resulting analysis batch

This means the primary comparison unit is not a single run.
It is a batch of repeated runs under stable conditions.

## Controlled Variables

The following should remain fixed within a single experiment batch:

- source input
- SDE workflow version
- execution lens version
- active output schema expectations

These controls are necessary so observed variation can be attributed to repeated model behavior rather than setup drift.

## Observed Variables

The experiment is intended to observe variation in:

- group structure
- question count
- priority distribution
- ambiguity signaling
- completeness signaling
- group presence
- question content

These observed variables are captured through the analysis tables.

## Minimum Batch Sizes

Recommended usage:

- **5 runs** → early sanity check
- **10 runs** → first usable pattern detection
- **20–30 runs** → first serious layer analysis
- **50–100 runs** → stronger evidence for refinement conclusions

Small batches are useful for detecting obvious instability.
Larger batches are better for tuning decisions.

## Success Model

The experiment is not trying to prove exact output identity.

Success is defined by:

- stable structure
- consistent semantic coverage
- bounded variability

### Stable structure
The structural shell should remain consistent across repeated runs.

### Consistent semantic coverage
Expected semantic areas should remain present across repeated runs.

### Bounded variability
Variation in counts, priorities, and content should remain explainable and controlled.

## Batch Comparison Model

Experiments should be compared in one of two ways:

### 1. Within-version analysis
Compare repeated runs under a single execution-lens version.

Purpose:
- measure current behavior
- detect instability
- establish a baseline

### 2. Cross-version analysis
Compare run batches across two execution-lens versions.

Purpose:
- determine whether a lens revision improved behavior
- identify which layer signals changed

## Evidence Capture

Each experiment batch should write evidence into:

- `sde_runs`
- `sde_group_presence`
- `sde_questions`

Derived metrics should then be written into:

- `availability_metrics`
- `direction_metrics`
- `stabilization_metrics`
- `sde_layer_metrics`

## Recommended Experiment Sequence

1. choose the evaluation input
2. fix the execution-lens version
3. run SDE repeatedly
4. capture all evidence
5. compute all derived metrics
6. inspect the batch-level signals
7. determine whether refinement is needed
8. revise the lens if warranted
9. repeat the same experiment under the revised version

## Experiment Boundaries

An experiment should not:

- mix multiple different inputs without clear labeling
- mix multiple execution-lens versions in one batch
- treat one output as representative of the batch
- interpret variability without checking batch context

## Experiment Output

A completed experiment should produce:

- a traceable batch of runs
- evidence tables populated
- layer-specific metrics populated
- a basis for deciding whether to keep, revise, or compare an execution lens version

## Non-Goals

This experiment design does not:

- claim statistical completeness
- guarantee universal conclusions from one input
- eliminate the need for inspection when metrics conflict
- require zero variability as a target

## Notes

This design is intentionally lightweight enough to be implemented inside SDE’s current evaluation system while still being structured enough to support serious repeated-run analysis.