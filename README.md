# Structured Discovery Engine (SDE)

Status: Active  
Version: 0.1

---

## What SDE Is

SDE is a structured AI workflow that converts ambiguous business problem descriptions into grouped discovery questions before any system design or automation begins.

It exists to force clarity **before execution**, not after.

---

## Why This Exists

Many AI and automation projects fail because the initial problem is:

- vague  
- incomplete  
- full of hidden assumptions  

SDE addresses this by:

- validating inputs  
- structuring ambiguity  
- exposing missing information  
- generating targeted discovery questions  

---

## What SDE Does

SDE:

- accepts rough business or workflow input  
- normalizes it into a structured intake format  
- validates it against a defined schema  
- generates grouped discovery questions  
- surfaces ambiguity and completeness gaps  
- produces outputs in Markdown, JSON, and PDF  
- emits diagnostics if outputs are invalid or incomplete  
- supports downstream handoff (e.g., AFE)

---

## What SDE Does Not Do

SDE does not:

- solve the business problem  
- generate implementation plans  
- make recommendations or decisions  
- automate execution  

It is a **pre-execution clarity system**.

---

## High-Level Flow

```
Raw Input
→ Intake Normalization
→ Schema Validation
→ AI Question Generation
→ Output Parsing
→ Output Validation
→ Artifact Generation
→ Diagnostics (if failure)
→ Optional Downstream Handoff
```

---

## Example Artifacts

See:

- `sample-input/` → example intake input  
- `sample-output/` → generated outputs  
- `screenshots/` → workflow and system views  

---

## Implementation Overview

SDE is currently implemented as an **n8n workflow** with:

- structured intake mapping  
- validation gates  
- bounded AI generation  
- output structure enforcement  
- artifact generation (Markdown, JSON, PDF)  
- internal diagnostics and failure signaling  

The workflow export is available in:

→ `workflow-export/sde.n8n.workflow.json`

---

## Repository Structure

```
sde/
├─ README.md
├─ screenshots/
├─ sample-input/
├─ sample-output/
├─ workflow-export/
├─ docs/
├─ docs-support/
├─ schemas/
└─ fixtures/
```

### Key Areas

- `sample-input/` → example problem inputs  
- `sample-output/` → generated question sets and artifacts  
- `screenshots/` → workflow visuals  
- `workflow-export/` → n8n workflow export  
- `schemas/` → input/output validation schemas  
- `docs/` → system-level explanation and mapping  
- `docs-support/` → playbooks and operator definitions  
- `fixtures/` → validation and test artifacts  

---

## Design Principles

SDE is built around:

- **structure over intuition**  
- **validation before generation**  
- **explicit outputs over implicit reasoning**  
- **failure visibility over silent degradation**  

---

## Example Use Case

Input:

> “We want to use AI to handle customer requests and maybe automate some internal processes, but we’re not sure how it should work yet.”

SDE output:

- grouped discovery questions  
- prioritized clarification areas  
- identified ambiguity gaps  
- structured input for downstream systems  

---

## Status

- SDE is implemented and operational  
- used as the first step in a broader pipeline  
- downstream systems (AFE, DTPL, AGBE) are defined but not yet implemented  

---

## Role in DesignLogic

SDE is the first tool in the DesignLogic applied system:

Ambiguity  
→ **SDE (Structured Discovery)**  
→ AFE (Refinement)  
→ DTPL (Trace & Protection)  
→ AGBE (Governance Blueprint)

---

## Summary

SDE is a system for turning unclear ideas into structured questions so that:

- assumptions are exposed  
- requirements are clarified  
- downstream systems can be built with confidence  