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

### 2. Determine Paths

```
Project location: ./projects/<project-name>/
ai-sdlc repo URL: <from git remote get-url origin>
ai-sdlc version: <latest tag or user-specified>
```

### 3. Create Project Structure

```bash
mkdir -p ./projects/<project-name>/{.claude/commands,.claude/skills,docs/product/user-stories,docs/architecture/adr,src,tests}
```

### 4. Initialize Git and Add Submodule

```bash
cd ./projects/<project-name>
git init

# Add ai-sdlc as submodule
git submodule add <ai-sdlc-repo-url> ai-sdlc
cd ai-sdlc && git checkout <version> && cd ..
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
- `{{REPO_URL}}` → "TBD - update after creating remote repo"
- `{{LICENSE}}` → "TBD"

### 6. Create Placeholder Files

```bash
touch .claude/commands/.gitkeep
touch .claude/skills/.gitkeep
touch docs/product/user-stories/.gitkeep
touch docs/architecture/adr/.gitkeep
touch src/.gitkeep
touch tests/.gitkeep
```

### 7. Initial Commit

```bash
git add .
git commit -m "chore: initialize project with ai-sdlc framework"
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

### 9. Output Summary

```markdown
## Project Created: <project-name>

**Location**: ./projects/<project-name>/
**ai-sdlc version**: <version>
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

1. **Create GitHub repo** (optional):
   \`\`\`bash
   cd projects/<project-name>
   gh repo create <project-name> --private --source=. --push
   \`\`\`

2. **Start working**:
   \`\`\`bash
   cd projects/<project-name>
   claude
   \`\`\`

3. **Begin Discovery**:
   > "Let's explore [your product idea]"
```

## Notes

- All projects are created under `./projects/` directory
- Projects are gitignored from ai-sdlc repo but have their own git repos
- Each project uses ai-sdlc as a submodule (fetched from GitHub)
- New projects are auto-registered in siblings.json for `/release` updates
