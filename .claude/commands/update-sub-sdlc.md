# /update-sub-sdlc

Update the ai-sdlc submodule in the current project to latest or a specific version.

## Usage
```
/update-sub-sdlc [version]
```

Examples:
- `/update-sub-sdlc` → pulls latest from main branch
- `/update-sub-sdlc v1.2.0` → checks out specific version tag

## Behavior

### 1. Verify Context

Check that current directory has an `ai-sdlc` subdirectory that is a git repo.

If not found, output error:
```
Error: ai-sdlc submodule not found in current directory.
Run this command from your project root (where ai-sdlc/ exists).
```

### 2. Capture Current State

Record the current commit/tag for comparison:
```bash
cd ai-sdlc
git describe --tags --always
```

### 3. Fetch and Update

```bash
cd ai-sdlc
git fetch --tags origin
```

**If version argument provided:**
```bash
git checkout <version>
```

**If no version argument:**
```bash
git checkout main
git pull origin main
```

### 4. Show What Changed

```bash
# Back in project root
cd ..
git diff ai-sdlc  # Shows submodule pointer change
```

Show changelog between versions:
```bash
cd ai-sdlc
git log --oneline <old-ref>..<new-ref>
```

### 5. Output Summary

```markdown
## ai-sdlc Updated

**Previous**: <old-commit-or-tag>
**Current**: <new-version-or-commit>

### Changes Included
<list of commits between old and new>

### Next Steps

To commit this update:
\`\`\`bash
git add ai-sdlc
git commit -m "chore: update ai-sdlc to <version>"
\`\`\`

To revert:
\`\`\`bash
cd ai-sdlc && git checkout <old-ref> && cd ..
\`\`\`
```

## Notes

- This command runs from **child projects** that have ai-sdlc as a submodule
- Fetches from `origin` (GitHub), ensuring you get pushed changes
- Does NOT auto-commit; user decides when to commit the submodule update
- When called by `/release`, the commit is handled automatically
