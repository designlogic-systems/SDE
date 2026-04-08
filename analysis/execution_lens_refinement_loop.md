# Execution Lens Refinement Loop

## Purpose

This file defines the repeatable process used to refine the SDE execution lens using repeated-run evidence.

The loop is designed to reduce reliance on one-off output judgment and instead use structured run data to determine whether the execution lens should be adjusted.

## Core Principle

Execution-lens refinement should be driven by:

- repeated-run evidence
- measurable signals
- inspectable behavior patterns

Refinement should not be driven by:

- single-run preference
- rhetorical fluency
- isolated impressions
- output identity expectations

## Loop Overview

The refinement loop consists of seven stages:

1. select a fixed input and execution lens version
2. run SDE repeatedly
3. capture evidence
4. derive layer metrics
5. identify likely tuning targets
6. adjust the execution lens
7. rerun and compare

---

## Stage 1 — Fix the evaluation conditions

Before running the experiment, hold constant:

- source input
- execution lens version
- SDE workflow version

This ensures the comparison is measuring model behavior rather than uncontrolled setup variation.

---

## Stage 2 — Run SDE repeatedly

Execute SDE multiple times using the same input and same execution lens.

Recommended minimums:
- 5 runs for sanity checking
- 10 runs for early pattern detection
- 20–30 runs for first serious analysis
- 50–100 runs for stronger confidence

The goal is to observe repeated-run behavior, not one-off output quality.

---

## Stage 3 — Capture evidence

Store evidence in the analysis tables:

- `sde_runs`
- `sde_group_presence`
- `sde_questions`

These tables capture:
- run-level metrics
- group-level coverage
- question-level content

This is the evidence base for all later refinement decisions.

---

## Stage 4 — Derive metrics

From the evidence tables, compute metrics into:

- `availability_metrics`
- `direction_metrics`
- `stabilization_metrics`

Then aggregate key metrics into:
- `sde_layer_metrics`

The purpose of this stage is to convert raw evidence into structured layer signals.

---

## Stage 5 — Identify likely tuning targets

At this stage, the goal is not to “judge the output.”
The goal is to identify which layer is the most likely source of instability or weakness.

### Availability candidate signals
Examples:
- high generic question rate
- weak context-anchor usage
- low contextual consistency across runs

### Direction candidate signals
Examples:
- inconsistent group presence
- unstable priority distribution
- question-count variance beyond the intended band

### Stabilization candidate signals
Examples:
- group-count drift
- schema inconsistency
- repeated structural band-width expansion

---

## Stage 6 — Adjust execution lens

Once a likely layer target is identified, make a bounded execution-lens revision.

Adjustment examples:
- Availability: strengthen admitted-context constraints
- Direction: tighten task framing, priority rules, or required semantic coverage
- Stabilization: tighten boundedness constraints and structural expectations

The key principle is:
- adjust one layer deliberately
- do not rewrite everything at once

---

## Stage 7 — Re-run and compare

After adjusting the execution lens:

- run the same input again under the new lens version
- capture evidence into the same tables
- compare results across versions

The comparison should focus on:
- structure
- coverage
- bounded variability
- layer-specific improvement signals

## Interpretation Rule

Improvement does not mean identical output.

Improvement means:
- more stable structure
- more consistent semantic coverage
- more bounded and explainable variability
- reduced evidence of the targeted layer weakness

## Recommended Refinement Posture

Use small, controlled revisions.

Prefer:
- narrow changes
- batch comparison
- evidence-driven iteration

Avoid:
- large untraceable prompt rewrites
- mixing multiple unrelated changes into one revision
- declaring success from one run

## Refinement Output

Each completed refinement cycle should produce:

- a prior lens version
- a revised lens version
- a run batch under each version
- layer metrics for each batch
- a comparison basis for deciding whether the revision helped

## Non-Goals

This loop does not:
- guarantee convergence
- eliminate ambiguity entirely
- replace human oversight
- declare one layer solely responsible from one metric alone

## Notes

The execution-lens refinement loop is currently specific to SDE, but it establishes a reusable pattern for controlled refinement of AI-enabled workflows.