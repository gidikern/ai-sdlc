# /prepare-release

Prepare CHANGELOG.md for an upcoming release by reviewing commits and updating the [Unreleased] section.

## Usage
```
/prepare-release
```

Run this before `/release` to ensure CHANGELOG.md is up to date.

## Behavior

### 1. Find Latest Release

```bash
git tag --list 'v*' --sort=-version:refname | head -1
```

If no tags exist, use initial commit as baseline.

### 2. Show Commits Since Last Release

```bash
git log <last-tag>..HEAD --oneline --no-merges
```

Display commits to user in categorized format:
```markdown
## Commits Since <last-tag> (<count> commits)

### Features
- <commit-hash> feat: <message>

### Fixes
- <commit-hash> fix: <message>

### Documentation
- <commit-hash> docs: <message>

### Other
- <commit-hash> chore: <message>
```

### 3. Ask User to Review and Edit

Present the commits and ask:
```markdown
## Prepare CHANGELOG Entries

Based on the commits above, here are suggested CHANGELOG entries:

### Added
- <entry based on feat: commits>

### Changed
- <entry based on refactor/improve commits>

### Fixed
- <entry based on fix: commits>

### Documentation
- <entry based on docs: commits>

Would you like to:
1. Accept these entries
2. Edit before adding
3. Cancel
```

### 4. Update CHANGELOG.md

Read current CHANGELOG.md and update the [Unreleased] section:

```markdown
## [Unreleased]

### Added
<new entries>

### Changed
<new entries>

### Fixed
<new entries>

### Documentation
<new entries>

<rest of existing Unreleased content if any>
```

**Important**:
- Preserve any existing [Unreleased] entries (user may have added manually)
- Append new entries to appropriate sections
- If section doesn't exist, create it

### 5. Commit CHANGELOG Update

```bash
git add CHANGELOG.md
git commit -m "docs: update CHANGELOG for upcoming release"
```

### 6. Output Summary

```markdown
## CHANGELOG Updated

Added entries under [Unreleased]:
- X items in Added
- X items in Changed
- X items in Fixed
- X items in Documentation

### Next Steps

Ready to release? Run:
\`\`\`bash
/release v1.x.x
\`\`\`

Need more changes? The [Unreleased] section is ready - you can:
- Add more commits and run `/prepare-release` again
- Manually edit CHANGELOG.md
```

## Entry Generation Rules

Convert commit messages to CHANGELOG entries:

| Commit Pattern | CHANGELOG Section | Example |
|----------------|-------------------|---------|
| `feat:` | Added | "feat: add GitHub repo creation" → "GitHub repo creation in /init-project" |
| `fix:` | Fixed | "fix: use chained commands" → "Directory context loss in /init-project" |
| `docs:` | Documentation | "docs: update README" → "README.md updated with..." |
| `refactor:`, `perf:` | Changed | "refactor: simplify logic" → "Simplified..." |
| `chore:` | (Usually skip) | Only include if significant |

**Format guidelines:**
- Remove commit prefixes (feat:, fix:, etc.)
- Use past tense or present tense consistently
- Be specific but concise
- Group similar changes together

## Notes

- Run this multiple times if needed - it's idempotent
- Existing [Unreleased] entries are preserved
- User always has final approval before updating
- This command does NOT create a release or tag
