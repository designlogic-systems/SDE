# USO Operator Contract
Version: v0_1
Status: Draft
Scope: Structured Discovery Engine (SDE)
Classification: Tool-Local Operator (USS-Aligned, Non-Canon)

Operator ID: uso.sde.generate_question_set
Operator Family: SDE
Execution Surface: AI Generate Question Set
Governing Standards:
- `DESIGNLOGIC/USO/USO.spec.v1.0.md`
- `DESIGNLOGIC/USO/standards/uso.execution-lens.template.v0_1.md`
- `DESIGNLOGIC/USO/standards/uss.ai-node.integration.rules.v0_1.md`

Tool Governing Artifacts:
- `1-SDE/docs/sde.product.definition.v0_1.md`
- `1-SDE/docs/sde.question.generation.spec.v0_1.md`
- `1-SDE/docs/sde.workflow.v0_1.md`
- `1-SDE/docs/sde.workflow.governance.map.v0_1.md`
- `1-SDE/docs/sde.apex.slice.v0_1.md`
- `1-SDE/docs/sde.apex.graph.v0_1.md`

Schema References:
- `1-SDE/schemas/sde.input.schema.v0_1.json`
- `1-SDE/schemas/sde.output.schema.v0_1.json`

---

## 1. Name

SDE Generate Question Set

---

## 2. Purpose

This operator transforms a validated SDE input object into a structured discovery question set suitable for downstream review, artifact preparation, and later refinement stages.

It is a discovery-generation operator only.

It does not answer the underlying problem.
It does not produce final recommendations.
It does not produce execution plans.
It does not trigger workflows, authorize actions, or replace human judgment.

This boundary is consistent with SDE’s product definition as a definition-phase, execution-free tool whose purpose is to reduce ambiguity before downstream action. 

---

## 3. Intent

The intent of this operator is to:

- analyze a validated problem description and optional context
- identify the most relevant ambiguity domains
- generate grouped, high-signal discovery questions
- attach explicit question intent to each question
- assign priority based on ambiguity-reduction value
- optionally emit ambiguity flags and completeness notes
- remain within SDE’s first-pass discovery boundary

This operator exists to improve definition quality, not to solve the problem itself. 

---

## 4. Operator Role

This operator is the bounded semantic generation surface for the SDE question-generation stage.

Within the SDE workflow governance map, it corresponds to the semantic generation node with the role `DISCOVERY_QUESTION_GENERATION`, and it is explicitly constrained to discovery-only behavior with no execution planning and no recommendations. 

This operator is not:

- an execution node
- a recommendation node
- a planning node
- a validation node
- a comparison node
- a handoff-preparation node

---

## 5. Inputs

## 5.1 Required Input Envelope

The operator requires a request envelope containing:

- `request_id`
- `input`

The `input` payload must contain a validated SDE input object conforming to the SDE input contract.

At minimum, the validated input must support:
- `sde_version`
- `input_id`
- `problem_description`

This requirement is directly grounded in the question-generation spec. :contentReference[oaicite:3]{index=3}

## 5.2 Optional Input Content

If present and source-grounded, the operator may use:

- `business_context`
- `desired_outcome`
- `domain`
- `stakeholders`
- `known_constraints`
- `desired_output_type`
- `notes`
- `source_metadata`

These optional inputs may influence grouping logic, question specificity, ambiguity flags, and completeness notes. :contentReference[oaicite:4]{index=4}

## 5.3 Admitted Auxiliary References

The operator may use, when explicitly passed or embedded in stage context:

- normalized group names
- output structure reminders
- schema shape reminders
- operator-local generation constraints
- audit context

These references are admitted only to shape lawful generation.
They must not expand semantic authority.

---

## 6. Outputs

The operator emits a structured result envelope containing:

- `status`
- `output`
- optional `errors`
- optional `evidence`
- `audit`

When successful, `output` contains a candidate SDE output object intended for downstream parsing, structural validation, artifact shaping, and review.

This operator produces candidate discovery output only.
Final admissibility remains downstream of parse and output validation stages. 

---

## 7. Output Object Shape

The candidate output must align with the SDE output contract.

At minimum, the output should include:

- `sde_version`
- `output_id`
- `source_input_id`
- `question_groups`

Optional but recommended:
- `ambiguity_flags`
- `completeness_notes`

Each emitted question must include:
- `question_id`
- `question_text`
- `question_intent`
- `priority`

This is directly required by the question-generation spec and build plan. 

---

## 8. Allowed Transformations

The operator may perform only the following transformation classes:

### 8.1 Ambiguity Surface Identification
- identify major unresolved meaning surfaces present in the input
- determine which ambiguity classes are most relevant

### 8.2 Discovery Question Generation
- generate high-signal questions that materially reduce ambiguity
- target unresolved meaning rather than restating what is already clear

### 8.3 Structured Group Assignment
- assign each question to exactly one normalized group
- omit irrelevant groups
- avoid boilerplate group inflation

### 8.4 Priority Assignment
- assign `HIGH`, `MEDIUM`, or `LOW` priority based on ambiguity-reduction value

### 8.5 Intent Annotation
- provide a specific `question_intent` explaining what ambiguity the question is designed to reduce

### 8.6 Optional Ambiguity and Completeness Annotation
- emit ambiguity flags for major unresolved surfaces
- emit completeness notes when obvious missing context remains

These transformation classes are derived directly from the SDE question-generation specification. :contentReference[oaicite:7]{index=7}

---

## 9. Constraints

## 9.1 Hard Constraints

The operator must:

- remain discovery-only
- generate context-aware questions
- reduce ambiguity rather than inflate question count
- remain grounded in the validated input
- avoid unstated assumptions
- produce grouped structured output
- include `question_intent` for every question
- assign explainable priorities
- preserve SDE’s definition-first boundary

## 9.2 Forbidden Behaviors

The operator must not:

- answer the problem
- make final recommendations
- propose execution plans
- trigger workflows
- score answers
- produce follow-up logic for downstream phases
- produce legal, financial, medical, or operational judgment
- assume unstated facts
- emit generic filler when a more specific question is possible
- generate near-duplicate questions
- use questionnaire fullness as a substitute for relevance
- convert guessed context into output facts

These prohibitions are directly grounded in the question-generation spec and the SDE product/workflow boundaries. 

---

## 10. Grouping Rules

The operator must organize questions into one or more structured groups.

Allowed normalized group names are:

- `GOALS`
- `SCOPE`
- `CONSTRAINTS`
- `STAKEHOLDERS`
- `DATA_AND_SYSTEMS`
- `RISKS`
- `SUCCESS_CRITERIA`
- `ASSUMPTIONS`
- `OTHER`

Grouping requirements:

1. Every generated question must belong to exactly one group.
2. Every emitted group must contain at least one question.
3. Grouping must reflect actual ambiguity in the input, not a fixed template.
4. Irrelevant groups must be omitted.
5. `OTHER` may be used only when no existing normalized group captures the question cleanly.

These rules are taken directly from the SDE question-generation spec. :contentReference[oaicite:9]{index=9}

---

## 11. Priority Rules

Each generated question must include one of the following priority values:

- `HIGH`
- `MEDIUM`
- `LOW`

Priority reflects ambiguity-reduction value, not rhetorical force.

Priority assignment must remain explainable from the input and the question’s intent, consistent with the priority posture defined in the question-generation specification. :contentReference[oaicite:10]{index=10}

---

## 12. Question Intent Rules

Every generated question must include `question_intent`.

Intent requirements:

1. It must be specific.
2. It must explain why the question matters.
3. It must not merely restate the question.
4. It should identify the ambiguity class being reduced.

Intent is required for inspectability and downstream reuse. :contentReference[oaicite:11]{index=11}

---

## 13. Context-Awareness Rules

The operator must generate context-aware questions.

This means:

- workflow-oriented inputs should produce workflow-relevant questions
- automation-oriented inputs should surface control, authority, and constraint questions where relevant
- multi-stakeholder inputs should surface ownership and stakeholder questions
- risk-sensitive inputs should surface risk and constraint questions
- sparse inputs may justify broader foundational questions
- richer inputs should result in fewer, more precise questions

The same input under the same governing rules should yield substantially the same question-selection logic. :contentReference[oaicite:12]{index=12}

---

## 14. Unknown Handling

Unknown handling is mandatory.

When meaning is missing or unresolved, the operator must:

- surface missing information as a question
- emit ambiguity flags where major unresolved surfaces exist
- emit completeness notes where obvious missing context remains
- avoid guessing missing facts in order to preserve polish

The operator must not smooth over ambiguity or invent context merely to create a more complete-looking question set. :contentReference[oaicite:13]{index=13}

---

## 15. Operator Boundary

This operator generates first-pass discovery structure only.

It does not:

- validate its own output structurally
- determine final admissibility
- prepare customer-facing presentation artifacts
- prepare technical/developer artifacts
- prepare machine handoff artifacts
- resolve run status

These functions remain outside the operator and are handled elsewhere in the workflow. 

---

## 16. Failure Modes

This operator fails when it produces any of the following:

- generic filler questions
- repetitive or near-duplicate questions
- questions that ignore clear context
- questions that assume unstated facts
- missing coverage of obvious major ambiguity areas
- weak or unusable `question_intent`
- malformed grouping structure
- priorities that are not explainable from the input
- outputs that do not support downstream refinement

These failure modes are directly grounded in the question-generation spec and workflow quality posture. 

---

## 17. Success Criteria

The operator succeeds when it produces a candidate question set that is:

- grouped meaningfully
- context-aware
- non-generic
- ambiguity-reducing
- reusable by downstream tools
- inspectable by a human reviewer
- structurally aligned with the required output shape
- free from recommendation or execution drift

This success posture is directly aligned with the SDE product definition and question-generation spec. 

---

## 18. Audit Fields

The operator result should include audit fields sufficient for replayability and review.

Recommended audit content:

- `operator_id`
- `operator_version`
- `request_id`
- `source_input_id`
- `input_schema_ref`
- `output_schema_ref`
- `grouping_mode`
- `assumption_posture`
- `unknown_handling_posture`
- `notes`

This audit posture should support human inspection of whether the operator stayed within discovery boundary, avoided filler, and produced inspectable question logic. Review boundaries for semantic output and comparison are explicitly declared in the workflow governance map. 

---

## 19. Effects Posture

This operator is semantic-only.

It must not:

- invoke tools
- trigger external workflows
- perform external side effects
- access undeclared resources
- claim execution authority

Any side-effect permissions, if ever introduced, must be enforced outside the prompt through declared effects posture and runtime boundary, consistent with the deny-by-default stance of the USO effects-envelope specification. :contentReference[oaicite:18]{index=18}

---

## 20. Relationship to Execution Lens

The prompt used to realize this operator must be built from the USO execution-lens template and must explicitly encode:

- Layer 1 — Availability
- Layer 2 — Direction
- Layer 3 — Stabilization

The execution lens realizes this contract.
It does not replace it.

This is consistent with the USO spec’s separation between the operator contract, the execution lens, and the adapter/runtime execution layer. 

---

## 21. Plain-English Summary

This operator takes a validated SDE input and generates the first structured set of discovery questions.

It is allowed to identify ambiguity, group questions, assign intent, and set priorities.

It is not allowed to solve the problem, recommend actions, or move into execution planning.

Its job is to improve clarity before downstream refinement.

---

## 22. Summary

`uso.sde.generate_question_set` is the tool-local USO operator for the SDE question-generation stage.

It defines a bounded semantic operation that:

- analyzes validated intake
- identifies relevant ambiguity domains
- generates grouped, high-signal discovery questions
- attaches intent and priority
- optionally emits ambiguity flags and completeness notes
- remains strictly inside SDE’s definition-first, execution-free boundary

It is an SDE-local operator realization built under USO standards and is not yet a shared generalized operator.

---