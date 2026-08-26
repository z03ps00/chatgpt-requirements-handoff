# Quality Gates

Run this review before returning a Contract.

## Gate 1 — Understandable without the original chat
PASS if another engineer can understand the task, scope, and expected result without reading the raw human input.

## Gate 2 — No invented requirements
For every `R-*`, verify that it is grounded in the input, is not merely model-preferred "best practice", and does not hide an unconfirmed implementation choice.

## Gate 3 — WHAT is separate from HOW
A procedure, module, handler, API, or architecture mechanism must not become a Requirement unless explicitly mandated.

## Gate 4 — Fact / inference / unknown
Classify material current-state claims honestly. No `INFERRED` statement may be presented as confirmed.

## Gate 5 — Scope
Verify In Scope, Out of Scope, and Preserve. `NG-*` and `PR-*` are not interchangeable.

## Gate 6 — Testability
Every mandatory `R-*` has an observable result and at least one `AC-*`. AC should not require internal implementation knowledge unless necessary.

## Gate 7 — No hidden requirements in Scenarios or AC
Material statements in `S-*` and `AC-*` must trace to `R-*`, `PR-*`, or a Constraint.

## Gate 8 — Unknowns are split correctly
Technical unknown -> `INV-*`. Missing business decision -> `Q-*`. Do not use `BLOCKED` only because a technical question remains investigable.

## Gate 9 — Sources
Do not invent `SRC-*`. Material confirmed facts should reference real evidence when available.

## Gate 10 — Rationale
If an important option was explicitly rejected and the reason may affect future design, preserve it as `DEC-*`.

## Gate 11 — Neutrality
The Contract must not require OpenSpec, `/opsx propose`, a specific Plan Mode, `design.md`, a specific agent loop, or a tool-specific implementation report.

## Gate 12 — Status
- `READY`: business meaning is sufficient for the next stage.
- `BLOCKED`: only a genuinely blocking business decision is missing.
- `DRAFT`: normalization is objectively incomplete.

## Final traceability check
Ensure the traceability table contains every mandatory `R-*` and at least one `AC-*` for each.
