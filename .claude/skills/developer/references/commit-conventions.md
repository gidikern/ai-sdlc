# Commit Conventions

## Conventional Commits Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

## Types

| Type | Description | Example |
|------|-------------|---------|
| `feat` | New feature | `feat(auth): add password reset` |
| `fix` | Bug fix | `fix(api): handle null user response` |
| `docs` | Documentation | `docs(readme): update setup instructions` |
| `style` | Formatting (no code change) | `style: fix indentation` |
| `refactor` | Refactoring (no feature/fix) | `refactor(user): extract validation` |
| `perf` | Performance improvement | `perf(query): add index for user lookup` |
| `test` | Adding tests | `test(auth): add login integration tests` |
| `chore` | Maintenance | `chore(deps): update dependencies` |
| `ci` | CI/CD changes | `ci: add staging deployment` |
| `build` | Build system | `build: update webpack config` |
| `revert` | Revert commit | `revert: feat(auth): add oauth` |

## Scope

Scope is optional but helpful. Use module/feature name:

```
feat(auth): add JWT validation
fix(payments): correct tax calculation
refactor(user-profile): simplify avatar upload
```

## Subject

- Use imperative mood ("add" not "added" or "adds")
- Don't capitalize first letter
- No period at end
- Max 50 characters

```
✓ feat(auth): add password validation
✗ feat(auth): Added password validation.
✗ feat(auth): Adds password validation
```

## Body

- Explain what and why (not how)
- Wrap at 72 characters
- Separate from subject with blank line

```
feat(notifications): add email digest option

Users requested a way to receive daily/weekly summaries instead of
individual notifications. This adds a preference setting and a
scheduled job to compile and send digests.

Closes #234
```

## Footer

Reference issues and breaking changes:

```
feat(api)!: change user endpoint response format

BREAKING CHANGE: User endpoint now returns nested address object
instead of flat fields.

Closes #456
Refs #123, #124
```

## Breaking Changes

Two ways to indicate:

1. `!` after type/scope: `feat(api)!: change response format`
2. `BREAKING CHANGE:` in footer

## Examples

### Simple Feature

```
feat(dashboard): add activity chart
```

### Bug Fix with Context

```
fix(checkout): prevent duplicate order submission

When users double-clicked the submit button, duplicate orders were
created. Added debounce and disabled button during processing.

Fixes #789
```

### Refactoring

```
refactor(user-service): extract email validation

Move email validation to shared utility for reuse in registration
and profile update flows.
```

### Breaking Change

```
feat(api)!: require authentication for all endpoints

BREAKING CHANGE: All API endpoints now require Bearer token.
Previously, read-only endpoints were public.

Migration guide: https://docs.example.com/migration/v2-auth
```

## Commit Best Practices

1. **Atomic commits** - One logical change per commit
2. **Commit often** - Small, incremental changes
3. **Don't commit broken code** - Each commit should build
4. **Reference issues** - Link to tickets/stories
5. **Review before committing** - `git diff --staged`

## Git Hooks

Use commitlint to enforce conventions:

```bash
# Install
npm install --save-dev @commitlint/cli @commitlint/config-conventional

# commitlint.config.js
module.exports = { extends: ['@commitlint/config-conventional'] };

# With husky
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
```
