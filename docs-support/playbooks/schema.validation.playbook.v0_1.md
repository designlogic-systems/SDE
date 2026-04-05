# Structured Discovery Engine (SDE)
## Schema Validation Playbook
Version: 0.1
Status: STUB
Owner: Design Logic

---

# 1. Purpose

This playbook defines the human procedure for reviewing schema validation behavior within Structured Discovery Engine (SDE).

It exists to guide how an operator evaluates whether:

- input artifacts conform to the SDE input contract
- output artifacts conform to the SDE output contract
- validation failures were surfaced correctly
- downstream gating behavior matched the validation result

This playbook governs human review only.

It does not replace machine validation logic.

---

# 2. Applies To

This playbook applies to the following SDE structural areas:

- input contract validation
- output contract validation
- validation fail branches
- admissibility gating after validation
- validation-related run results

Primary graph attachment points:

- `Validate Input Structure`
- `Input Admissibility Gate`
- `Validate Output Structure`
- fail/stop boundaries related to invalid input or invalid output

---

# 3. Trigger Conditions

Use this playbook when any of the following occurs:

- a new input fixture is introduced
- a new output fixture is introduced
- input validation fails
- output validation fails
- schema files are changed
- workflow node behavior changes around validation
- gating behavior appears incorrect
- comparison output suggests malformed or weak structure
- the operator wants to confirm that validation is enforcing the intended contract

---

# 4. Human Role

Primary role:
- operator / builder / reviewer

Optional supporting role:
- technical reviewer
- governance reviewer

The human role is to inspect validation behavior and decide whether the workflow is behaving consistently with the declared schema contracts.

The human role is not to override the schema informally.

---

# 5. Governing Inputs

This playbook is governed by:

- `1-SDE/schemas/sde.input.schema.v0_1.json`
- `1-SDE/schemas/sde.output.schema.v0_1.json`
- `1-SDE/docs/sde.workflow.v0_1.md`
- `1-SDE/docs/sde.n8n.build.plan.v0_1.md`
- `1-SDE/docs/sde.apex.slice.v0_1.md`
- `1-SDE/docs/sde.apex.graph.v0_1.md`

Optional review inputs:

- `1-SDE/fixtures/F01_valid_input.json`
- `1-SDE/fixtures/F01_expected_output.json`
- workflow run outputs
- validation error outputs
- run result artifact

---

# 6. Review Procedure

## Step 1 — Identify Validation Surface

Determine which validation surface is being reviewed:

- input validation
- output validation
- both

Record the artifact or workflow run under review.

## Step 2 — Confirm Governing Schema

Verify which schema is authoritative for the boundary:

- input boundary -> `sde.input.schema.v0_1.json`
- output boundary -> `sde.output.schema.v0_1.json`

Do not validate against memory or expectation alone.

## Step 3 — Inspect Actual Object Shape

Inspect the actual object being validated.

Check:

- required fields
- field types
- enum values
- array/object structure
- additional property behavior
- nested object structure where relevant

## Step 4 — Compare Validation Outcome to Contract

Confirm that the machine validation result is consistent with the schema.

Questions to ask:

- did the validator catch missing required fields?
- did it catch invalid enum values?
- did it reject malformed arrays or objects?
- did it preserve valid inputs as pass?
- did it preserve valid outputs as pass?

## Step 5 — Confirm Downstream Consequence

Check whether workflow control matched validation status.

For invalid input:
- downstream semantic generation must not continue

For invalid output:
- artifact preparation and comparison should not proceed as though the output were valid

Validation review is incomplete if only the error is surfaced but execution control is wrong.

## Step 6 — Record Findings

Record one of the following findings:

- validation behavior correct
- validation behavior partially correct
- validation behavior incorrect
- schema needs revision
- workflow gating needs revision

---

# 7. Expected Outputs

This playbook should produce one or more of the following human outcomes:

- confirmation that validation behavior is correct
- identified mismatch between schema and workflow behavior
- identified mismatch between validation result and gating behavior
- recommendation to revise a schema
- recommendation to revise validation logic
- recommendation to revise downstream gating

This playbook does not itself generate machine artifacts automatically.

---

# 8. Review Standards

## 8.1 Pass Standard

Validation behavior is considered correct when:

- the correct schema was applied
- valid objects pass
- invalid objects fail
- failure reasons are inspectable
- downstream behavior matches pass/fail status

## 8.2 Partial Standard

Validation behavior is partial when:

- core structural issues are caught
- but some edge-case checks are weak
- or downstream gating is inconsistent
- or error reporting is unclear but not misleading

## 8.3 Fail Standard

Validation behavior is failing when:

- invalid objects are treated as valid
- valid objects are rejected without contract basis
- workflow continues past invalid input or invalid output without explicit justification
- the operator cannot determine why validation passed or failed

---

# 9. Non-Goals

This playbook does not:

- redefine the schemas
- act as a substitute for schema files
- authorize manual bypass of validation
- replace workflow logic
- replace comparison review
- define semantic quality of questions
- define customer-facing output quality

Its job is validation review only.

---

# 10. Current Maturity

- Maturity: STUB
- Operational Readiness: LIMITED
- Intended Use: development and early prototype review

This playbook is currently a minimal procedural attachment to the SDE Apex Slice.

It may be expanded later with:

- edge-case review checklist
- schema revision decision rules
- invalid artifact examples
- remediation flow for repeated validation failures

---

# 11. Summary

This playbook defines the human review procedure for schema validation behavior in SDE.

It ensures that:

- schema contracts are actually being enforced
- failures are surfaced correctly
- downstream gating matches validation outcomes
- the operator has a repeatable method for checking contract-boundary behavior