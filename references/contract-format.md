# Requirements Handoff Contract format

## Purpose

The Contract is a neutral analysis artifact between a human task description and engineering work. It is not `design.md`, an implementation plan, or a coding task list.

## IDs

Use stable IDs only for real items:
- `R-001` Requirement
- `S-001` Scenario
- `AC-001` Acceptance Criterion
- `NG-001` Non-Goal
- `PR-001` Preserve / invariant
- `FC-001` Functional Constraint
- `TC-001` Technical Constraint
- `VAL-001` Exact Value
- `INV-001` Technical Investigation
- `Q-001` Business Open Question
- `DEC-001` Significant Decision / rejected alternative
- `RISK-001` Risk
- `SRC-001` Evidence / Source
- `CTX-001` Current context fact

Do not create placeholder items just to fill the template.

## Output structure

```markdown
# Requirements Handoff Contract — <short task name>

## 0. Status
READY | DRAFT | BLOCKED

## 1. Objective
<what changes, why, and the required observable outcome>

## 2. Scope
### In Scope
- ...

### Out of Scope
#### NG-001 — <name>
<intentionally excluded behavior>

## 3. Current Behavior
### CTX-001
**Status:** CONFIRMED | INFERRED | UNKNOWN
**Fact / observation:** ...
**Source:** SRC-001 | none
**Needs verification:** yes | no

## 4. Expected Behavior
<short target flow; no new requirements>

## 5. Requirements
### R-001 — <name>
**Condition:** ...
**Requirement:** ...
**Expected result:** ...
**Source:** SRC-001 | original request

## 6. Scenarios
### S-001 — <name>
**Covers:** R-001
**Given:** ...
**When:** ...
**Then:** ...

## 7. Acceptance Criteria
### AC-001
**Verifies:** R-001
**Condition:** ...
**Action:** ...
**Expected:** ...

## 8. Preserve / Invariants
### PR-001 — <name>
<behavior that must keep working>

## 9. Constraints
### Functional
#### FC-001
...

### Technical
#### TC-001
...

## 10. Exact Text and Values
### VAL-001 — <purpose>
```text
<exact value>
```

## 11. Known Technical Context
- ...

## 12. Technical Investigation
### INV-001
**Question:** ...
**Why it matters:** ...
**Where to investigate:** source | configuration | docs | runtime | tests | other
**Blocks dependent technical decision:** yes | no

## 13. Open Business Questions
### Q-001
**Question:** ...
**Blocking:** yes | no
**Owner:** customer | analyst | product owner | other

## 14. Decisions and Rejected Alternatives
### DEC-001
**Decision:** ...
**Rejected alternative:** ...
**Reason:** ...
**Source:** SRC-001

## 15. Risks
### RISK-001
**Risk:** ...
**Related to:** R-001 / PR-001
**Why it matters:** ...

## 16. Sources
### SRC-001
**Type:** business | source-code | configuration | documentation | runtime | test | communication
**Source:** ...
**Supports:** CTX-001, R-001, PR-001, VAL-001

## 17. Traceability
| Requirement | Scenarios | Acceptance Criteria | Source |
|---|---|---|---|
| R-001 | S-001 | AC-001 | SRC-001 |

## 18. Handoff Conditions
- preserve `R-*` meaning;
- respect `NG-*`;
- preserve `PR-*`;
- respect Constraints and `VAL-*`;
- do not treat assumptions as facts;
- resolve relevant `INV-*` before dependent decisions;
- expose conflicts between the Contract and the actual system;
- preserve requirement-to-verification traceability.
```

## Section semantics

### Objective
States what and why. No unconfirmed HOW.

### Current Behavior / CTX
Current state only. Keep desired behavior separate. Mark each material statement `CONFIRMED`, `INFERRED`, or `UNKNOWN`.

### Expected Behavior
A compact target-flow overview. It must not introduce new requirements.

### Requirements
Primary source of truth for required behavior. Mandatory requirements must be atomic and testable.

### Scenarios
Show requirements in context. They do not create new requirements.

### Acceptance Criteria
Primary completion-verification contract. Every mandatory `R-*` needs at least one `AC-*`.

### Non-Goals
Intentionally excluded scope.

### Preserve
Regression invariants that must continue to work.

### Constraints
Restrict valid solutions without inventing new business behavior.

### Technical Investigation
Questions the next engineering stage can answer by inspecting the system. Not customer questions by default.

### Open Business Questions
Only missing business decisions. A blocking `Q-*` may justify `BLOCKED`.

### Decisions
Keep rationale for important accepted/rejected alternatives when losing it could cause a rejected approach to be proposed again.

## Conflict precedence

1. Explicit final business decisions and `VAL-*`
2. `R-*`
3. `NG-*`, `PR-*`, Constraints
4. `AC-*`
5. Expected Behavior
6. `S-*`
7. Known Technical Context
8. Assumptions and examples

If a conflict changes observable business behavior and sources cannot resolve it, expose the conflict instead of choosing silently.
