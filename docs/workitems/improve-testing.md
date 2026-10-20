# Improve Testing Workflow

Use this workflow when you want a dedicated pass to check current test quality and improve it.

## Goal

- Raise confidence in existing behavior by improving test coverage and test quality.
- Run the review with senior-level SDET and software architecture rigor.

## Review Role

Act as a senior SDET and software architect.

## Required Sequence

1. Open a new branch for the testing-improvement item.
2. Execute this testing workflow.
3. Follow the Delivery Policy in [project.md](../project.md) before landing.

## Branch Rule

- Use `chore/test-<short-name>` by default.
- Keep one testing-improvement scope per branch.

## Testing Improvement Checklist

### 1) Define Scope

- Pick a concrete target area (module, flow, or feature slice).
- State expected behavior to protect and non-goals to avoid scope drift.

### 2) Check Existing Tests

- Analyze the implementation and existing tests for the target area.
- Review all of the following dimensions:
  1. Test Coverage
  2. Branch Coverage
  3. Edge Cases
  4. Error Handling
  5. Regression Risks
  6. Security Risks
  7. Performance Risks
  8. Configuration Risks
- Identify missing behavior cases (happy path, validation, boundary, error path, idempotency if relevant).
- Identify weak assertions coupled to implementation details.

### 3) Improve Tests

- Add or update tests to cover missing observable behavior.
- Strengthen assertions to validate outputs/state rather than internals.
- Remove flaky patterns and stabilize fixtures/data setup.
- Keep naming behavior-focused and readable.

### 4) Verify

- Run targeted tests for touched areas.
- Run broader related suite to detect regressions.
- Run lint/format checks for test files if configured.

### 5) Deliver

- Update related docs when test strategy or usage guidance changes.
- Follow Delivery Policy from [project.md](../project.md) for commit/PR/merge rules.

## Completion Definition

Testing improvement is done when:

- Scope goals are met.
- Missing/weak test cases in scope are addressed.
- Required verification is green.
- Delivery is completed per policy.

## Missing Test Reporting Requirements

Identify all missing tests found in scope.

For each missing test, provide:

- Risk Level
- Why it matters
- Example test case
- Example test code

Prioritize findings by business impact.

## Standard Output Template (Use for `improve testing <short-name>`)

Use this response structure when reporting results:

```md
# Testing Improvement Review: <short-name>

## Scope
- Target area(s):
- Non-goals:
- Baseline verification used:

## Review Dimensions
- Test Coverage:
- Branch Coverage:
- Edge Cases:
- Error Handling:
- Regression Risks:
- Security Risks:
- Performance Risks:
- Configuration Risks:

## Missing Tests (Prioritized by Business Impact)
1. <Missing test title>
   - Risk level:
   - Business impact:
   - Why it matters:
   - Example test case:
   - Example test code:
     ```<lang>
     <test code>
     ```

## Recommended Execution Order
1. <Highest-impact test to implement first>
2. <Next>

## Verification
- Tests run:
- Lint/format run:
- Result:
- Regressions found:
```
