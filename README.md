# openclaw-skills

This repository contains reusable OpenClaw skills.  
Each skill is stored in its own folder and documented in a `SKILL.md` file.

## Project structure

```text
openclaw-skills/
└── scheduled-repo-worker/
    ├── SKILL.md
    └── references/
        ├── project-memory-templates.md
        ├── question-flow.md
        └── task-engine-notes.md
```

## What a skill contains

At minimum, a skill folder should include:

- `SKILL.md`: Frontmatter + full instructions for the skill.
- `references/` (optional but recommended): Supporting templates, decision guides, and notes referenced by the skill.

## How to create a new OpenClaw skill

1. Create a new folder at the repository root (example: `my-new-skill/`).
2. Add `my-new-skill/SKILL.md`.
3. Add frontmatter at the top of `SKILL.md`:
   - `name`: unique skill name
   - `description`: when and why to use the skill
4. Write clear sections in `SKILL.md`, for example:
   - required outcome
   - inputs to collect
   - execution rules
   - quality/safety rules
   - final response format
5. If the skill needs reusable guidance, create `my-new-skill/references/` and put helper docs there.
6. In `SKILL.md`, reference those helper docs with relative paths.
7. Keep instructions actionable, bounded, and focused on producing meaningful work.

## Example: existing skill in this repo

The `scheduled-repo-worker` skill shows a complete structure:

- `scheduled-repo-worker/SKILL.md` defines modes (`project-memory`, `task-engine`, `hybrid`), required inputs, branch/PR policy, cron setup, and output format.
- `scheduled-repo-worker/references/question-flow.md` helps collect missing user inputs.
- `scheduled-repo-worker/references/project-memory-templates.md` provides templates for state files.
- `scheduled-repo-worker/references/task-engine-notes.md` explains how to integrate with existing task systems.

## How to use a skill in OpenClaw

When running OpenClaw, invoke the skill by name and provide context the skill requires.

### Example 1: use the existing `scheduled-repo-worker` skill

Use this when you want cron-based repo automation with Discord summaries:

- repo path or URL
- project goal
- mode (`project-memory`, `task-engine`, or `hybrid`)
- timezone
- normal run schedule
- PR run schedule
- Discord channel target

Expected result: OpenClaw prepares the right project state files/prompts and configures scheduled runs with clear PR behavior.

### Example 2: use your new skill

After creating `my-new-skill/SKILL.md`, call it in OpenClaw by its `name` from frontmatter and pass the required inputs you defined in that file.

## Authoring tips

- Keep one skill per folder.
- Prefer explicit checklists over vague guidance.
- Include references/templates when the workflow has repeated structure.
- Define what “done” looks like in the required outcome section.
