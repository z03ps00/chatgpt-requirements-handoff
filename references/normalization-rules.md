# Human-requirements normalization rules

## Goal

Convert conversational, repetitive, incomplete, or partly conflicting input into an engineering-ready Contract without losing business intent or inventing requirements.

## Drop as noise

You may omit verbatim:
- emotional phrasing;
- greetings and coordination chatter;
- repeated statements of the same decision;
- discussion that does not affect the final decision;
- early options clearly superseded later;
- unsupported technical guesses unless they matter as an investigation lead.

## Always preserve

- final requirements;
- rationale when it explains an important constraint;
- exceptions and edge cases;
- negative requirements;
- exact text and values;
- qualifiers such as only, except, while preserving, do not change;
- confirmed technical facts;
- explicit environment constraints;
- reasons for rejecting important alternatives when the next engineer could otherwise repeat them.

## Negative statements

Treat phrases such as "do not change", "must not", "do not show", "do not create", "keep as is", "only", "except", or "without changing" as potentially important.

Classify them by meaning as Requirement, Non-Goal, Preserve, or Constraint.

## WHAT vs HOW

Input:
> Add an AfterWrite handler and show a dialog after posting.

If only the behavior is mandatory, normalize to:
- `R-*`: show a warning after successful posting;
- `INV-*` or possible approach: identify the correct implementation point.

Keep a specific handler as mandatory only when it is explicitly required or confirmed as a technical constraint/decision.

## Confidence

### CONFIRMED
Directly supported by an appropriate source.

Distinguish business evidence from technical evidence. A customer statement such as "the system currently does X" confirms the reported observation, not necessarily the internal mechanism behind X.

### INFERRED
A strong conclusion that still lacks sufficient verification.

### UNKNOWN
Insufficient evidence. Do not fill with the most likely answer.

## Business question vs technical investigation

Use `Q-*` when the answer requires a business decision, for example:
- exact user-facing text;
- priority between business rules;
- which behavior is correct;
- whether a process change is acceptable.

Use `INV-*` when system investigation can answer it, for example:
- where a mechanism is called;
- which form participates;
- which extension point is safer;
- whether a shared module already exists;
- which clients are actually supported;
- whether relevant tests already exist.

## Conflicts and chronology

When sources conflict:
1. Determine whether a later decision clearly supersedes an earlier one.
2. If yes, use the final decision and add `DEC-*` when the rationale matters.
3. If no, do not merge incompatible variants. Create `Q-*` or expose the conflict.

## Requirement atomicity

Bad:
> On posting, show a dialog, remove the old message, and do not change the validation algorithm.

Better:
- `R-001`: show the warning under condition X;
- `R-002`: remove the old notification path;
- `PR-001`: preserve the violation-detection algorithm.

## Scenarios and AC

A Scenario or Acceptance Criterion must not invent behavior absent from Requirements.

If AC construction reveals a missing rule, first add or refine a Requirement only when a source supports it. Otherwise preserve the uncertainty.
