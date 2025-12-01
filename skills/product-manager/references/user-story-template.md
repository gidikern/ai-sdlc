# User Story Template

## Format

```markdown
# [EPIC-ID] Story Title

**As a** [user type]
**I want to** [action/capability]
**So that** [benefit/value]

## Acceptance Criteria

- [ ] Given [context], when [action], then [expected result]
- [ ] Given [context], when [action], then [expected result]

## Technical Notes
[Any known technical considerations]

## Dependencies
- [Story IDs this depends on]

## Estimation
**Size**: S | M | L | XL
**Complexity**: Low | Medium | High

## Priority
**Value**: High | Medium | Low
**Effort**: High | Medium | Low
**Priority Score**: [Value/Effort]
```

## Size Guidelines

| Size | Description | Typical Duration |
|------|-------------|------------------|
| S | Simple, well-understood, minimal dependencies | < 1 day |
| M | Moderate complexity, some unknowns | 1-3 days |
| L | Complex, multiple components, some risk | 3-5 days |
| XL | Very complex, should consider splitting | > 5 days |

## Good User Story Checklist (INVEST)

- **I**ndependent: Can be developed separately
- **N**egotiable: Details can be discussed
- **V**aluable: Delivers user value
- **E**stimable: Can be sized
- **S**mall: Fits in a sprint
- **T**estable: Has clear acceptance criteria

## Examples

### Good Example

```markdown
# AUTH-001 User Login

**As a** registered user
**I want to** log in with my email and password
**So that** I can access my personalized dashboard

## Acceptance Criteria
- [ ] Given valid credentials, when I submit login form, then I'm redirected to dashboard
- [ ] Given invalid credentials, when I submit login form, then I see an error message
- [ ] Given I forgot my password, when I click "Forgot Password", then I receive a reset email

## Technical Notes
- Use JWT tokens with 24h expiration
- Rate limit: 5 attempts per minute

## Dependencies
- AUTH-000 User registration

## Estimation
**Size**: M
**Complexity**: Medium
```

### Bad Example (too vague)

```markdown
# User can log in

User should be able to log in to the system.
```
