# /init-project

Initialize a new project using ai-sdlc framework.

## Usage
```
/init-project <project-name>
```

Example: `/init-project my-startup`

Creates: `./projects/my-startup/` inheriting from parent ai-sdlc directory

## Behavior

### 1. Gather Information

Ask the user:
- Project name (from argument)
- Brief project description
- GitHub repo visibility: Public or Private? (default: Private)

### 2. Capture ai-sdlc Root

```bash
AI_SDLC_ROOT=$(pwd)
```

Determine project location: `$AI_SDLC_ROOT/projects/<project-name>/`

**CRITICAL**: The Bash tool's working directory **persists** between invocations. Capture `AI_SDLC_ROOT` at the beginning and use it in all subsequent commands.

### 3. Create Project Structure

```bash
mkdir -p $AI_SDLC_ROOT/projects/<project-name>/.claude/commands \
         $AI_SDLC_ROOT/projects/<project-name>/.claude/workflows \
         $AI_SDLC_ROOT/projects/<project-name>/.claude/skills \
         $AI_SDLC_ROOT/projects/<project-name>/docs/product/user-stories \
         $AI_SDLC_ROOT/projects/<project-name>/docs/architecture/adr \
         $AI_SDLC_ROOT/projects/<project-name>/docs/legal \
         $AI_SDLC_ROOT/projects/<project-name>/src \
         $AI_SDLC_ROOT/projects/<project-name>/tests
```

### 4. Copy and Customize Templates

Copy from `templates/child-project/`:
- `CLAUDE.md` from `CLAUDE.md.template`
- `.claude/settings.json` from `settings.json.template`
- `README.md` from `README.md.template`

Replace placeholders:
- `{{PROJECT_NAME}}` → project name
- `{{PROJECT_DESCRIPTION}}` → description from user
- `{{DOMAIN_CONTEXT}}` → "To be defined during Discovery"
- `{{TECHNICAL_CONSTRAINTS}}` → "To be defined during Architecture"

### 5. Copy Workflow Commands and Workflows

**Workflow commands** (NOT framework management commands like /init-project, /release, etc.):

```bash
# Copy workflow commands to project
cp $AI_SDLC_ROOT/.claude/commands/cross-functional-discovery.md \
   $AI_SDLC_ROOT/projects/<project-name>/.claude/commands/
```

**Workflow files:**

```bash
# Copy all workflows to project
cp $AI_SDLC_ROOT/workflows/*.md \
   $AI_SDLC_ROOT/projects/<project-name>/.claude/workflows/
```

**Note**: Only workflow commands are copied to projects. Framework management commands (`/init-project`, `/release`, `/new-skill`, `/validate-skill`, `/prepare-release`) remain in the parent directory only.

### 6. Create Placeholder Files

```bash
touch $AI_SDLC_ROOT/projects/<project-name>/.claude/skills/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/docs/product/user-stories/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/docs/architecture/adr/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/docs/legal/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/src/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/tests/.gitkeep
```

### 7. Initialize Git and Create GitHub Repository

```bash
cd $AI_SDLC_ROOT/projects/<project-name> && \
  git init && \
  git add . && \
  git commit -m "chore: initialize project with ai-sdlc framework" && \
  gh repo create <project-name> --<public|private> --source=. --push
```

### 8. Register in siblings.json

Add the new project to `.claude/siblings.json`:

```json
{
  "projects": [
    ...existing...,
    { "path": "./projects/<project-name>", "autoUpdate": true }
  ]
}
```

**Note**: `autoUpdate: true` means `/release` will check for missing skills, commands, and workflows, and ask to sync them.

### 9. Output Summary

```markdown
## Project Created: <project-name>

**Location**: ./projects/<project-name>/
**Framework**: Inherits from parent ai-sdlc directory
**GitHub repo**: <repo-url>
**Registered in**: .claude/siblings.json (autoUpdate: true)

### Structure Created
\`\`\`
projects/<project-name>/
├── .claude/
│   ├── settings.json    ← References ../../skills/
│   ├── commands/        ← Workflow commands (synced from parent)
│   ├── workflows/       ← Workflow files (synced from parent)
│   └── skills/          ← Local overrides
├── docs/
│   ├── product/
│   └── architecture/
├── src/
├── tests/
├── CLAUDE.md
└── README.md
\`\`\`

### Next Steps

1. **Start working**:
   \`\`\`bash
   cd projects/<project-name>
   claude
   \`\`\`

2. **Begin Discovery**:
   > "Let's explore [your product idea]"
```

## Notes

- All projects are created under `./projects/` directory
- Projects are gitignored from ai-sdlc repo
- Each project has its own git repo and GitHub remote (always created)
- Projects inherit skills from parent via relative paths (`../../skills/`)
- Workflow commands and workflows are copied to `.claude/commands/` and `.claude/workflows/`
- Local skill overrides go in `.claude/skills/`
- Projects are registered in siblings.json for automatic sync during releases
- `/release` syncs skills, workflow commands, and workflows to registered projects
- Requires `gh` CLI installed and authenticated (`gh auth login`)
