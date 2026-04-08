# SDE Analysis Data Model

## Purpose

The SDE analysis data model defines how repeated-run evidence, derived metrics, and cross-layer signals are stored for the Structured Discovery Engine (SDE).

Its purpose is to make SDE behavior inspectable, comparable, and refinement-ready.

The data model is organized into:

- evidence tables
- layer-specific metric tables
- combined rollup metrics

## Design Principles

The data model follows these principles:

1. raw evidence is stored separately from derived metrics
2. each metric should have a single source-of-truth table
3. repeated runs are the primary evaluation unit
4. interpretation should be based on inspectable data, not one-off impressions
5. the model should support execution-lens refinement through measurable signals

## Table Categories

### 1. Evidence Tables

These tables store the direct evidence produced by repeated SDE runs.

#### `sde_runs`
One row per SDE run.

Purpose:
- capture run-level summary metrics
- compare repeated runs
- detect aggregate variability

Typical fields:
- `run_id`
- `execution_lens_version`
- `technical_group_count`
- `technical_question_count_total`
- `technical_high_count`
- `technical_medium_count`
- `technical_low_count`
- `technical_ambiguity_flag_count`
- `technical_completeness_note_count`
- `customer_group_count`
- `customer_question_count_total`
- `customer_high_count`
- `customer_ambiguity_flag_count`
- `customer_completeness_note_count`
- delta and compression formula fields

#### `sde_group_presence`
One row per `(run_id, group_name)`.

Purpose:
- track semantic group presence across runs
- detect coverage loss
- support direction and stabilization analysis

Typical fields:
- `run_id`
- `execution_lens_version`
- `group_name`
- `technical_present`
- `customer_present`
- `question_count` (optional)
- presence delta formulas

#### `sde_questions`
One row per question.

Purpose:
- analyze question-level content variance
- support contextuality, genericity, redundancy, and specificity analysis
- provide evidence for Availability metrics

Typical fields:
- `run_id`
- `execution_lens_version`
- `surface_type`
- `group_name`
- `question_id`
- `question_text`
- `priority`
- `has_ambiguity_flag`
- `has_completeness_note`

---

### 2. Layer Metric Tables

These tables store deterministic metrics derived from the evidence tables.

#### `availability_metrics`
Purpose:
- measure how well SDE uses admitted context
- detect generic or weakly grounded question behavior

Derived primarily from:
- `sde_questions`

Example metric types:
- context-anchor usage
- generic question rate
- context-token match rate
- cross-run contextual consistency

#### `direction_metrics`
Purpose:
- measure whether SDE consistently performs the intended task

Derived primarily from:
- `sde_runs`
- `sde_group_presence`
- optionally `sde_questions`

Example metric types:
- question-count variance
- priority-distribution variance
- required-group presence rate
- group-presence stability

#### `stabilization_metrics`
Purpose:
- measure boundedness and structural repeatability

Derived primarily from:
- `sde_runs`
- `sde_group_presence`

Example metric types:
- group-count stability
- total-question band width
- priority band width
- missing-group incidents
- schema consistency rate

---

### 3. Combined Rollup Table

#### `sde_layer_metrics`
Purpose:
- combine key Availability, Direction, and Stabilization metrics into one exportable summary surface
- support cross-layer comparison
- support communication of experiment-level results

Typical fields:
- `experiment_id`
- `execution_lens_version`
- `run_count`
- key Availability metrics
- key Direction metrics
- key Stabilization metrics
- layer-specific tuning candidate flags

## Data Flow Model

The intended data flow is:

1. SDE runs generate technical and customer-facing artifacts
2. evidence is written into:
   - `sde_runs`
   - `sde_group_presence`
   - `sde_questions`
3. derived metrics are computed into:
   - `availability_metrics`
   - `direction_metrics`
   - `stabilization_metrics`
4. combined metrics are written into:
   - `sde_layer_metrics`

## Modeling Rationale

This structure separates:

- what happened
from
- what it means

### Evidence tables answer:
- what did SDE produce?

### Layer metric tables answer:
- what does repeated-run behavior imply about each execution-lens layer?

### Combined metrics table answers:
- what is the overall experiment-level picture?

## Non-Goals

This data model does not:

- treat single-run outputs as authoritative
- collapse all analysis into one table
- rely on subjective narrative as the primary refinement signal
- assume exact output identity is required

## Notes

The SDE analysis data model is product-specific.

It may inform a broader DesignLogic product analysis model later, but the current structure is scoped to SDE and its execution-lens refinement process.