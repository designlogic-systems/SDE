# SDE Metrics Framework

## Purpose

This framework defines how SDE behavior is evaluated through deterministic metrics.

The purpose of the metrics framework is to support execution-lens refinement by measuring repeated-run behavior across three execution layers:

- Availability
- Direction
- Stabilization

The framework does not assume exact output identity.
It assumes repeated-run behavior should be:

- structurally stable
- semantically consistent
- bounded in variability

## Measurement Philosophy

The metrics framework is based on these principles:

1. repeated-run behavior matters more than single-run impression
2. variability is not automatically a failure
3. acceptable variability must remain bounded and inspectable
4. metrics should support layer-specific refinement decisions
5. metrics should be grounded in evidence tables rather than informal preference

---

## Availability Metrics

### Purpose
Availability metrics evaluate whether the model is using admitted context effectively rather than defaulting to generic discovery behavior.

### What Availability is trying to measure
- contextual specificity
- use of input-conditioned terms
- resistance to generic template behavior
- consistency of contextual grounding across runs

### Example metric set
- `availability_context_token_match_rate`
- `availability_generic_question_rate`
- `availability_unique_context_anchor_count`
- `availability_cross_run_context_consistency`

### Evidence source
Primarily:
- `sde_questions`

### Interpretation
Strong Availability behavior means:
- questions reflect the actual input context
- questions are not overly generic
- contextual anchors persist across runs
- the system does not collapse into generic discovery phrasing

Weak Availability behavior means:
- input-specific details are underused
- question sets resemble generic templates
- contextual signals appear inconsistently across repeated runs

---

## Direction Metrics

### Purpose
Direction metrics evaluate whether SDE is consistently performing the intended task.

### What Direction is trying to measure
- task adherence
- semantic coverage consistency
- consistent prioritization behavior
- consistency in how the question set is shaped

### Example metric set
- `direction_group_count_variance`
- `direction_question_count_variance`
- `direction_priority_distribution_variance`
- `direction_required_group_presence_rate`
- `direction_group_presence_stability`

### Evidence source
Primarily:
- `sde_runs`
- `sde_group_presence`

Optionally:
- `sde_questions`

### Interpretation
Strong Direction behavior means:
- expected groups remain present
- question count stays within a controlled range
- priority distribution is reasonably stable
- outputs remain aligned to the intended discovery task

Weak Direction behavior means:
- required semantic groups disappear
- question count varies too widely
- priority labeling shifts unpredictably
- the model appears to interpret task scope differently across runs

---

## Stabilization Metrics

### Purpose
Stabilization metrics evaluate structural boundedness and repeatability.

### What Stabilization is trying to measure
- schema consistency
- structural shell stability
- bounded variation in output size
- bounded variation in priority composition

### Example metric set
- `stabilization_group_count_stability`
- `stabilization_total_question_band_width`
- `stabilization_priority_band_width`
- `stabilization_missing_group_incidents`
- `stabilization_schema_consistency_rate`

### Evidence source
Primarily:
- `sde_runs`
- `sde_group_presence`

### Interpretation
Strong Stabilization behavior means:
- output structure remains fixed
- schema remains consistent
- variation remains bounded
- no structural collapse or drift is observed

Weak Stabilization behavior means:
- output shape changes unexpectedly
- variability becomes difficult to explain
- semantic groups disappear unpredictably
- schema adherence degrades

---

## Metric Ownership

Each metric should be computed in one place first.

Recommended ownership:

- Availability metrics → `availability_metrics`
- Direction metrics → `direction_metrics`
- Stabilization metrics → `stabilization_metrics`

The combined table `sde_layer_metrics` should aggregate or expose those metrics, not become the original computation surface.

## Tuning Signal Philosophy

Metrics are not used to prove correctness.
They are used to identify likely tuning targets.

Examples:

- persistent group loss suggests a Direction issue
- wide question-count band width suggests a Stabilization issue
- high generic question rate suggests an Availability issue

Metrics are signals for refinement, not authority substitutes for human judgment.

## Non-Goals

This framework does not:

- define final thresholds for all future products
- claim that one metric fully determines one layer
- eliminate the need for inspection when contradictory signals appear
- require zero variability

## Notes

The Availability / Direction / Stabilization framing is specific to the current SDE execution-lens model.

This framework is intended to make refinement inspectable and repeatable, not to create the illusion of perfect measurement.