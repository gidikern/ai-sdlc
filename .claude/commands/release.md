# /release

Create a new versioned release of ai-sdlc.

## Usage
```
/release <version>
```

Example: `/release v1.1.0`

## Behavior

### 1. Validate Version Format
- Must match semver: `vMAJOR.MINOR.PATCH`
- Must be greater than current latest tag

### 2. Pre-Release Checklist

Prompt user to confirm:

```markdown
## Pre-Release Checklist for [version]

### Documentation
- [ ] CHANGELOG.md updated with changes
- [ ] README.md is current
- [ ] All skills have valid SKILL.md

### Quality
- [ ] All skills validated (`/validate-skill` passed)
- [ ] Tested on at least one child project
- [ ] No known breaking issues

### Breaking Changes (if MAJOR version)
- [ ] Breaking changes documented in CHANGELOG
- [ ] Migration guide provided (if needed)

Confirm release? (yes/no)
```

### 3. If Confirmed

Guide user through:

```bash
# Ensure everything is committed
git status

# Create annotated tag
git tag -a v1.x.x -m "Release v1.x.x: [brief description]"

# Push tag
git push origin v1.x.x
```

### 4. Post-Release

Remind user:
- Update child projects to new version if desired
- Announce changes to team (if applicable)

## Version Guidelines

| Change Type | Version Bump | Example |
|-------------|--------------|---------|
| Breaking skill interface changes | MAJOR | v1.0.0 → v2.0.0 |
| New skills or workflows | MINOR | v1.0.0 → v1.1.0 |
| Bug fixes, doc updates | PATCH | v1.0.0 → v1.0.1 |
