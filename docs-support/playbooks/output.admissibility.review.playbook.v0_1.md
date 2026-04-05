# Structured Discovery Engine (SDE)
## Output Admissibility Review Playbook
Version: 0.1
Status: STUB
Owner: Design Logic

---

# 1. Purpose

This playbook defines the human procedure for reviewing whether SDE outputs are admissible for their intended downstream use.

It exists to guide how an operator evaluates whether a generated SDE output may correctly function as:

- a customer-facing discovery artifact
- a technical/developer artifact
- an internal diagnostic artifact
- a machine handoff artifact for AFE
- a run result artifact

This playbook governs human review only.

It does not replace schemas, workflow logic, or artifact preparation nodes.

---

# 2. Applies To

This playbook applies to the following SDE structural areas:

- prepared output artifact review
- customer-facing output review
- technical/developer output review
- internal diagnostic output review
- SDE handoff object review
- final run result review

Primary graph attachment points:

- `Prepare Output Artifact`
- `Compare To Expected Output`
- `Internal Diagnostics Preparation`
- `Customer Output Preparation`
- `Technical Output Preparation`
- `SDE Handoff Preparation`
- `Emit Run Result`

---

# 3. Trigger Conditions

Use this playbook when any of the following occurs:

- a new SDE output artifact is produced
- a customer-facing artifact is prepared for sharing
- a technical/developer artifact is prepared for internal use
- a diagnostic artifact is prepared for internal review
- a handoff object is prepared for AFE
- the operator is unsure whether an output belongs to the correct artifact class
- outputs appear structurally valid but contextually misclassified
- output branching or artifact naming changes

---

# 4. Human Role

Primary role:
- operator / builder / reviewer

Optional supporting role:
- governance reviewer
- product reviewer
- downstream tool reviewer

The human role is to verify that an output artifact is admissible for its intended class and use.

The human role is not to silently repurpose one artifact class into another without explicit reclassification.

---

# 5. Governing Inputs

This playbook is governed by:

- `1-SDE/docs/sde.product.definition.v0_1.md`
- `1-SDE/docs/sde.workflow.v0_1.md`
- `1-SDE/docs/sde.n8n.build.plan.v0_1.md`
- `1-SDE/docs/sde.apex.slice.v0_1.md`
- `1-SDE/docs/sde.apex.graph.v0_1.md`
- `1-SDE/schemas/sde.output.schema.v0_1.json`

Optional review inputs:

- prepared output artifact
- customer-facing output artifact
- technical/developer artifact
- internal diagnostics artifact
- SDE handoff artifact
- run result artifact
- comparison notes
- operator notes

---

# 6. Review Procedure

## Step 1 — Identify Artifact Class

Determine which output class is under review.

Allowed SDE output classes include:

- SDE Discovery Question Set
- SDE Prepared Output Artifact
- SDE Comparison Result
- SDE Internal Diagnostic Output
- SDE Customer-Facing Discovery Output
- SDE Technical/Developer Output
- SDE Handoff Object for AFE
- SDE Run Result

Record the intended artifact class explicitly.

## Step 2 — Confirm Artifact Eligibility

Check whether the artifact class is allowed under the SDE Apex Slice artifact contract.

Questions to ask:

- Is this artifact class explicitly allowed?
- Is this output being treated as something SDE is actually permitted to emit?
- Is any disallowed output being smuggled in through naming or formatting?

If the artifact class is not allowed, the output is inadmissible.

## Step 3 — Confirm Output Matches Intended Audience

Inspect whether the artifact matches the audience and purpose it claims.

### For customer-facing output
Check:
- readable by non-technical users
- focused on discovery questions
- no internal diagnostics leakage
- no machine-only structural clutter

### For technical/developer output
Check:
- structurally useful
- clear for internal technical review
- not pretending to be a machine handoff by default

### For internal diagnostic output
Check:
- comparison or debugging information present
- not formatted as customer-facing output
- not treated as final handoff artifact

### For machine handoff output
Check:
- explicitly classified as handoff artifact
- machine-consumable
- not mixed with customer prose or diagnostic commentary
- suitable for AFE consumption

### For run result output
Check:
- describes workflow result, not discovery content itself
- not substituted for the actual discovery artifact

## Step 4 — Confirm Artifact Boundary Integrity

Questions to ask:

- Has a customer-facing artifact been incorrectly treated as a handoff object?
- Has a diagnostic artifact been incorrectly treated as a customer artifact?
- Has a technical output been incorrectly treated as final workflow result?
- Has a prepared output artifact been mistaken for a fully classified downstream artifact?

Artifact classes must remain distinct.

## Step 5 — Confirm Admissibility for Downstream Use

If the artifact is intended for downstream use, confirm that it is admissible in that path.

Example checks:

- customer-facing output may go to human review or customer delivery
- handoff object may go to AFE
- diagnostic output may go to internal review only
- run result may go to workflow monitoring or reporting

An artifact is inadmissible if it is structurally correct but routed to the wrong downstream consumer.

## Step 6 — Record Findings

Record one of the following findings:

- output admissible as classified
- output partially admissible
- output inadmissible
- artifact class needs correction
- downstream routing needs correction
- audience mismatch detected
- artifact boundary collapse detected

---

# 7. Expected Outputs

This playbook should produce one or more of the following human outcomes:

- confirmation that the artifact is admissible for its intended use
- identification of artifact misclassification
- identification of audience mismatch
- identification of boundary collapse between artifact classes
- recommendation to relabel or reroute the output
- recommendation to revise workflow branching or artifact preparation logic

This playbook does not itself generate machine artifacts automatically.

---

# 8. Review Standards

## 8.1 Pass Standard

Output admissibility is considered correct when:

- the artifact class is allowed by the SDE Apex Slice
- the artifact is correctly classified
- the artifact matches its intended audience
- the artifact is routed only to an admissible downstream consumer
- no boundary collapse exists between artifact classes

## 8.2 Partial Standard

Output admissibility is partial when:

- the artifact is mostly usable
- but contains mixed signals about audience or purpose
- or contains small amounts of content that belong to another artifact class
- or the routing logic is understandable but not fully clean

## 8.3 Fail Standard

Output admissibility is failing when:

- the artifact class is not allowed
- customer-facing output is being treated as machine handoff
- diagnostic output is being treated as customer-facing
- run result is substituted for content artifact
- output is structurally valid but contextually routed to the wrong consumer
- artifact class boundaries are materially collapsed

---

# 9. Non-Goals

This playbook does not:

- redefine the Apex Slice artifact contract
- redefine the output schema
- replace output validation
- define AFE input behavior in detail
- define DTPL trace closure
- authorize downstream execution
- act as a general product-review playbook

Its job is output admissibility review only.

---

# 10. Current Maturity

- Maturity: STUB
- Operational Readiness: LIMITED
- Intended Use: development and early prototype review

This playbook is currently a minimal procedural attachment to the SDE Apex Slice.

It may be expanded later with:

- artifact audience checklist
- handoff-object readiness checklist
- branch-by-branch routing review rules
- artifact class examples and anti-patterns

---

# 11. Summary

This playbook defines the human review procedure for SDE output admissibility.

It ensures that:

- only allowed artifact classes are emitted
- each output matches its intended audience and purpose
- downstream routing stays correct
- customer, diagnostic, technical, handoff, and run-result artifacts do not collapse into one another