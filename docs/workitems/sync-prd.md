# Sync PRD Workflow

Use this workflow when implementation has drifted and `docs/prd/` must be rewritten to match the current codebase as source of truth.

## Goal

- Regenerate all PRD source files in `docs/prd/` so they can bootstrap an equivalent implementation in a fresh project.
- Remove stale or contradictory product requirements caused by refactors, feature additions, or behavior changes.

## Required Sequence

1. Decide the synchronization scope (full `docs/prd/` by default).
2. Audit current implementation behavior and architecture from source code and executable artifacts.
3. Rewrite all relevant PRD files under `docs/prd/` to reflect current reality.
4. Verify cross-file consistency and traceability.
5. Follow Delivery Policy in [project.md](../project.md) before landing.

## Scope Rule

- Default scope is full refresh of:
  - `docs/prd/00-index.md`
  - `docs/prd/01-master-prd.md`
  - `docs/prd/10-scope-and-goals.md`
  - `docs/prd/20-requirements-functional.md`
  - `docs/prd/30-requirements-nonfunctional.md`
  - `docs/prd/40-user-flows.md`
  - `docs/prd/50-acceptance-criteria.md`
  - `docs/prd/90-open-questions.md`
- Do not leave unresolved `TBD` placeholders for behavior that already exists in code.
- If evidence is missing or ambiguous, record it explicitly in `90-open-questions.md` instead of guessing.

## Sync Checklist

### 1) Capture Ground Truth from Code

- Identify actual user-visible behavior and supported workflows.
- Derive architecture/component boundaries from current code layout.
- Extract configuration, constraints, and operational expectations.
- Collect measurable validation points (tests, benchmarks, checks).

### 2) Rewrite PRD Sources

- Update [01-master-prd.md](../prd/01-master-prd.md) with an accurate executive summary.
- Update [10-scope-and-goals.md](../prd/10-scope-and-goals.md) for real in-scope/out-of-scope boundaries and measurable goals.
- Update [20-requirements-functional.md](../prd/20-requirements-functional.md) with atomic requirements matching implemented behavior.
- Update [30-requirements-nonfunctional.md](../prd/30-requirements-nonfunctional.md) with measurable NFR targets and validation methods.
- Update [40-user-flows.md](../prd/40-user-flows.md) with concrete, testable journey steps.
- Update [50-acceptance-criteria.md](../prd/50-acceptance-criteria.md) so FR/NFR mappings are observable and verifiable.
- Update [90-open-questions.md](../prd/90-open-questions.md) with unresolved gaps and explicit owners/due dates.
- Move all resolved questions/decisions into their owning PRD sections (scope/requirements/flows/acceptance), then remove those closed items from `90-open-questions.md` to keep it short.
- Update [00-index.md](../prd/00-index.md) metadata and navigation if versioning/read-order changed.

### 3) Enforce Traceability

- Every high-priority functional requirement must map to:
  1. at least one user flow, and
  2. at least one acceptance criterion.
- IDs must stay unique/stable (`FR-*`, `NFR-*`, `UF-*`, `AC-*`, `Q-*`).
- Remove contradictory statements between files.
- `90-open-questions.md` should contain only active open/deferred items after sync; closed items belong in owning PRD docs.

### 4) Verify

- Check all intra-PRD links resolve.
- Check requirement/flow/acceptance mapping is complete.
- Check terminology is consistent across all PRD files.
- Record exact verification commands/manual checks and outcomes.

### 5) Deliver

- Include PRD sync changes in delivery commit(s).
- Update command references in [README.md](../../README.md) and [project.md](../project.md) if command behavior changed.
- Follow branch landing policy from [project.md](../project.md).

## Completion Definition

PRD sync is done when:

- `docs/prd/` reflects current implementation behavior and architecture.
- Cross-file traceability is complete and consistent.
- No stale placeholders remain for implemented functionality.
- Verification checks pass.
- Delivery is completed per policy.

## Standard Output Template (Use for `sync prd`)

Use this response structure when reporting results:

```md
# PRD Synchronization Report

## Scope
- Sync mode: Full `docs/prd/` refresh
- Evidence sources:
- Non-goals:

## Code-to-PRD Alignment Summary
- Product summary changes:
- Functional requirement updates:
- Non-functional requirement updates:
- User flow updates:
- Acceptance criteria updates:

## Files Updated
1. docs/prd/00-index.md
2. docs/prd/01-master-prd.md
3. docs/prd/10-scope-and-goals.md
4. docs/prd/20-requirements-functional.md
5. docs/prd/30-requirements-nonfunctional.md
6. docs/prd/40-user-flows.md
7. docs/prd/50-acceptance-criteria.md
8. docs/prd/90-open-questions.md

## Open Gaps
- Gap 1:
- Owner:
- Due date:

## Verification
- Link checks:
- Traceability checks:
- Result (pass/fail):
```
