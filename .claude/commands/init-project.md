# /init-project

Initialize a new project using ai-sdlc framework.

## Usage
```
/init-project <project-name>
```

## Behavior

### 1. Gather Information

Ask the user:
- Project name (default from argument)
- Brief project description
- Git repository URL for ai-sdlc (default: prompt for their repo)
- ai-sdlc version to use (default: latest tag)

### 2. Create Project Structure

```bash
mkdir -p <project-name>/{.claude/commands,.claude/skills,docs/product/user-stories,docs/architecture/adr,src,tests}
```

### 3. Initialize Git and Add Submodule

```bash
cd <project-name>
git init

# Add ai-sdlc as submodule at specified version
git submodule add -b <version> <ai-sdlc-repo-url> ai-sdlc
```

### 4. Create Files from Templates

Copy and customize templates:
- `CLAUDE.md` from `CLAUDE.md.template`
- `.claude/settings.json` from `settings.json.template`
- `README.md` from `README.md.template`

Replace placeholders:
- `{{PROJECT_NAME}}` → project name
- `{{PROJECT_DESCRIPTION}}` → description
- `{{AI_SDLC_VERSION}}` → version tag
- `{{DOMAIN_CONTEXT}}` → "To be defined during Discovery"
- `{{TECHNICAL_CONSTRAINTS}}` → "To be defined during Architecture"
- `{{REPO_URL}}` → project repo URL (or placeholder)
- `{{LICENSE}}` → "TBD"

### 5. Initial Commit

```bash
git add .
git commit -m "chore: initialize project with ai-sdlc framework"
```

### 6. Next Steps

Output:
```markdown
## Project Initialized: <project-name>

### Structure Created
- ai-sdlc submodule @ <version>
- Claude Code configuration
- Documentation folders

### Next Steps

1. **Create GitHub repo** (if not done):
   ```bash
   gh repo create <project-name> --private --source=. --push
   ```

2. **Start Claude Code**:
   ```bash
   cd <project-name>
   claude
   ```

3. **Begin Discovery**:
   > "Let's explore [your product idea]"

Happy building! 🚀
```
