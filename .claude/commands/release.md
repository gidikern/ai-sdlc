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

### 4. Sync Skills, Commands, and Workflows to Registered Projects

Read `.claude/siblings.json` and for each project with `autoUpdate: true`:

**CRITICAL**: The Bash tool's working directory persists between invocations. Use absolute paths with `$AI_SDLC_ROOT`.

First, get the ai-sdlc root directory:
```bash
AI_SDLC_ROOT=$(pwd)
```

Then, for each project, check THREE things:

#### a) Check Skills (Settings.json)

1. Read parent `.claude/settings.json` to get all available skills
2. Read project's `.claude/settings.json` to get current skills
3. Compare and identify missing skills (cumulative, not just new ones)

#### b) Check Workflow Commands

1. List workflow commands in parent `.claude/commands/`:
   - `cross-functional-discovery.md`
   - (Exclude framework commands: init-project, release, new-skill, validate-skill, prepare-release)
2. List workflow commands in project `.claude/commands/`
3. Compare and identify missing or updated commands

#### c) Check Workflow Files

1. List workflows in parent `workflows/*.md`
2. List workflows in project `.claude/workflows/*.md`
3. Compare and identify missing or updated workflows

#### d) Ask User for Each Project with Missing Items

If any missing/updated items found:
```markdown
## Project: <project-name>

**Missing skills:**
- facilitator
- ux-researcher

**Missing/updated commands:**
- cross-functional-discovery.md (updated)

**Missing/updated workflows:**
- cross-functional-discovery.md (new)
- discovery-to-architecture.md (updated)

Sync these to project? (yes/no)
```

#### e) Update Project if Approved

If user says yes:
1. Add missing skill paths to project's `.claude/settings.json`
2. Copy missing/updated commands to project's `.claude/commands/`
3. Copy missing/updated workflows to project's `.claude/workflows/`
4. Commit the changes:

```bash
cd $AI_SDLC_ROOT/<project-path> && \
  git add .claude/ && \
  git commit -m "chore: sync skills, commands, and workflows from ai-sdlc <version>" && \
  git push
```

Display progress:
```markdown
## Syncing Projects

| Project | Updates | Status |
|---------|---------|--------|
| projects/haas | 2 skills, 1 command, 1 workflow | ✅ Synced |
| projects/health-coach | (none) | ✅ Already in sync |
| projects/experimental | - | ⏭️ Skipped (autoUpdate: false) |
```

### 5. Post-Release Summary

```markdown
## Release Complete: <version>

### ai-sdlc
- Tag `<version>` created and pushed

### Projects Synced
- projects/haas → Added 2 skills, 1 command, 1 workflow
- projects/health-coach → Already in sync

### Projects Skipped
- projects/experimental (autoUpdate: false)

### Next Steps
- Announce release to team (if applicable)
- Projects now have latest skills, commands, and workflows
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
  "description": "Projects managed by ai-sdlc. Used by /release to sync skills, commands, and workflows.",
  "projects": [
    { "path": "./projects/my-startup", "autoUpdate": true },
    { "path": "./projects/experimental", "autoUpdate": false }
  ]
}
```

- `path`: Relative path from ai-sdlc root to the project
- `autoUpdate`: If `true`, `/release` will check for missing/updated items and ask to sync

## Notes

- Sync is cumulative: checks for ALL missing items, not just newly added ones
- Syncs three things: skills (settings.json), workflow commands (.claude/commands), and workflows (.claude/workflows)
- Only workflow commands are synced; framework commands (init-project, release, etc.) stay in parent
- User approval required for each project
- If user declines, they'll be asked again in the next release
- Projects can evolve at their own pace
