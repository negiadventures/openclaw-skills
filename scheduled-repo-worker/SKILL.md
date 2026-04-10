---
name: scheduled-repo-worker
description: Bootstrap and maintain recurring repo automation for coding or content projects that should make bounded progress on a schedule, update repo-local project state, create PRs on designated runs, and post summaries to Discord. Use when setting up or improving scheduled autonomous work for a repository, especially when the repo needs cron-driven coding or content updates, PR packaging runs, branch-from-main discipline, repo memory files, task-engine integration, or Discord delivery. Supports project-memory mode, task-engine mode, and hybrid mode.
---

# Scheduled Repo Worker

Set up recurring repo automation that makes real progress, maintains repo-local state, packages coherent PRs on designated runs, and posts summaries to Discord.

## Required outcome

After using this skill, the repo should have:
- a clear scheduled-work operating model
- repo-local memory/state files appropriate to the mode
- normal-run and PR-run prompt files
- branch/PR rules that sync from updated main before packaging
- OpenClaw cron jobs wired to the correct Discord target
- a clear first next step for future runs

## Modes

Choose one mode before creating files.

### 1. project-memory
Use for open-ended product repos that do not already have a task engine.

Create and maintain:
- `docs/WORK_STATE.md`
- `docs/NEXT_ACTIONS.md`
- `docs/PROJECT_LOG.md`

### 2. task-engine
Use for repos that already have a machine-readable task/queue/state workflow.

Examples:
- `state.json`
- `queue.json`
- `NEXT_TASK.md`
- `RUN_LOG.md`
- task files in a plan/tasks directory

### 3. hybrid
Use when the repo has a task engine but also needs higher-level project memory and handoff.

Create/use both task-engine files and JobPilot-style memory files.

## Inputs to collect

Ask for these before making changes.

### Required
- repo path
- project goal
- mode (`project-memory`, `task-engine`, or `hybrid`)
- timezone
- Discord target (channel ID or Discord URL)
- normal run times
- PR run time(s)

### Optional but useful
- repo URL
- default branch (default `main`)
- quality priorities
- design priorities
- scalability goals
- whether docs-only PRs should be skipped (default yes)
- preferred branch prefix
- timeout seconds

If the user does not know the schedule, offer defaults from `references/question-flow.md`.

## Discord target handling

Accept either:
- raw channel ID
- full Discord URL like `https://discord.com/channels/<guild>/<channel>`

Extract the final channel ID for cron configuration.

## Branch / PR policy

Always encode this in PR-run guidance:
1. return to the default branch first
2. pull latest default branch with fast-forward only
3. create a fresh branch from updated default branch
4. do not stack on old PR branches
5. create PR only if the work is meaningful and reviewable
6. skip PR if only docs/status churn exists
7. if no PR is created, explain why clearly

Preferred example commands:
- `git checkout main`
- `git pull --ff-only origin main`

If the repo uses `master`, adapt accordingly.

## What to generate

### For project-memory mode
Create:
- `docs/WORK_STATE.md`
- `docs/NEXT_ACTIONS.md`
- `docs/PROJECT_LOG.md`
- normal-run cron prompt
- PR-run cron prompt

Use the templates in `references/project-memory-templates.md`.

### For task-engine mode
Inspect the existing task engine and align prompts to it.

Read and respect:
- queue/state files
- next-task file
- run log
- task specs

Create:
- normal-run cron prompt
- PR-run cron prompt

Use `references/task-engine-notes.md`.

### For hybrid mode
Do both:
- preserve and use the task engine
- add `docs/WORK_STATE.md`
- add `docs/NEXT_ACTIONS.md`
- add `docs/PROJECT_LOG.md`

## Prompt-writing rules

### Normal-run prompt
Require the run to:
- read the relevant state files in the correct order
- pull latest default branch first
- choose one bounded, meaningful improvement
- prefer real product progress over status-only churn
- update repo-local state after meaningful work
- run relevant checks/tests where practical
- return a Discord-friendly summary

### PR-run prompt
Require the run to:
- read the relevant state files in the correct order
- sync updated default branch first
- review whether there is coherent work to package
- create a fresh PR branch if warranted
- avoid stale carry-over branch packaging
- skip docs-only PRs
- return a Discord-friendly PR-or-no-PR summary

## Quality rules

Do not set up automations that:
- repeatedly open fluff PRs
- rewrite status docs without implementation movement
- operate from stale PR branches
- ignore the repo’s existing task system
- post to the wrong Discord channel

Prefer:
- bounded progress
- clear handoff
- strong branch discipline
- real code/content/design progress
- repo-local memory that accumulates value

## Cron creation

Use OpenClaw cron, not system cron.

For each configured run:
- name it clearly
- set timezone
- use isolated session unless there is a strong reason otherwise
- announce to the correct Discord channel
- set an explicit timeout

Use the repo’s prompts as the message payload.

## Read these references when needed
- `references/question-flow.md` for the question flow and defaults
- `references/project-memory-templates.md` for state-file templates
- `references/task-engine-notes.md` for adapting the skill to existing task systems

## Final response format

After setup, report:
- mode used
- files created/updated
- cron names
- cron IDs
- Discord target
- branch/PR policy
- recommended first implementation task
