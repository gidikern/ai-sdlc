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

### 5. Create Placeholder Files

```bash
touch $AI_SDLC_ROOT/projects/<project-name>/.claude/commands/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/.claude/skills/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/docs/product/user-stories/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/docs/architecture/adr/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/docs/legal/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/src/.gitkeep \
      $AI_SDLC_ROOT/projects/<project-name>/tests/.gitkeep
```

### 6. Initialize Git and Create GitHub Repository

```bash
cd $AI_SDLC_ROOT/projects/<project-name> && \
  git init && \
  git add . && \
  git commit -m "chore: initialize project with ai-sdlc framework" && \
  gh repo create <project-name> --<public|private> --source=. --push
```

### 7. Register in siblings.json

Add the new project to `.claude/siblings.json`:

```json
{
  "projects": [
    ...existing...,
    { "path": "./projects/<project-name>", "autoUpdate": true }
  ]
}
```

**Note**: `autoUpdate: true` means `/release` will check for missing skills and ask to update this project's settings.json.

### 8. Output Summary

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
│   ├── commands/
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
- Projects inherit skills/workflows from parent via relative paths (`../../skills/`)
- Local skill overrides go in `.claude/skills/`
- Projects are registered in siblings.json for automatic skill sync during releases
- Requires `gh` CLI installed and authenticated (`gh auth login`)
