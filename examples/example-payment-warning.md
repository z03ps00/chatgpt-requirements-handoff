# Example — warning after posting

A compact example of the expected result. It demonstrates semantics; do not copy empty sections or create items that the task does not need.

# Requirements Handoff Contract — payment-warning

## 0. Status
READY

## 1. Objective
Change how users are informed about a payment-schedule violation after successful posting. When a violation exists, show one separate warning while preserving the existing violation-detection algorithm.

## 2. Scope
### In Scope
- new user notification after posting;
- both Post and Post and Close flows;
- removal of the duplicate legacy notification.

### Out of Scope
#### NG-001 — Validation business rules
Do not change the rules that determine a payment-schedule violation.

## 3. Current Behavior
### CTX-001
**Status:** CONFIRMED  
**Fact / observation:** when a violation is detected, the user currently receives a system message.  
**Source:** SRC-001  
**Needs verification:** no

## 4. Expected Behavior
After successful posting, if a violation exists, the user receives one separate warning. If no violation exists, no extra warning appears.

## 5. Requirements
### R-001 — Warning after posting
**Condition:** the document is successfully posted and the existing check detects a violation.  
**Requirement:** show a separate warning to the user.  
**Expected result:** one warning per posting action.  
**Source:** SRC-001

### R-002 — Remove the legacy notification
**Condition:** a violation is detected.  
**Requirement:** do not show the duplicate legacy system message.  
**Expected result:** the user does not receive a second notification for the same violation.  
**Source:** SRC-001

## 6. Scenarios
### S-001 — Posting with a violation
**Covers:** R-001, R-002  
**Given:** the existing check identifies a violation.  
**When:** the user posts the document.  
**Then:** posting succeeds, exactly one warning is shown, and the legacy message is absent.

## 7. Acceptance Criteria
### AC-001
**Verifies:** R-001  
**Condition:** a violation exists.  
**Action:** the user posts the document.  
**Expected:** the warning appears exactly once.

### AC-002
**Verifies:** R-002  
**Condition:** a violation exists.  
**Action:** posting is performed.  
**Expected:** the legacy system message does not appear.

## 8. Preserve / Invariants
### PR-001 — Violation detection
The existing violation-detection algorithm and its input conditions must remain unchanged.

## 12. Technical Investigation
### INV-001
**Question:** which point in the current flow can show the warning correctly for both Post and Post and Close?  
**Why it matters:** the implementation must preserve the required behavior in both user flows.  
**Where to investigate:** form source and current write/post flow.  
**Blocks dependent technical decision:** yes

## 13. Open Business Questions
None.

## 16. Sources
### SRC-001
**Type:** business  
**Source:** original user requirement.  
**Supports:** R-001, R-002, PR-001

## 17. Traceability
| Requirement | Scenarios | Acceptance Criteria | Source |
|---|---|---|---|
| R-001 | S-001 | AC-001 | SRC-001 |
| R-002 | S-001 | AC-002 | SRC-001 |
