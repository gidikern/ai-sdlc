# AI-SDLC Framework

This project IS the AI-native Software Development Lifecycle framework. These instructions guide development of the framework itself.

## Project Purpose

Provide reusable AI agent skills, workflows, and commands that other projects inherit via relative paths.

## Architecture

```
ai-sdlc/
├── skills/           # Agent definitions (Product Manager, Architect, etc.)
├── workflows/        # Multi-phase processes
├── projects/         # Child projects (gitignored) - inherit via ../../skills/
├── .claude/
│   ├── settings.json
│   ├── siblings.json # Tracks projects for skill sync on release
│   └── commands/     # CLI commands for skill development
└── templates/        # Scaffolding for child projects
```

## Project Management

### Creating Projects

All projects live under `projects/` (gitignored). Each project:
- Has its own git repo and GitHub remote
- Inherits skills/workflows from parent via relative paths (`../../skills/`)
- Is registered in `.claude/siblings.json`

```bash
/init-project my-startup
# Creates: projects/my-startup/ with structure and GitHub repo
# Registers in siblings.json for skill sync
```

### Syncing to Projects

After adding new skills, commands, or workflows:
1. Commit and push to GitHub
2. Run `/release v1.x.x` to tag the release
3. `/release` will check each project for missing/updated items and ask to sync:
   - Skills (updates `.claude/settings.json`)
   - Workflow commands (copies to `.claude/commands/`)
   - Workflows (copies to `.claude/workflows/`)
4. Framework commands (`/init-project`, `/release`, etc.) stay in parent only

### siblings.json

Controls which projects get checked for sync on release:

```json
{
  "projects": [
    { "path": "./projects/my-startup", "autoUpdate": true },
    { "path": "./projects/experimental", "autoUpdate": false }
  ]
}
```

- `autoUpdate: true` = Check for missing items during `/release` and ask to sync
- `autoUpdate: false` = Skip this project during release
- Sync is cumulative: checks for ALL missing items, not just new ones

## Development Guidelines

### Modifying Skills

1. Skills are in `skills/<name>/SKILL.md`
2. Keep SKILL.md under 500 lines - use `references/` for details
3. Test changes on a real project before committing
4. Update CHANGELOG.md
5. Run `/validate-skill` to check structure

### Creating New Skills

Use command: `/new-skill <name>`

This will:
1. Create `skills/<name>/SKILL.md` with template
2. Create `skills/<name>/references/` directory
3. Remind you to register in both settings files

After creation, you must:
1. Fill in SKILL.md content
2. Add to `.claude/settings.json`
3. Add to `templates/child-project/.claude/settings.json.template`
4. Update CHANGELOG.md
5. Update README.md (agents table)

### Creating Commands

Commands go in `.claude/commands/<name>.md`:

```markdown
# /command-name

Description of what this command does.

## Usage
/command-name <args>

## Behavior
[Instructions for Claude when command is invoked]
```

### Versioning

We use semantic versioning with git tags:

- **MAJOR** (v2.0.0): Breaking changes to skill interfaces
- **MINOR** (v1.1.0): New skills, workflows, or backward-compatible changes
- **PATCH** (v1.0.1): Bug fixes, documentation updates

To release:
```bash
# 1. Prepare CHANGELOG (review commits, update [Unreleased])
/prepare-release

# 2. Create release (moves [Unreleased] to version, tags, pushes, updates projects)
/release v1.x.x
```

### Quality Checklist

Before committing skill changes:
- [ ] SKILL.md has valid frontmatter (name, description)
- [ ] Description clearly states when to trigger
- [ ] Instructions are actionable, not vague
- [ ] References exist for detailed content
- [ ] Tested on real project usage
- [ ] Registered in both settings files
- [ ] CHANGELOG.md updated
- [ ] README.md agents table updated (if new skill)

## Commands

| Command | Purpose |
|---------|---------|
| `/new-skill <name>` | Scaffold a new skill |
| `/validate-skill <path>` | Check skill structure and quality |
| `/prepare-release` | Review commits and update CHANGELOG [Unreleased] |
| `/release <version>` | Create release and sync skills to projects |
| `/init-project <name>` | Create new project under projects/ |

## Documentation Responsibilities

| File | Updated By | When |
|------|------------|------|
| `CHANGELOG.md` | `/prepare-release` | Before every release |
| `README.md` | Manual | New skills, workflow changes |
| `CLAUDE.md` | Manual | Framework structure changes |
| `.claude/settings.json` | `/new-skill` reminder | New skills |
| `templates/.../settings.json.template` | `/new-skill` reminder | New skills |
| `.claude/siblings.json` | `/init-project` | New projects |
