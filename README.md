# Project Workflow Template

A lightweight, stage-based workflow for shipping one work item per branch.

## Core Files

| File | Scope | Purpose |
| --- | --- | --- |
| `docs/project.md` | Whole codebase | One-time project definition: target, architecture, roadmap, milestones |
| `docs/status.md` | Single branch / work item | Day-to-day execution through INIT/PLAN/IMPLEMENTATION/VERIFICATION/DELIVERY |

Works for web, desktop, mobile, CLI, libraries, backend services, and embedded projects.

---

## Startup Modes

### New Project

1. Fill `docs/project.md` (Final Target, Architecture, Roadmap, Milestones).
2. Set `Status: DEFINED` only after content is reviewed and approved.

### Existing Project

1. Copy this template into the repo.
2. Run `init` to scan languages/frameworks/layout and draft fields.
3. Fill Final Target and Roadmap manually (the scan cannot infer business goals).

---

## Is Project Defined?

Use `Init Status` in `project.md` (`TEMPLATE` or `DEFINED`):

```bash
PROJECT_FILE="docs/project.md"
[ -f "$PROJECT_FILE" ] || PROJECT_FILE=".workflow/project.md"
[ -f "$PROJECT_FILE" ] || PROJECT_FILE="project.md"

if [ -f "$PROJECT_FILE" ] && grep -q '^Status: DEFINED' "$PROJECT_FILE"; then
  echo "defined"
else
  echo "not defined"
fi
```

---

## Per-Branch Workflow

1. Create branch: `<type>/<short-name>` (`feature|fix|chore|docs`).
2. Prepare `docs/status.md`, then run `goto init`.
3. Choose track:
   - FULL: INIT -> PLAN -> IMPLEMENTATION -> VERIFICATION
   - LIGHT: INIT -> IMPLEMENTATION -> VERIFICATION
4. Move forward with `goto next stage` (guarded by exit criteria).
5. After IMPLEMENTATION and VERIFICATION are complete, run Delivery:
   - Update docs (`docs/project.md`, other docs, `README.md`) as needed.
   - Commit delivery updates.
   - Apply branch policy:
     - If main is protected (therefore PR is required): run `open pr` (one PR per branch; reuse existing PR).
     - If main is not protected (therefore PR is not required): push the delivery commit directly to `main`.
   - Merge (if needed), then `finish`.

---

## Stage Command Semantics

- `goto next stage`: guarded transition; auto-starts entered stage.
- `goto plan|implementation|verification`: explicit navigation; no guard; no auto-start.
- Manual stage change must record a one-line reason in `Next Action`.
- Only `goto init` resets checklist items.

---

## File Location

- Small/new projects: keep workflow files in `docs/`.
- Large existing repos: use `.workflow/` to avoid conflicts.

On FULL track, PLAN output goes to `<workflow-dir>/workitems/<name>.md`.

---

## Template Notes

- This repository is a template; copy or use it as a starting point.
- In target projects, keep canonical workflow files under `docs/` (or `.workflow/` for large repos).
- This README describes workflow mechanics; target-project README should describe that project's product.
- See `docs/project.md` and `docs/status.md` for complete command behavior and AI rules.
