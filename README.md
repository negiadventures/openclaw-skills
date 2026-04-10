# openclaw-skills

Reusable OpenClaw skills, organized around the OpenClaw skills guide: <https://docs.openclaw.ai/tools/skills>.

## Skill layout

Each skill lives in its own top-level directory:

```text
openclaw-skills/
└── <skill-name>/
    ├── SKILL.md
    └── references/   (optional)
```

## `SKILL.md` requirements

Each skill must have a `SKILL.md` file with frontmatter:

```yaml
---
name: your-skill-name
description: When to use this skill and what result it drives.
---
```

Naming note: keep `name` stable and unique; prefer matching the folder name (for example, `my-new-skill`).

Recommended body sections:

- required outcome
- inputs to collect
- execution rules / workflow
- quality and safety rules
- final response format

Guidance:

- Keep instructions explicit, bounded, and action-oriented.
- Prefer checklists and clear decision rules over vague prose.
- Define “done” so runs can terminate reliably.
- Reference helper docs using relative paths.

## Optional `references/` folder

Use `references/` for reusable artifacts:

- templates
- decision trees / question flows
- integration notes

Keep durable guidance in references and task-driving instructions in `SKILL.md`.

## Add a new skill

1. Create a folder at repo root (example: `my-new-skill/`).
2. Add `my-new-skill/SKILL.md` with `name` and `description` frontmatter.
3. Add the core sections listed above.
4. Add `my-new-skill/references/` if reusable support docs are needed.
5. Link reference files from `SKILL.md` with relative paths.

## Use a skill in OpenClaw

Invoke the skill by its frontmatter `name` and provide all required inputs defined in `SKILL.md`.

## Repository example

`scheduled-repo-worker/` is the canonical example in this repo:

- `scheduled-repo-worker/SKILL.md`
- `scheduled-repo-worker/references/question-flow.md`
- `scheduled-repo-worker/references/project-memory-templates.md`
- `scheduled-repo-worker/references/task-engine-notes.md`
