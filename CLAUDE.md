# AI-SDLC Framework

This project IS the AI-native Software Development Lifecycle framework. These instructions guide development of the framework itself.

## Project Purpose

Provide reusable AI agent skills, workflows, and commands that other projects inherit via git submodule.

## Architecture

```
ai-sdlc/
├── skills/          # Agent definitions (Product Manager, Architect, etc.)
├── workflows/       # Multi-phase processes
├── .claude/
│   ├── settings.json
│   └── commands/    # CLI commands for skill development
└── templates/       # Scaffolding for child projects
```

## When Used as Submodule

Child projects include ai-sdlc as a git submodule and reference its skills:

```json
// child-project/.claude/settings.json
{
  "skills": [
    { "path": "./ai-sdlc/skills/product-manager" },
    { "path": "./ai-sdlc/skills/architect" }
  ]
}
```

**Override behavior**: If child project has `skills/product-manager/SKILL.md`, it fully replaces the base version.

## Development Guidelines

### Modifying Skills

1. Skills are in `skills/<name>/SKILL.md`
2. Keep SKILL.md under 500 lines - use `references/` for details
3. Test changes on a real child project before committing
4. Update CHANGELOG.md

### Creating New Skills

Use command: `/new-skill <name>`

Or manually:
```
skills/<name>/
├── SKILL.md           # Required: frontmatter + instructions
└── references/        # Optional: detailed guides
```

### Creating Commands

Commands go in `.claude/commands/<name>.md`:

```markdown
---
name: command-name
description: What this command does
---

# Command: /command-name

[Instructions for Claude when command is invoked]
```

### Versioning

We use semantic versioning with git tags:

- **MAJOR** (v2.0.0): Breaking changes to skill interfaces
- **MINOR** (v1.1.0): New skills, workflows, or backward-compatible changes  
- **PATCH** (v1.0.1): Bug fixes, documentation updates

To release:
```bash
# Update CHANGELOG.md, then:
git tag v1.x.x
git push origin v1.x.x
```

### Quality Checklist

Before committing skill changes:
- [ ] SKILL.md has valid frontmatter (name, description)
- [ ] Description clearly states when to trigger
- [ ] Instructions are actionable, not vague
- [ ] References exist for detailed content
- [ ] Tested on real project usage

## Commands

- `/new-skill <name>` - Scaffold a new skill
- `/validate-skill <path>` - Check skill structure and quality
- `/release <version>` - Create a new release

## Child Project Template

To create a new project using ai-sdlc:

```bash
# Copy template
cp -r templates/child-project my-project
cd my-project

# Add ai-sdlc as submodule
git init
git submodule add -b v1.0.0 git@github.com:USER/ai-sdlc.git

# Update settings.json paths
# Edit CLAUDE.md for your project

git add .
git commit -m "chore: initial setup with ai-sdlc"
```
