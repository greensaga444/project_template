# Optimize Code Workflow

Use this workflow when you want to run a dedicated optimization pass with delivery discipline.

## Goal

- Improve existing code quality/performance without changing intended behavior.

## Required Sequence

1. Open a new branch for the optimization item.
2. Execute this optimize workflow.
3. Follow the Delivery Policy in [project.md](../project.md) before landing.

## Branch Rule

- Use `chore/optimize-<short-name>` by default.
- Keep one optimization scope per branch.

## Optimization Checklist

### 1) Define Scope

- Pick a clear target (module, flow, or bottleneck).
- State the non-goals explicitly to avoid scope drift.
- Record a baseline for the chosen scope (tests, key metrics, or other relevant signals).

### 2) Preserve Behavior

- Keep current observable behavior unless a behavior change is explicitly requested.
- Add/update tests before refactors when risk is non-trivial.

### 3) Implement Optimization

- Remove duplication and simplify control flow.
- Improve naming, structure, and maintainability.
- Apply performance improvements only when validated by before/after evidence, or document why direct measurement is not feasible.
- Remove dead code and unused variables.
- Minimize code size only when readability is preserved.
- Reuse existing patterns/utilities and avoid unnecessary abstractions.

Classify optimization scope as one of:

- `cleanup`: readability and maintainability improvements.
- `perf`: runtime, memory, or build-size improvements with measurable impact.

### 4) Verify

- Run targeted tests for touched areas.
- Run lint/format checks if configured.
- Confirm no regressions in expected outputs.
- Record the exact verification commands and results.

### 5) Deliver

- Update related docs when behavior, API, or usage changes.
- Follow Delivery Policy from [project.md](../project.md) for commit/PR/merge rules.
- For high-risk changes, include a rollback or fallback note.

## Completion Definition

Optimization is done when:

- Scope goals are met.
- Existing behavior is preserved (or intentionally changed and documented).
- Required verification is green.
- Delivery is completed per policy.

## Full Refactoring Review Requirement

Run this mode only when explicitly requested as a **full refactoring review**. In this mode, perform a project-wide audit and implementation pass aligned with the checklist above.

### Required Deliverables

1. Refactoring suggestions
2. Before/After examples
3. Expected benefits

### Change Reporting Rule

For every implemented change, include:

- What changed
- Why it changed (rationale)
- How behavior compatibility was preserved

Use concise, code-linked explanations so each change is traceable and reviewable.

## Standard Output Template (Use for `optimize <short-name>`)

Use this response structure when reporting a full refactoring review:

```md
# Refactoring Review: <short-name>

## Scope
- Target area(s):
- Non-goals:
- Baseline verification used:

## Refactoring Suggestions
1. <Suggestion title>
   - Location:
   - Problem:
   - Suggested change:
   - Why:

## Implemented Changes (with Rationale)
1. <Change title>
   - Location:
   - Before:
     ```<lang>
     <before snippet>
     ```
   - After:
     ```<lang>
     <after snippet>
     ```
   - Rationale:
   - Behavior preservation check:

## Before/After Examples
### Example 1: <name>
- Before summary:
- After summary:
- Net effect:

## Expected Benefits
- Maintainability:
- Readability:
- Performance (if applicable):
- Code size reduction (if applicable):
- Risk reduction:

## Verification
- Tests run (exact command):
- Lint/format run (exact command):
- Result (pass/fail):
- Regressions found:

## Final Notes
- Constraints/tradeoffs:
- Follow-up opportunities (optional):
```
