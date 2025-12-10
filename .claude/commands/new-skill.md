# /new-skill

Create a new skill in the ai-sdlc framework.

## Usage
```
/new-skill <skill-name>
```

## Behavior

When invoked, create the following structure:

```
skills/<skill-name>/
├── SKILL.md
└── references/
    └── .gitkeep
```

### SKILL.md Template

```markdown
---
name: <skill-name>
description: [TODO: Describe what this skill does and when it should trigger. Be specific about trigger phrases and use cases.]
---

# [Skill Name] Agent

## Role

Act as an experienced [role] who excels at:
- [Capability 1]
- [Capability 2]
- [Capability 3]

## Core Workflow

1. **[Phase 1]** → [Description]
2. **[Phase 2]** → [Description]
3. **[Phase 3]** → [Description]

## Behaviors

### When [Trigger Condition 1]

[Instructions for this scenario]

### When [Trigger Condition 2]

[Instructions for this scenario]

## Output Artifacts

| Artifact | File | Purpose |
|----------|------|---------|
| [Name] | `path/to/file` | [Purpose] |

## Handoff

When complete:

\`\`\`markdown
## [Next Agent] Handoff

**Deliverables**: [list]
**Key Notes**: [notes]

Ready for [next phase].
\`\`\`

## Interaction Style

- [Style guideline 1]
- [Style guideline 2]
```

## After Creation

### Register the Skill

Add the new skill to both settings files:

1. **`.claude/settings.json`** (ai-sdlc's own settings):
```json
{ "path": "./skills/<skill-name>" }
```

2. **`templates/child-project/.claude/settings.json.template`** (for new projects):
```json
{ "path": "./ai-sdlc/skills/<skill-name>" }
```

### Update Documentation

After registering the skill, update these files:

3. **`CHANGELOG.md`** - Add entry under `[Unreleased]` → `Added`:
```markdown
- **[Skill Name] skill** for [purpose]
  - [Key feature 1]
  - [Key feature 2]
```

4. **`README.md`** - Add to the Agents table:
```markdown
| **[Skill Name]** | [Role description] | [Focus areas] |
```

### Remind the User

1. Fill in the TODO sections in SKILL.md
2. Add references if needed
3. Test the skill on a real project
4. Verify all documentation is updated:
   - [ ] `.claude/settings.json`
   - [ ] `templates/child-project/.claude/settings.json.template`
   - [ ] `CHANGELOG.md`
   - [ ] `README.md` agents table
5. Run `/validate-skill skills/<skill-name>` to verify structure
