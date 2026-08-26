# Requirements Handoff Contract — [short task name]

## 0. Status
`READY | DRAFT | BLOCKED`

## 1. Objective
[What must change, why, and the required observable outcome.]

## 2. Scope
### In Scope
- [item]

### Out of Scope
#### NG-001 — [name]
[Intentionally excluded behavior.]

## 3. Current Behavior
### CTX-001
**Status:** `CONFIRMED | INFERRED | UNKNOWN`  
**Fact / observation:** [description]  
**Source:** `SRC-001 | none`  
**Needs verification:** `yes | no`

## 4. Expected Behavior
[Short target flow without new requirements.]

## 5. Requirements
### R-001 — [name]
**Condition:** [when it applies]  
**Requirement:** [what the system must do]  
**Expected result:** [observable result]  
**Source:** `SRC-001 | original request`

## 6. Scenarios
### S-001 — [name]
**Covers:** `R-001`  
**Given:** [initial state]  
**When:** [action / event]  
**Then:** [expected result]

## 7. Acceptance Criteria
### AC-001
**Verifies:** `R-001`  
**Condition:** [state]  
**Action:** [what happens]  
**Expected:** [unambiguous result]

## 8. Preserve / Invariants
### PR-001 — [name]
[Behavior that must keep working.]

## 9. Constraints
### Functional
None.

### Technical
None.

## 10. Exact Text and Values
None.

## 11. Known Technical Context
None.

## 12. Technical Investigation
### INV-001
**Question:** [question]  
**Why it matters:** [impact]  
**Where to investigate:** [source / configuration / docs / runtime / tests / other]  
**Blocks dependent technical decision:** `yes | no`

## 13. Open Business Questions
None.

## 14. Decisions and Rejected Alternatives
None.

## 15. Risks
None.

## 16. Sources
### SRC-001
**Type:** [business / source-code / configuration / documentation / runtime / test / communication]  
**Source:** [description]  
**Supports:** [CTX/R/PR/VAL]

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
