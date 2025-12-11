# /init-project

Initialize a new project using ai-sdlc framework.

## Usage
```
/init-project <project-name>
```

Example: `/init-project my-startup`

Creates: `./projects/my-startup/` with ai-sdlc as submodule

## Behavior

### 1. Gather Information

Ask the user:
- Project name (from argument)
- Brief project description
- ai-sdlc version to use (default: latest tag, or `main` for bleeding edge)
- Create GitHub repository? (Yes/No)
- If Yes: Public or Private?

### 2. Determine Paths and Capture ai-sdlc Root

```bash
# Capture ai-sdlc root directory for all subsequent commands
AI_SDLC_ROOT=$(pwd)
```

Then determine:
```
Project location: $AI_SDLC_ROOT/projects/<project-name>/
ai-sdlc repo URL: <from git remote get-url origin>
ai-sdlc version: <latest tag or user-specified>
```

**CRITICAL**: The Bash tool's working directory **persists** between invocations - it does NOT reset to ai-sdlc root. Capture `AI_SDLC_ROOT` at the beginning and use it in all subsequent commands to ensure reliability.

### 3. Create Project Structure and Initialize Git

Use chained commands with `$AI_SDLC_ROOT` to ensure correct paths:

```bash
# Create base directory and subdirectories, then initialize git
mkdir -p $AI_SDLC_ROOT/projects/<project-name> && \
  cd $AI_SDLC_ROOT/projects/<project-name> && \
  mkdir -p .claude/commands .claude/skills docs/product/user-stories docs/architecture/adr docs/legal src tests && \
  git init && \
  git submodule add <ai-sdlc-repo-url> ai-sdlc
```

### 4. Checkout ai-sdlc Version

```bash
# Checkout specific version
cd $AI_SDLC_ROOT/projects/<project-name>/ai-sdlc && \
  git checkout <version>
```

### 5. Create Files from Templates

Copy and customize from `templates/child-project/`:
- `CLAUDE.md` from `CLAUDE.md.template`
- `.claude/settings.json` from `settings.json.template`
- `README.md` from `README.md.template`

Replace placeholders:
- `{{PROJECT_NAME}}` → project name
- `{{PROJECT_DESCRIPTION}}` → description from user
- `{{AI_SDLC_VERSION}}` → version tag
- `{{DOMAIN_CONTEXT}}` → "To be defined during Discovery"
- `{{TECHNICAL_CONSTRAINTS}}` → "To be defined during Architecture"
- `{{REPO_URL}}` → "TBD - will be updated after GitHub creation"
- `{{LICENSE}}` → "TBD"

### 6. Create Placeholder Files

```bash
cd $AI_SDLC_ROOT/projects/<project-name> && \
  touch .claude/commands/.gitkeep \
        .claude/skills/.gitkeep \
        docs/product/user-stories/.gitkeep \
        docs/architecture/adr/.gitkeep \
        docs/legal/.gitkeep \
        src/.gitkeep \
        tests/.gitkeep
```

### 7. Initial Commit

```bash
cd $AI_SDLC_ROOT/projects/<project-name> && \
  git add . && \
  git commit -m "chore: initialize project with ai-sdlc framework"
```

### 8. Create GitHub Repository (if requested)

If user chose to create GitHub repo:

```bash
cd $AI_SDLC_ROOT/projects/<project-name> && \
  gh repo create <project-name> --<public|private> --source=. --push

# After creation, update README.md with actual repo URL
cd $AI_SDLC_ROOT/projects/<project-name> && \
  # Replace {{REPO_URL}} or "TBD" with https://github.com/<user>/<project-name>.git
  # Then commit and push the update
  git add README.md && \
  git commit -m "docs: update README with GitHub repo URL" && \
  git push
```

### 9. Register in siblings.json

Add the new project to `.claude/siblings.json`:

```json
{
  "projects": [
    ...existing...,
    { "path": "./projects/<project-name>", "autoUpdate": true }
  ]
}
```

### 10. Output Summary

```markdown
## Project Created: <project-name>

**Location**: ./projects/<project-name>/
**ai-sdlc version**: <version>
**GitHub repo**: <repo-url if created, or "Not created">
**Registered in**: .claude/siblings.json (autoUpdate: true)

### Structure Created
\`\`\`
projects/<project-name>/
├── ai-sdlc/              ← Submodule @ <version>
├── .claude/
│   ├── settings.json
│   ├── commands/
│   └── skills/
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

<if GitHub repo not created>
3. **Create GitHub repo later** (optional):
   \`\`\`bash
   cd projects/<project-name>
   gh repo create <project-name> --private --source=. --push
   \`\`\`
</if>
```

## Notes

- All projects are created under `./projects/` directory
- Projects are gitignored from ai-sdlc repo but have their own git repos
- Each project uses ai-sdlc as a submodule (fetched from GitHub)
- New projects are auto-registered in siblings.json for `/release` updates
- Requires `gh` CLI installed if creating GitHub repo
- Check `gh auth status` before running if GitHub creation is desired
