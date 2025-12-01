# Code Review Checklist

## Quick Review (Every PR)

### Functionality
- [ ] Code does what it's supposed to do
- [ ] Edge cases considered
- [ ] Error states handled
- [ ] No regressions in existing functionality

### Code Quality
- [ ] Readable and understandable
- [ ] No unnecessary complexity
- [ ] DRY (no duplicate code)
- [ ] Functions/methods are focused (single responsibility)

### Testing
- [ ] New code has tests
- [ ] Tests are meaningful (not just coverage)
- [ ] All tests pass

### Security
- [ ] No hardcoded secrets
- [ ] User input validated
- [ ] No SQL injection risks
- [ ] Authentication/authorization correct

## Deep Review (Major Features)

### Architecture
- [ ] Fits within existing architecture
- [ ] Follows established patterns
- [ ] Appropriate separation of concerns
- [ ] No unnecessary dependencies added

### Data
- [ ] Database changes are safe
- [ ] Migrations are reversible
- [ ] Indexes added where needed
- [ ] No N+1 query issues

### API
- [ ] Endpoints follow conventions
- [ ] Input validation present
- [ ] Error responses consistent
- [ ] Documentation updated

### Performance
- [ ] No obvious bottlenecks
- [ ] Appropriate caching considered
- [ ] Large datasets handled efficiently
- [ ] No memory leaks

## Review Comments Guide

### Blocking (🔴)

Must be fixed before merge:

```
🔴 **Security**: This SQL query is vulnerable to injection.
Use parameterized queries:

// Instead of
const users = await db.query(`SELECT * FROM users WHERE id = ${id}`);

// Use
const users = await db.query('SELECT * FROM users WHERE id = $1', [id]);
```

### Suggestion (🟡)

Recommended improvement:

```
🟡 **Readability**: Consider extracting this logic into a named function.
This would improve readability and make it easier to test:

function isEligibleForDiscount(user: User): boolean {
  return user.isPremium && user.ordersCount > 5;
}
```

### Nitpick (🟢)

Optional, minor item:

```
🟢 **Style**: Nitpick - this could be simplified with optional chaining:

// Current
const name = user && user.profile && user.profile.name;

// Suggested
const name = user?.profile?.name;
```

### Question (❓)

Seeking clarification:

```
❓ **Question**: Is this intentional? I expected this to filter active users only.
Could you clarify the business requirement?
```

### Highlight (✅)

Positive feedback:

```
✅ **Nice**: Great use of the strategy pattern here.
This makes adding new payment providers much cleaner!
```

## Common Issues to Watch For

### Logic Errors
- Off-by-one errors in loops
- Incorrect comparison operators
- Missing null checks
- Race conditions in async code

### Security Issues
- SQL/NoSQL injection
- XSS vulnerabilities
- CSRF missing
- Sensitive data in logs
- Insecure random generation

### Performance Issues
- N+1 queries
- Missing indexes
- Large objects in memory
- Unnecessary re-renders (React)
- Blocking operations in async code

### Maintainability Issues
- Magic numbers/strings
- Deep nesting
- Large functions
- Tight coupling
- Missing error context

## Tone Guidelines

**Do:**
- "Consider using..." instead of "You should use..."
- "This might cause..." instead of "This is wrong"
- "What do you think about..." instead of "Change this to..."

**Don't:**
- Use absolute language ("never", "always", "wrong")
- Make it personal ("you always", "your code")
- Be condescending
- Leave vague feedback
