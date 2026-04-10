# Task Engine Notes

Use this when the repo already has a queue/state/task system.

## What to preserve
- `state.json` or equivalent current-task source of truth
- `queue.json` or dependency graph
- `NEXT_TASK.md`
- `RUN_LOG.md`
- task spec files

## What not to do
- do not replace the task engine with a docs-only workflow
- do not skip ahead arbitrarily unless the repo’s own rules allow it
- do not create status churn that fights the task engine

## Good adaptation pattern
- read the task engine first
- align prompts to the task engine's current-task contract
- add project-memory files only if hybrid mode is chosen or if the user explicitly wants them
- let the PR run package completed or coherent task work from updated main on a fresh branch

## Hybrid recommendation
If the repo has strong task mechanics but weak high-level handoff, add:
- `docs/WORK_STATE.md`
- `docs/NEXT_ACTIONS.md`
- `docs/PROJECT_LOG.md`

This gives the repo both:
- machine-readable task progression
- human-readable project memory
