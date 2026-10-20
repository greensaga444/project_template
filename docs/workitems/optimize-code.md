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

### 2) Preserve Behavior

- Keep current observable behavior unless a behavior change is explicitly requested.
- Add/update tests before refactors when risk is non-trivial.

### 3) Implement Optimization

- Remove duplication and simplify control flow.
- Improve naming, structure, and maintainability.
- Apply performance improvements only where measurable or clearly justified.
- Remove redundant code.
- Eliminate duplicated logic.
- Minimize code size where possible without reducing readability.
- Consolidate similar methods into reusable utilities.
- Remove dead code and unused variables.
- Simplify nested `if/else` statements.
- Follow clean code principles (clear naming, single responsibility, readable flow).
- Preserve all existing functionality.
- Do not introduce unnecessary abstractions.

### 4) Verify

- Run targeted tests for touched areas.
- Run lint/format checks if configured.
- Confirm no regressions in expected outputs.

### 5) Deliver

- Update related docs when behavior, API, or usage changes.
- Follow Delivery Policy from [project.md](../project.md) for commit/PR/merge rules.

## Completion Definition

Optimization is done when:

- Scope goals are met.
- Existing behavior is preserved (or intentionally changed and documented).
- Required verification is green.
- Delivery is completed per policy.

## Full Refactoring Review Requirement

When running this workflow as a **full refactoring review**, perform a project-wide audit and implementation pass aligned with the checklist above.

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
- Tests run:
- Lint/format run:
- Result:
- Regressions found:

## Final Notes
- Constraints/tradeoffs:
- Follow-up opportunities (optional):
```
