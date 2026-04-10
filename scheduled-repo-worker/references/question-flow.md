# Question Flow

Use this when the user has not fully specified the setup.

## Minimal flow

Ask for:
1. repo path or repo URL
2. project goal in 1 to 3 sentences
3. mode:
   - project-memory
   - task-engine
   - hybrid
4. schedule preset:
   - light
   - medium
   - custom
5. Discord channel ID or URL
6. special quality priorities

## Schedule presets

### Light
- 9 AM normal
- 3 PM normal
- 9 PM PR

### Medium
- 4 AM normal
- 8 AM normal
- 12 PM normal
- 4 PM PR
- 8 PM normal
- 12 AM normal

### Custom
User provides exact times.

## Explicit template

```text
- Repo path:
- Repo URL (optional):
- Project goal:
- Mode:
- Default branch:
- Timezone:
- Normal run times:
- PR run times:
- Discord target:
- Quality priorities:
- PR policy notes:
- Branch prefix:
- Timeout seconds:
```

## Notes
- Accept Discord URLs and extract the final channel ID.
- If the user is unsure about timing, recommend light first.
- If the repo already has queue/state/task files, suggest task-engine or hybrid.
- If the repo is open-ended and exploratory, suggest project-memory.
