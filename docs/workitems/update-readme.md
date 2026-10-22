# Update README Workflow

Use this workflow when you want to refresh project README content from the current repository state.

## Role

Act as a senior software architect and technical writer.

## Goal

- Keep README accurate and synchronized with the codebase structure and available commands.
- Produce onboarding-ready documentation for new developers.

## Required Sequence

1. Identify the README scope to refresh (template workflow, product docs, or both).
2. Scan repository evidence relevant to that scope and collect current structure/command sources.
3. Update README sections that are stale or missing.
4. Verify links and command descriptions against source documents using explicit checks.
5. Follow the Delivery Policy in [project.md](../project.md) before landing.

## Scope Rule

- Prefer surgical edits to existing README sections.
- Do not invent product capabilities that are not present in the repository.
- Keep wording aligned with canonical sources in [docs/project.md](../project.md) and [docs/status.md](../status.md).
- Use source code and executable project artifacts as the source of truth.
- Treat existing README content as potentially stale; keep only statements verified from repository evidence.
- In the refreshed README, prefer a conversational and onboarding-friendly tone (clear, direct, human-readable) while preserving technical accuracy.
- Conversational-tone requirement applies to `README.md` only. Keep technical workflow/spec documents (`project.md`, `status.md`, `docs/prd/*.md`, `docs/workitems/*.md`) precise and formal.

## Repository Audit Requirements

Perform a documentation audit for the selected refresh scope and:

- detect major workflows automatically;
- infer setup instructions from build scripts, package manager files, Dockerfiles, CI pipelines, and configuration files;
- extract public APIs, CLI commands, environment variables, and configuration options;
- refresh README content as a professional onboarding document without unverified claims.

## Update Checklist

### 1) Define Refresh Target

- Confirm which README file to update (`README.md` by default).
- Record intended sections to update (commands, structure, workflow, examples).
- Capture a baseline snapshot of the current README sections being updated.
- Record non-goals for this pass to prevent scope drift.

### 2) Scan Current Repository State

- Confirm actual directories and key docs currently present.
- Confirm active command set from [project.md](../project.md).
- Confirm stage semantics and delivery flow from [status.md](../status.md).
- Detect build, test, lint, and release workflows from automation/config files.
- Extract setup and runtime requirements from package/dependency manifests and scripts.
- Inventory user-facing commands, APIs, environment variables, and config knobs.
- If evidence is missing or ambiguous, mark the item explicitly instead of inferring behavior.

### 3) Apply README Updates

- Add missing sections required by current repo structure.
- Remove stale or misleading statements.
- Keep command and workflow descriptions concise and consistent.
- Rewrite rigid or overly formal README phrasing into a more conversational style when it improves clarity.
- Preserve existing valid content not related to the refresh target.
- Keep every added statement traceable to repository evidence.

### 4) Verify

- Check all updated links resolve.
- Check command descriptions match canonical command docs.
- Re-read only touched sections for consistency and duplication.
- Record exact verification commands/manual checks and pass/fail outcomes.

### 5) Deliver

- Include README updates in delivery commit(s) with related docs when applicable.
- Follow Delivery Policy from [project.md](../project.md) for commit/PR/merge rules.

## Completion Definition

README refresh is done when:

- Updated sections reflect the current repository state.
- Command and workflow descriptions align with canonical docs.
- All updated links are valid.
- Setup instructions are inferred from real project automation/configuration assets.
- In-scope APIs, CLI commands, env vars, and config options are documented (or explicitly marked none found).
- Delivery is completed per policy.

## Standard Output Template (Use for `update readme`)

Use this response structure when reporting a README refresh:

```md
# Documentation Audit and README Refresh Report

## 1) Documentation Gap Analysis
- Gaps found:
- Outdated/incorrect content detected:
- Evidence sources:

## 2) Missing Sections
- Missing section 1:
- Missing section 2:
- Priority order:

## 3) Updated README.md
- Target README:
- Sections updated:
- Sources used:

## Repository Scan Summary
- Current structure notes:
- Command-set notes:
- Workflow-pack notes:
- Build/setup inference notes:
- API/CLI/env/config extraction notes:

## Changes Applied
1. <Section or topic>
   - What changed:
   - Why:
   - Source alignment:

## Verification
- Link checks (exact command/manual check):
- Command consistency checks (exact command/manual check):
- Result (pass/fail):

## 4) Suggested Improvements
- Improvement 1:
- Improvement 2:

## Final Notes
- Assumptions/unknowns:
- Follow-ups (if any):
```
