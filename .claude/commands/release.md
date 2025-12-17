# /release

Create a new versioned release of ai-sdlc and optionally sync skills to registered projects.

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

### 4. Sync Skills to Registered Projects

Read `.claude/siblings.json` and for each project with `autoUpdate: true`:

**CRITICAL**: The Bash tool's working directory persists between invocations. Use absolute paths with `$AI_SDLC_ROOT`.

First, get the ai-sdlc root directory:
```bash
AI_SDLC_ROOT=$(pwd)
```

Then, for each project:

#### a) Read and Compare Settings

1. Read parent `.claude/settings.json` to get all available skills
2. Read project's `.claude/settings.json` to get current skills
3. Compare and identify missing skills (cumulative, not just new ones)

#### b) Ask User for Each Project with Missing Skills

If missing skills found:
```markdown
## Project: <project-name>

Missing skills:
- facilitator
- ux-researcher
- data-analyst

Add these skills to project settings.json? (yes/no)
```

#### c) Update Settings if Approved

If user says yes:
1. Add missing skill paths to project's settings.json
2. Commit the change:

```bash
cd $AI_SDLC_ROOT/<project-path> && \
  git add .claude/settings.json && \
  git commit -m "chore: sync skills from ai-sdlc <version>" && \
  git push
```

Display progress:
```markdown
## Syncing Projects

| Project | Missing Skills | Status |
|---------|----------------|--------|
| projects/haas | facilitator, ux-researcher | ✅ Updated |
| projects/health-coach | (none) | ✅ Already in sync |
| projects/experimental | - | ⏭️ Skipped (autoUpdate: false) |
```

### 5. Post-Release Summary

```markdown
## Release Complete: <version>

### ai-sdlc
- Tag `<version>` created and pushed

### Projects Synced
- projects/haas → Added 2 skills
- projects/health-coach → Already in sync

### Projects Skipped
- projects/experimental (autoUpdate: false)

### Next Steps
- Announce release to team (if applicable)
- Projects will inherit new skills on next Claude session
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
  "description": "Projects managed by ai-sdlc. Used by /release to sync skills.",
  "projects": [
    { "path": "./projects/my-startup", "autoUpdate": true },
    { "path": "./projects/experimental", "autoUpdate": false }
  ]
}
```

- `path`: Relative path from ai-sdlc root to the project
- `autoUpdate`: If `true`, `/release` will check for missing skills and ask to sync

## Notes

- Skills sync is cumulative: checks for ALL missing skills, not just newly added ones
- User approval required for each project
- If user declines, they'll be asked again in the next release
- Projects can evolve at their own pace
