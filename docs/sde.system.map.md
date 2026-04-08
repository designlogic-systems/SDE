# SDE System Map

## Purpose

This file explains how the major parts of SDE connect.

## High-Level Flow

Input
→ intake normalization
→ schema validation
→ AI question generation
→ output parsing
→ output validation
→ artifact generation
→ diagnostics / downstream handoff

## Main Repository Surfaces

- `sample-input/`
  - example intake used to demonstrate the system

- `sample-output/`
  - example customer-facing and technical outputs

- `schemas/`
  - input and output validation boundaries

- `n8n-workflow/`
  - n8n workflow export

- `fixtures/`
  - validation-oriented examples and expected outputs

- `docs-support/operators/`
  - operator contract and execution-lens prompt used in question generation

## Main Idea

SDE is designed to reduce ambiguity before downstream implementation by turning rough business input into a structured discovery artifact.