# Project Workflow Template

A lightweight, stage-based workflow for building software one work item at a time.
Two files drive everything:

| File | Scope | When |
| --- | --- | --- |
| `project.md` | Whole codebase | Filled once at project start (or scanned from an existing repo) |
| `status.md` | One work item | Copied per branch; walks a Track — FULL (INIT → PLAN → IMPLEMENTATION → VERIFICATION) or LIGHT (INIT → IMPLEMENTATION → VERIFICATION) |

Works for any project type: web, desktop (Windows/macOS/Linux), mobile (Android/iOS), CLI, library, backend, or embedded.

---

## Two flows

### 1. Whole new project

1. Create the project, then fill in `project.md`: Final Target, Architecture, Roadmap (give each roadmap item a one-line Definition of Done).
2. `project.md` is read **once** to initialize; after that it is ignored during branch work and only revisited on `report` from `main`/`master`, or when you ask to modify it.

### 2. Existing project (e.g. OpenBMC, Linux kernel)

1. Copy the template in, then run `init` — it scans the codebase (languages, frameworks, structure, build files) and drafts the empty fields for your confirmation.
2. Fill Final Target and Roadmap yourself (a scan can't invent those).

---

## Is `project.md` defined?

`project.md` carries an **Init Status** marker (`TEMPLATE` or `DEFINED`), so the check is a one-liner:

```bash
PROJECT_FILE="docs/project.md"
[ -f "$PROJECT_FILE" ] || PROJECT_FILE="project.md"

if [ -f "$PROJECT_FILE" ] && grep -q '^Status: DEFINED' "$PROJECT_FILE"; then
  echo "defined"
else
  echo "not defined"
fi
```

---

## Per work item (single branch)

1. Create a branch: `<type>/<short-name>` (type = `feature` / `fix` / `chore` / `docs`).
2. Copy `status.md` into your workflow directory (`docs/` by default) and run `goto init` to reset it.
3. Pick a **Track**: FULL for large/risky items (full PLAN pipeline), LIGHT for small/clear ones (skips PLAN).
4. Progress through the stages with `goto next stage`.
  - If `goto next stage` succeeds, the next stage starts immediately in the same turn.
  - If Exit Criteria are not met, stage does not change and missing checklist items are listed.
  - You can still use explicit `goto plan|implementation|verification` to move back for rework; these commands change stage only and do not auto-start work.
5. Deliver: `open pr` (if your Delivery Policy requires a PR — always confirmed before opening; updates `project.md`, docs, and `README.md`, then commits before opening), then merge, then `finish`.

---

## Stage command semantics

- `goto next stage`: guarded transition. Requires current-stage Exit Criteria; auto-starts the entered stage.
- `goto plan|implementation|verification`: explicit stage navigation (including rework moves). No Exit Criteria gate; no auto-start.
- On manual stage navigation, record a one-line reason in `Next Action`.
- Stage changes do not auto-check or auto-uncheck checklist items. Only `goto init` resets checklist state.

---

## Where to put the files

- Small/new project: `docs/`
- Large existing repo (kernel, OpenBMC): a dedicated folder like `.workflow/` to avoid clashing with the project's own `docs/` or `Documentation/`. Add it to `.gitignore` if you don't intend to upstream it.

On the FULL track, the PLAN stage's Spec and Tasks outputs land together in `<workflow-dir>/workitems/<name>.md` (usually `docs/workitems/<name>.md`). The LIGHT track skips it — status.md holds the whole trail.

---

## Using this repo

This is a **template repository** — click **Use this template** (or copy `project.md` + `status.md`) into your project on a new branch.
In this template repo, workflow files are at the repository root (`project.md`, `status.md`, `workitems/`).
In a target project, place them under `docs/` (or `.workflow/` for very large existing repos).
This README describes the template workflow itself. In a new project created from this template, the project README is expected to be rewritten to describe that project's product and milestones.
See each file's own **Commands** and **AI Instructions** sections for the full command set.
