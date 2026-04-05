# SDE Demo Script

## Short Version

SDE is a structured AI workflow that takes a vague business problem and turns it into grouped discovery questions before any downstream design or automation begins.

## Walkthrough

1. Start with rough business input.
2. Normalize it into a structured input object.
3. Validate the input against a schema.
4. Use a bounded AI step to generate grouped discovery questions.
5. Validate the generated output.
6. Emit customer-facing, technical, and diagnostic artifacts.
7. Use the result to reduce ambiguity before implementation.