# /release

Create a new versioned release of ai-sdlc and optionally update all registered projects.

## Usage
```
/release <version>
```

Example: `/release v1.2.0`

## Behavior

### 1. Validate Version Format
- Must match semver: `vMAJOR.MINOR.PATCH`
- Must be greater than current latest tag

### 2. Pre-Release Checklist

Prompt user to confirm:

```markdown
## Pre-Release Checklist for [version]

### Documentation (User Responsibility)
- [ ] CHANGELOG.md updated with all changes under [Unreleased]
- [ ] README.md agents table is current (if new skills added)
- [ ] CLAUDE.md updated (if framework structure changed)
- [ ] All skills registered in both settings files

### Quality
- [ ] All skills have valid SKILL.md
- [ ] Run `/validate-skill` on any new/modified skills
- [ ] Tested on at least one child project
- [ ] No known breaking issues

### Breaking Changes (if MAJOR version)
- [ ] Breaking changes documented in CHANGELOG
- [ ] Migration guide provided (if needed)

Confirm release? (yes/no)
```

**Note**: The `/release` command does NOT automatically update documentation files.
These must be updated manually BEFORE running `/release`:
- `CHANGELOG.md` - Add changes under [Unreleased]
- `README.md` - Update agents table, commands, etc.
- `CLAUDE.md` - Update if framework structure changed

### 3. Create and Push Tag

```bash
# Ensure everything is committed
git status

# Create annotated tag
git tag -a <version> -m "Release <version>: [brief description]"

# Push commits and tag
git push origin main
git push origin <version>
```

### 4. Update Registered Projects

Read `.claude/siblings.json` and for each project with `autoUpdate: true`:

Use chained commands with full paths to maintain directory context:

```bash
# Update submodule to new version
cd <project-path>/ai-sdlc && \
  git fetch --tags origin && \
  git checkout <version>

# Commit and push the submodule update
cd <project-path> && \
  git add ai-sdlc && \
  git commit -m "chore: update ai-sdlc to <version>" && \
  git push
```

**Important**: Each Bash tool invocation starts from the ai-sdlc root directory. Use full relative paths (e.g., `./projects/haas/ai-sdlc`) and chain commands with `&&`.

Display progress:
```markdown
## Updating Projects

| Project | Status |
|---------|--------|
| projects/my-startup | ✅ Updated to <version> |
| projects/another-project | ✅ Updated to <version> |
| projects/experimental | ⏭️ Skipped (autoUpdate: false) |
```

### 5. Post-Release Summary

```markdown
## Release Complete: <version>

### ai-sdlc
- Tag `<version>` created and pushed

### Projects Updated
- projects/my-startup → <version>
- projects/another-project → <version>

### Projects Skipped
- projects/experimental (autoUpdate: false)

### Next Steps
- Push project changes to their remotes if desired:
  \`\`\`bash
  cd projects/my-startup && git push
  cd projects/another-project && git push
  \`\`\`
- Announce release to team (if applicable)
```

## Version Guidelines

| Change Type | Version Bump | Example |
|-------------|--------------|---------|
| Breaking skill interface changes | MAJOR | v1.0.0 → v2.0.0 |
| New skills or workflows | MINOR | v1.0.0 → v1.1.0 |
| Bug fixes, doc updates | PATCH | v1.0.0 → v1.0.1 |

## siblings.json Format

Located at `.claude/siblings.json`:

```json
{
  "description": "Projects managed by ai-sdlc. Used by /release to auto-update submodules.",
  "projects": [
    { "path": "./projects/my-startup", "autoUpdate": true },
    { "path": "./projects/experimental", "autoUpdate": false }
  ]
}
```

- `path`: Relative path from ai-sdlc root to the project
- `autoUpdate`: If `true`, `/release` will update this project's submodule
