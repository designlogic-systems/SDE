# SDE Fixture Notes
## F01
Version: 0.1
Status: Active
Owner: Design Logic

---

# 1. Purpose

This file documents the intent and review posture for fixture `F01`.

It exists to explain:

- what the fixture is testing
- why it is a good first SDE test case
- what the expected output is intended to demonstrate
- what kinds of failures or weaknesses the fixture should help surface

This file is descriptive only.

It does not replace the input schema, output schema, or expected output artifact.

---

# 2. Fixture Identity

- Fixture ID: `F01`
- Input File: `F01_valid_input.json`
- Expected Output File: `F01_expected_output.json`
- Tool: Structured Discovery Engine (SDE)
- Fixture Type: Positive / valid-input baseline

---

# 3. Fixture Summary

`F01` represents an early-stage internal AI assistant request in which the operator wants to explore a tool that can:

- answer SOP questions for an operations team
- possibly create maintenance tickets later
- reduce repetitive operational support work
- improve response speed

The request is intentionally underdefined.

It blends:

- advisory behavior
- possible future execution behavior
- unclear systems access
- unclear approval requirements
- unclear success criteria

That makes it a strong baseline discovery fixture.

---

# 4. Why This Is a Good SDE Test Case

This fixture is a good first SDE case because it contains multiple important ambiguity classes without being unrealistic.

It includes:

- objective ambiguity
- scope ambiguity
- stakeholder ambiguity
- system/data ambiguity
- risk ambiguity
- approval ambiguity
- success-criteria ambiguity
- assumption ambiguity

This allows SDE to demonstrate its core value:

- grouped first-pass discovery
- high-signal question generation
- ambiguity surfacing
- completeness signaling

---

# 5. What the Input Is Testing

`F01_valid_input.json` is intended to test whether SDE can correctly handle an intake that is:

- structurally valid
- semantically early-stage
- broad enough to require first-pass discovery
- rich enough to support grouped questioning
- ambiguous enough to expose whether SDE is actually useful

More specifically, the input tests whether SDE can distinguish between:

- current desired behavior
- future possible behavior
- known constraints
- unknown governance boundaries

without collapsing those into recommendations.

---

# 6. What Good SDE Output Should Demonstrate

A good SDE output for `F01` should demonstrate all of the following:

## 6.1 Correct Discovery Role

The output should remain in discovery mode.

It should:

- ask questions
- not solve the problem
- not recommend architecture
- not recommend tools
- not produce execution plans
- not issue decisions

## 6.2 Strong Grouping

The output should organize questions into meaningful discovery groups such as:

- GOALS
- SCOPE
- CONSTRAINTS
- STAKEHOLDERS
- DATA_AND_SYSTEMS
- RISKS
- SUCCESS_CRITERIA
- ASSUMPTIONS

`OTHER` may appear if justified, but should not be used as a default dumping group.

## 6.3 High-Signal Questions

The output should ask questions that materially reduce ambiguity.

Good questions for this fixture should focus on areas like:

- what the first version is actually meant to do
- whether the first phase is advisory-only
- what systems the assistant should access
- who owns approvals and governance
- what risks are unacceptable
- how success would be measured

## 6.4 Good Question Intent

Each question should include a meaningful `question_intent` that explains why the question matters.

Intent should not merely restate the question.

## 6.5 Believable Priorities

The highest-priority questions should be the ones most critical to:

- defining scope
- identifying constraints
- clarifying risk
- determining ownership
- separating advisory use from action-taking behavior

## 6.6 Ambiguity and Completeness Signaling

A good output should surface:

- ambiguity flags where major unresolved areas exist
- completeness notes when the input is still too weak for downstream certainty

---

# 7. What Bad Output Would Look Like

A weak or failing SDE output for this fixture would show one or more of the following:

- generic filler questions
- repeated questions with slight wording changes
- missing the advisory vs automation distinction
- ignoring unclear approval boundaries
- failing to ask about systems access
- failing to ask about success criteria
- drifting into recommendations or solutioning
- weak or circular `question_intent`
- priorities that do not reflect ambiguity importance

---

# 8. Relationship to Expected Output

`F01_expected_output.json` is not intended to be the only possible correct output.

It is intended to function as a **gold reference** for:

- structure
- quality level
- grouping logic
- ambiguity coverage
- expected usefulness

Equivalent wording variation is acceptable.

What matters is whether the generated output is materially aligned with the expected discovery function.

---

# 9. Fixture Review Posture

When reviewing SDE output against this fixture, the reviewer should ask:

- Did SDE remain in discovery mode?
- Did SDE generate context-aware groups?
- Did SDE ask the right kinds of questions?
- Did SDE surface the key ambiguity areas?
- Did SDE avoid premature recommendation behavior?
- Would answering these questions actually improve downstream clarity?

This fixture is successful when it helps expose both structural correctness and discovery quality.

---

# 10. Non-Goals

This fixture does not attempt to test:

- full production realism
- multiple rounds of refinement
- downstream AFE behavior
- DTPL trace closure
- AGEF handoff
- complex negative-case branching

Its purpose is to provide a strong positive baseline for first-pass SDE discovery behavior.

---

# 11. Summary

`F01` is the baseline positive fixture for SDE v0.1.

It is designed to test whether SDE can take an early-stage, underdefined internal AI request and convert it into a structured, high-signal first-pass discovery question set that is:

- grouped
- useful
- inspectable
- ambiguity-aware
- non-recommendatory