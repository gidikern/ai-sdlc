# ADR Template

Architecture Decision Records capture important technical decisions.

## File Naming

```
ADR-NNN-short-title.md
```

Example: `ADR-001-use-postgresql-for-primary-database.md`

## Template

```markdown
# ADR-NNN: [Title]

**Date**: YYYY-MM-DD
**Status**: Proposed | Accepted | Deprecated | Superseded by ADR-XXX
**Deciders**: [Names/roles]

## Context

What is the issue that we're seeing that is motivating this decision or change?

## Decision Drivers

- [Driver 1: e.g., scalability requirement]
- [Driver 2: e.g., team expertise]
- [Driver 3: e.g., cost constraints]

## Considered Options

### Option 1: [Name]
**Description**: Brief description

**Pros**:
- Pro 1
- Pro 2

**Cons**:
- Con 1
- Con 2

### Option 2: [Name]
**Description**: Brief description

**Pros**:
- Pro 1
- Pro 2

**Cons**:
- Con 1
- Con 2

### Option 3: [Name]
[Same structure]

## Decision

We will use **[chosen option]** because [rationale].

## Consequences

### Positive
- [Positive consequence 1]
- [Positive consequence 2]

### Negative
- [Negative consequence 1]
- [Trade-off we accept]

### Risks
- [Risk 1 and mitigation]

## Follow-up Actions
- [ ] Action item 1
- [ ] Action item 2

## References
- [Link to relevant documentation]
- [Link to related ADR]
```

## Common ADR Categories

| Category | Examples |
|----------|----------|
| **Data** | Database choice, caching strategy, data format |
| **Integration** | API style, message broker, auth provider |
| **Infrastructure** | Cloud provider, container orchestration, CDN |
| **Architecture** | Monolith vs microservices, event sourcing |
| **Frontend** | Framework choice, state management, styling |
| **Security** | Auth mechanism, encryption, secrets management |

## ADR Index Template

Maintain an index file `adr/README.md`:

```markdown
# Architecture Decision Records

| ADR | Title | Status | Date |
|-----|-------|--------|------|
| [001](ADR-001-xxx.md) | Title | Accepted | 2024-01-15 |
| [002](ADR-002-xxx.md) | Title | Accepted | 2024-01-20 |
```
