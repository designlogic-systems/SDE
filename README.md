
# Structured Discovery Engine (SDE)

**Status:** Active  
**Version:** 0.1

---

## What SDE Is

SDE is a working AI workflow that converts ambiguous business or workflow requests into grouped discovery questions **before** system design, automation, or implementation begins.

It is designed to force clarity at the intake stage by turning rough problem descriptions into structured discovery artifacts.

---

## What This Repo Demonstrates

This repository demonstrates:

- AI workflow design in **n8n**
- structured intake normalization
- schema-aware input validation
- bounded AI question generation
- output parsing and validation
- multi-format artifact generation
- failure diagnostics and visibility
- workflow documentation and system mapping

This is not a prompt experiment. It is a structured workflow artifact with explicit validation, output discipline, and supporting documentation.

---

## Why This Exists

Many AI and automation efforts fail before execution because the initial request is:

- vague
- incomplete
- under-scoped
- full of hidden assumptions
- missing constraints or success criteria

SDE addresses that failure surface by generating the discovery questions needed to clarify the problem **before downstream build work starts**.

---

## What SDE Does

SDE:

- accepts rough business or workflow input
- normalizes it into a structured intake format
- validates it against a defined input schema
- generates grouped discovery questions
- surfaces ambiguity and completeness gaps
- validates output structure against a defined output schema
- produces artifacts in Markdown, JSON, and PDF
- emits diagnostics if output is invalid or incomplete
- supports downstream handoff into later stages

---

## What SDE Does Not Do

SDE does **not**:

- solve the business problem
- generate implementation plans
- make recommendations or decisions
- execute automation
- replace downstream design or governance work

SDE is a **pre-execution clarity system**.

---

## High-Level Workflow

```text
Raw Input
→ Intake Normalization
→ Schema Validation
→ AI Question Generation
→ Output Parsing
→ Output Validation
→ Artifact Generation
→ Diagnostics (if failure)
→ Optional Downstream Handoff
````

---

## 3-Minute Review Path

For a fast review of the repo:

1. Read this README
2. Open `docs/sde_demo_script.md`
3. Review `sample-input/sample_input_01.md`
4. Review `sample-output/sample_output_01.md`
5. Inspect `n8n-workflow/sde.n8n.workflow.json`
6. Review `screenshots/`

This gives the quickest view of the system, the workflow shape, and the generated artifacts.

---

## Repository Structure

```text
sde/
├─ README.md
├─ docs/
├─ docs-support/
├─ fixtures/
├─ sample-input/
├─ sample-output/
├─ schemas/
├─ screenshots/
└─ n8n-workflow/
```

### Key Areas

* `docs/`
  System explanation, workflow mapping, and demo guidance

* `docs-support/`
  Operator definitions

* `fixtures/`
  Validation and test artifacts

* `sample-input/`
  Example intake input

* `sample-output/`
  Example generated outputs and artifacts

* `schemas/`
  Input and output validation schemas

* `screenshots/`
  Workflow, system, and execution visuals

* `n8n-workflow/`
  Exported n8n workflow definition

---

## Implementation Overview

SDE is currently implemented as an **n8n workflow** with:

* structured intake mapping
* schema validation gates
* bounded AI generation
* output structure enforcement
* artifact generation
* internal diagnostics and failure signaling

Workflow export:

`n8n-workflow/sde.n8n.workflow.json`

---

## Example Use Case

Input:

> “We want to use AI to handle customer requests and maybe automate some internal processes, but we’re not sure how it should work yet.”

SDE output:

* grouped discovery questions
* prioritized clarification areas
* identified ambiguity gaps
* structured artifacts for downstream review or handoff

---

## Example Artifacts

See:

* `sample-input/` for example intake input
* `sample-output/` for generated question sets and artifacts
* `screenshots/` for workflow and system views

---

## Design Principles

SDE is built around:

* **structure over intuition**
* **validation before generation**
* **explicit outputs over implicit reasoning**
* **failure visibility over silent degradation**
* **clarity before execution**

---

## Current Role in the Broader System

SDE is the first implemented workflow in a broader DesignLogic definition pipeline:

```text
Ambiguity
→ SDE (Structured Discovery)
→ AFE (Refinement)
→ DTPL (Trace & Protection)
→ AGBE (Governance Blueprint)
```

At present, SDE is the implemented and operational first stage.

---

## What This Repo Shows

This repo shows the ability to design and document an AI workflow with:

* bounded intake handling
* validation-aware workflow structure
* LLM integration with output discipline
* artifact generation across formats
* explicit failure handling
* downstream-oriented system design

---

## Status

* SDE is implemented and operational
* SDE is currently the first step in a broader pipeline
* downstream systems are defined but not yet implemented in this public repo

---

## Summary

SDE turns unclear business or workflow requests into structured discovery questions so that:

* assumptions are exposed
* requirements are clarified
* ambiguity is made visible
* downstream work starts from a stronger definition state