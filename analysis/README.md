# SDE Analysis

## Purpose

This directory contains the evaluation and refinement system for the Structured Discovery Engine (SDE).

Its purpose is to make SDE behavior measurable across repeated runs so execution-lens refinement can be based on structured evidence instead of one-off output judgment.

## What this analysis system does

The SDE analysis system is designed to measure:

- structural consistency
- semantic coverage consistency
- bounded variability across repeated runs

It supports execution-lens refinement by capturing evidence at three levels:

- run level
- group level
- question level

## Core analysis artifacts

- `sde.analysis.system.md`
  - defines the full analysis system, its purpose, architecture, and refinement role

- `data_model.md`
  - defines the evidence tables, metric tables, and their responsibilities

- `metrics_framework.md`
  - defines the Availability, Direction, and Stabilization metric model

- `execution_lens_refinement_loop.md`
  - defines the refinement loop used to improve SDE behavior

- `experiment_design.md`
  - defines how repeated-run experiments are structured and evaluated

## Analysis principles

SDE is not evaluated by exact output identity.

Instead, it is evaluated by whether repeated runs preserve:

- stable structure
- consistent semantic coverage
- bounded variability

## Current status

This analysis system is specific to SDE.

It is the first implemented case of a broader product analysis pattern that may later be generalized within DesignLogic.