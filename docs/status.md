# PROJECT STATUS

> Use this file for a **single work item** (feature, fix, chore, docs) on its own branch.
> Place it in your workflow directory (`<workflow-dir>/status.md`, usually `docs/status.md`), fill in the Current Work Item, reset the checklist to unchecked, and start at the INIT stage.
> For whole-codebase architecture, target, and roadmap, see `project.md`.

## Project

See `project.md` for Project Name, Repository, and Tech Stack.
(For a standalone task with no `project.md`, fill those in here instead.)

---

## Current Work Item

Work Item Name: TBD

Description: TBD

---

## Track

FULL

Tracks:

- FULL — INIT → PLAN → IMPLEMENTATION → VERIFICATION. Use for large/risky items with real unknowns.
- LIGHT — INIT → IMPLEMENTATION → VERIFICATION (skips the PLAN doc). Use for small, clear items.

Choose LIGHT when scope and design are obvious; FULL when there are unknowns worth writing down.

---

## Current Stage

INIT

Available Stages (depends on Track):

- INIT
- PLAN            (FULL track only)
- IMPLEMENTATION
- VERIFICATION

---

## Stage Definitions

### INIT

Goal:

Set up this task's context before any requirements work.

Output:

Filled header of this file (Project + Current Work Item).

Allowed:

- Confirm Branch
- Set Work Item Name / Description
- Inherit Tech Stack from project.md
- Agree Task Boundary / Scope Line
- Confirm the item's one-line Definition of Done and check it doesn't overlap an earlier item

Not Allowed:

- Requirements / MVP Definition
- Task Planning
- Source Code

Exit Criteria:

- Branch created
- Work Item Name + Description filled
- Tech Stack confirmed
- Scope boundary agreed
- Definition of Done confirmed and overlap with earlier items checked

---

### PLAN

Goal:

Define requirements/MVP and break them into implementable tasks.  (FULL track only — skipped on LIGHT.)

Output:

<workflow-dir>/workitems/<name>.md — "Spec" and "Tasks" sections (`<workflow-dir>` is usually `docs/`; in this template repo it is the repository root)

Allowed:

- Business Goal
- User Story
- MVP
- Scope Definition
- Acceptance Criteria
- Task Breakdown
- Dependencies
- Priorities
- Development Order

Not Allowed:

- Source Code
- Implementation Discussion

Exit Criteria:

- MVP is clearly defined
- Scope is agreed
- Success criteria exist
- Tasks are small, actionable, and can be completed independently

---

### IMPLEMENTATION

Goal:

Build the work item.

Output:

Source Code

Allowed:

- Data / Storage Changes
- Core / Logic Code
- UI / Interface Code
- Tests

Not Allowed:

- New Scope Changes

Exit Criteria:

- All tasks completed
- Code committed
- Tests added

---

### VERIFICATION

Goal:

Confirm implementation matches specification.

Output:

Verification Result

Allowed:

- Testing
- Code Review
- Spec Coverage Check
- Bug Fixes
- Check formatting / linting if the project defines it (formatter, linter, or style config)
- Run CI locally if a CI config exists (see "Local CI" below)

Exit Criteria:

- Implementation matches Spec
- Tests pass
- Formatting/lint clean if the project defines it (run the formatter/linter; fix or auto-format any issues)
- CI passes — if a CI config exists, run it locally and make it green before delivery (required if Delivery Policy in project.md sets CI Required = yes)
- No critical issues remain

#### Local CI

During VERIFICATION, detect and run CI locally before delivery:

1. Detect a CI config (first match wins): `.github/workflows/*.yml`, `.gitlab-ci.yml`, `.circleci/config.yml`, `azure-pipelines.yml`, `Jenkinsfile`, or a documented CI script.
2. If none exists, skip local CI — fall back to the project's own build + test commands and note "no CI config" in the checklist.
3. If one exists, reproduce its jobs locally (lint, build, test) — prefer a runner like `act` for GitHub Actions when available, otherwise run the equivalent commands the workflow invokes.
4. Make it green locally before `open pr`. Fix failures during VERIFICATION; do not defer them to remote CI.

---

## Delivery (after VERIFICATION)

> Not a stage. Runs once VERIFICATION is done.

Precondition: IMPLEMENTATION and VERIFICATION are already complete.

Flow:

1. Update delivery documents as needed: `project.md` progress (Roadmap/Milestones), related docs, and `README.md`.
2. Commit the delivery updates.
3. Apply branch policy:
   - Main Branch Protected = yes: run `open pr` (confirm, then push and open/update PR to main). One PR per branch only.
   - Main Branch Protected = no: skip `open pr`, push committed delivery updates directly.
4. Merge/land per policy.
5. `finish` — switch to main and delete the branch.

---

## Current Checklist

> On the LIGHT track, skip the PLAN section below.

### INIT

- [ ] Branch Created
- [ ] Work Item Name + Description
- [ ] Tech Stack Confirmed
- [ ] Scope Boundary Agreed
- [ ] Definition of Done + Overlap Checked

### PLAN

- [ ] Business Goal
- [ ] User Story
- [ ] MVP Defined
- [ ] Scope Defined
- [ ] Acceptance Criteria
- [ ] Core / Logic Tasks
- [ ] UI / Interface Tasks
- [ ] Data / Storage Tasks
- [ ] Test Tasks

### IMPLEMENTATION

- [ ] Data / Storage Changes
- [ ] Core / Logic Changes
- [ ] UI / Interface Changes
- [ ] Unit Tests

### VERIFICATION

- [ ] Work Item Tested
- [ ] Spec Coverage Verified (on the LIGHT track, verify against the item's Definition of Done)
- [ ] Format / Lint Checked (if the project defines a formatter or linter)
- [ ] CI Passed — run locally if a CI config exists (required if project.md Delivery Policy sets CI Required = yes)

### DELIVERY

- [ ] project.md progress updated (Roadmap/Milestones)
- [ ] Docs/README updated
- [ ] Delivery commit created
- [ ] Delivery updates pushed
- [ ] PR opened (if required by Delivery Policy)
- [ ] Single PR per branch respected (reuse existing PR if present)

---

## Current Task

TBD

> Keep this to 3-4 lines. Detail belongs in `<workflow-dir>/workitems/<name>.md` (`docs/` in target projects; root in this template repo), not here.

---

## Next Action

TBD

---

## AI Instructions

Always read this file first.

Rules:

1. Follow the Current Stage and Track. On the LIGHT track, INIT hands off directly to IMPLEMENTATION — skip PLAN.
2. Confirm the Track during INIT: FULL for items with unknowns, LIGHT for small/clear items. Record it in the Track section.
3. Do not jump to later stages unless the user explicitly issues a `goto <stage>` command.
4. Prefer MVP solutions.
5. Avoid over-engineering.
6. Suggest architecture changes only when absolutely necessary.
7. Focus on completing the current stage before moving forward.
8. Commit at meaningful checkpoints, not every stage: once at PLAN-agreed (FULL track) and once at IMPLEMENTATION-done. Do not create a commit per stage.
9. Keep the Current Task section to 3-4 lines; put detail in `<workflow-dir>/workitems/<name>.md`.
10. On `goto init`, reset this file to its init state: set Track to FULL, Current Stage to INIT, set Work Item Name/Description/Current Task/Next Action to TBD, and uncheck every checklist item.
11. On `open pr` (Main Branch Protected = yes), always show the PR title and description and ask for explicit user confirmation; ensure delivery document updates are done (`project.md`, docs, `README.md`), create a commit if needed, then push and open/update the branch PR. Enforce one PR per branch.
12. On `report`, check the current branch first: on `main` or `master`, report from `project.md`; on any other branch, summarize progress from this file only (current stage + checklist) and do not read `project.md`.
13. During VERIFICATION, if the project defines a formatter or linter, run it (auto-format/fix) before CI. Then detect a CI config and, if one exists, run CI locally and make it green before delivery (see "Local CI"). If none exists, run the project's build + test instead and note "no CI config". Do not defer CI failures to remote CI.
14. On `goto next stage`, advance only when the current stage Exit Criteria are met. If not met, remain in the current stage and list the missing checklist items.
15. If `goto next stage` advances successfully, immediately start the new stage's work in the same turn (do not wait for another user command).
16. For rule 15, "start the new stage's work" means all of the following in the same turn: update Current Stage, set Current Task, set Next Action, and perform at least one stage-allowed action.
17. `goto plan`, `goto implementation`, and `goto verification` are explicit stage-navigation commands (including moving back for rework): they change Current Stage only and do not auto-start work.
18. On `goto plan`, `goto implementation`, or `goto verification`, record a one-line reason in Next Action in the same turn (for traceability).
19. Stage changes do not auto-check or auto-uncheck checklist items. Checklist items change only when explicitly completed/uncompleted by work updates; only `goto init` resets all checklist items.
20. On `finish`, complete branch cleanup; if PR creation was skipped, ensure delivery document updates, a delivery commit, and push are complete first.

### Stage Transition Matrix

| Command | Allowed From | Allowed To | Exit Criteria Required | Auto-Start Work | Notes |
| --- | --- | --- | --- | --- | --- |
| `goto init` | Any stage | INIT | No | No | Resets header fields to TBD and unchecks all checklist items |
| `goto plan` | Any stage on FULL track | PLAN | No (explicit user command) | No | Must record one-line reason in Next Action |
| `goto implementation` | Any stage | IMPLEMENTATION | No (explicit user command) | No | Must record one-line reason in Next Action |
| `goto verification` | Any stage | VERIFICATION | No (explicit user command) | No | Must record one-line reason in Next Action |
| `goto next stage` | Current stage only | Next stage on current track | Yes | Yes | If blocked, stay put and list missing checklist items |

Efficiency (keep credit/token spend low):

- Reuse the shell environment: configure PATH/toolchain once per terminal, or call the project's build script — don't re-emit long environment setup on every command.
- Batch build + test into one command instead of running configure → build → test as separate calls.
- Don't re-run builds or tests that already passed unless the code changed.
- Prefer fewer, larger file reads over many small ranged reads of the same file.
- Persist build/run/test commands and workflow conventions to repo memory once confirmed, so they aren't re-derived each session.

---

## Commands

report   (check branch first: on main/master, report from project.md; on other branches, summarize this work item's progress from status.md only)

set track full | light   (choose the pipeline: FULL = PLAN + IMPLEMENTATION + VERIFICATION, LIGHT = IMPLEMENTATION + VERIFICATION only)

goto init   (reset this file to init state: track=FULL, stage=INIT, header fields=TBD, all checkboxes unchecked)

goto plan   (FULL track only; explicit stage navigation; changes Current Stage only and does not auto-start PLAN work; record one-line reason in Next Action)

goto implementation   (explicit stage navigation; changes Current Stage only and does not auto-start IMPLEMENTATION work; record one-line reason in Next Action)

goto verification   (explicit stage navigation; changes Current Stage only and does not auto-start VERIFICATION work; record one-line reason in Next Action)

goto next stage   (advances along the current Track only when current-stage Exit Criteria are met; otherwise stay in place and report missing checklist items; if advanced, immediately begin the new stage's work; on LIGHT, INIT → IMPLEMENTATION)

run ci   (VERIFICATION: detect a CI config and run it locally until green; if none exists, run the project's build + test instead)

open pr   (after VERIFICATION done: for Main Branch Protected = yes, ensure delivery document updates + commit are complete, then confirm PR title/description, push branch, and open/update the branch PR to main; one PR per branch; requires CI green if project.md sets CI Required = yes)

finish   (switch to main and delete the current branch; if PR is skipped, first ensure delivery document updates + commit + push are complete)

---

## Command Examples

1. `goto next stage` from PLAN, with PLAN Exit Criteria met
   Result: Current Stage becomes IMPLEMENTATION, Current Task and Next Action are updated, and at least one implementation action is performed in the same turn.

2. `goto next stage` from PLAN, with missing PLAN checklist items
   Result: Current Stage stays PLAN, and the missing checklist items are listed.

3. `goto implementation` from VERIFICATION to fix a bug
   Result: Current Stage becomes IMPLEMENTATION only (no auto-start), and Next Action records the one-line reason for moving back.
