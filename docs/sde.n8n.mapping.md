# SDE n8n Mapping

## Purpose

This file maps major workflow nodes to their functional role inside SDE.

## Node Roles

- Prepare Intake Payload
  - shapes raw intake into a structured form

- Map Input to SDE Input Object
  - normalizes intake into the SDE input structure

- Load Input Schema
  - loads schema boundary for validation

- Validate Input Structure
  - verifies input admissibility

- AI Generate Question Set
  - produces grouped discovery questions from validated input

- Parse AI Output
  - reads model output into structured form

- Validate Output Structure
  - checks generated output against expected schema

- Prepare Output Artifact
  - packages the output for downstream surfaces

- Prepare Customer-Facing SDE Output
  - formats stakeholder-facing review output

- Prepare Technical SDE Output
  - emits machine-facing JSON artifact

- Internal Diagnostics Failure Gate
  - routes failed runs into visible diagnostics