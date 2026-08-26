---
name: requirements-handoff
description: "ChatGPT Skill для преобразования неструктурированных человеческих ТЗ, задач из трекера, переписки, писем, заметок и расшифровок встреч в нейтральный Requirements Handoff Contract. Использовать в ChatGPT, когда нужно формализовать задачу для разработчика или следующего AI-этапа, подготовить ТЗ/спецификацию/handoff либо отделить требования от технических предположений и реализации."
license: MIT
metadata:
  version: "1.1.0"
  language: "en"
  artifact: "requirements-handoff-contract"
---

# Requirements Handoff

Turn messy human task descriptions into a neutral requirements contract that the next engineering stage can use without reconstructing intent from chat history.

## Use when

Use this skill when the user asks to:
- formalize a task or specification for a developer;
- prepare a task for an AI coding agent;
- convert tracker issues, chat, email, meeting notes, or research into a specification;
- prepare a development handoff;
- prepare input for OpenSpec, `/opsx propose`, or Plan Mode;
- separate requirements from technical assumptions or implementation ideas;
- consolidate scattered requirements into a testable contract.

Do not use it as the primary workflow when the user already has a sufficient contract and asks only for implementation, technical design, a tiny wording edit, or a plain summary.

## Inputs

Inputs may include user text, files, tracker issues, comments, email, meeting transcripts, research, source code, or technical notes.

When sources are provided, ground the contract in those sources. Do not fill gaps with general knowledge unless clearly marked as an assumption.

## Workflow

1. **Extract intent.** Identify the goal and observable outcome.
2. **Normalize input.** Remove repetition and conversational noise, but preserve decisions, exceptions, constraints, negative requirements, and important rejected alternatives.
3. **Separate information types.** Distinguish required behavior, current context, and implementation ideas.
4. **Classify confidence.** Use `CONFIRMED`, `INFERRED`, `UNKNOWN`.
5. **Set scope.** Capture In Scope, `NG-*`, and `PR-*`. Non-Goal and Preserve are different.
6. **Build requirements.** Create atomic, testable `R-*` that describe WHAT, not HOW.
7. **Add behavior checks.** Create `S-*` and `AC-*`. They must not introduce new requirements.
8. **Split unknowns.** Put system-research questions in `INV-*`; unresolved business decisions in `Q-*`.
9. **Capture constraints and evidence.** Use `FC-*`, `TC-*`, `VAL-*`, `RISK-*`, `DEC-*`, `SRC-*` only when needed.
10. **Build traceability.** Every mandatory `R-*` must have at least one `AC-*`.
11. **Run QA.** Read `references/quality-gates.md` and fix issues before returning the contract.
12. **Return a neutral contract.** Do not embed a specific agent or framework workflow.

## Core rules

- Requirements describe **WHAT**, not **HOW**, unless implementation is explicitly mandated.
- Never turn a plausible guess into a requirement or confirmed fact.
- Never invent missing business decisions.
- Technical uncertainty alone does not make the contract `BLOCKED` if the next engineering stage can investigate it.
- If a technical question can be investigated later, preserve it as `INV-*` instead of asking the user by default.
- `NG-*` means intentionally out of scope.
- `PR-*` means existing behavior that must keep working.
- Preserve exact text, values, and explicit business decisions when exactness matters.
- If a later decision clearly replaces an earlier one, use the final decision and keep the rejection rationale when useful.
- If conflicting sources cannot be resolved, expose the conflict or create `Q-*`; do not choose silently.
- Do not tailor the contract itself to OpenSpec, Codex, Claude Code, Cursor, OpenCode, or another downstream workflow.

## Output

Use `references/contract-format.md` and `assets/requirements-handoff-template.md`.

Contract status:
- `DRAFT`: normalization is not complete;
- `BLOCKED`: a missing business decision prevents unambiguous required behavior;
- `READY`: the business contract is sufficient for the next engineering stage.

`READY` does not mean implementation can start immediately. It means the downstream consumer can begin research, proposal, design, or planning.

Return the contract in the user's language unless they request another language. If the user asks for a file, create a Markdown contract.

## Handoff neutrality

The final contract must not require:
- OpenSpec or `/opsx propose`;
- a specific Plan Mode;
- `design.md`;
- a specific agent loop;
- specific coding-agent commands;
- a tool-specific implementation report.

The next stage must preserve requirements, scope, invariants, constraints, exact values, and verification intent, but it chooses its own engineering workflow.

## References

Before finishing, read `references/quality-gates.md`.

Use:
- `references/contract-format.md` for section semantics and IDs;
- `references/normalization-rules.md` for converting human prose;
- `examples/example-payment-warning.md` as a quality example when useful.
