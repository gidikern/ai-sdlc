# Technology Evaluation Framework

## Evaluation Criteria

Score each option 1-5 on these dimensions:

| Criterion | Weight | Description |
|-----------|--------|-------------|
| **Fit** | High | How well does it solve our specific problem? |
| **Maturity** | High | Production-ready? Stable API? |
| **Team** | High | Current team expertise? Learning curve? |
| **Ecosystem** | Medium | Libraries, tools, community support? |
| **Performance** | Medium | Meets our requirements? |
| **Cost** | Medium | Licensing, infrastructure, operational? |
| **Longevity** | Low | Will it be maintained in 5 years? |
| **Hiring** | Low | Can we hire people who know it? |

## Evaluation Matrix Template

```markdown
## Technology Evaluation: [Category]

**Date**: YYYY-MM-DD
**Decision**: [What we're deciding]

### Options

| Criterion (Weight) | Option A | Option B | Option C |
|--------------------|----------|----------|----------|
| Fit (3x) | 4 | 3 | 5 |
| Maturity (3x) | 5 | 4 | 3 |
| Team (3x) | 3 | 5 | 2 |
| Ecosystem (2x) | 4 | 4 | 4 |
| Performance (2x) | 4 | 3 | 5 |
| Cost (2x) | 3 | 4 | 2 |
| Longevity (1x) | 5 | 4 | 3 |
| Hiring (1x) | 4 | 5 | 2 |
| **Weighted Total** | **68** | **67** | **57** |

### Recommendation
[Option] because [key reasons]
```

## Common Stack Decisions

### Backend Framework

| Consideration | Node/Express | Python/FastAPI | Go | Java/Spring |
|--------------|--------------|----------------|-----|-------------|
| Learning curve | Low | Low | Medium | High |
| Performance | Medium | Medium | High | High |
| Ecosystem | Large | Growing | Medium | Large |
| Type safety | With TS | With hints | Built-in | Built-in |
| Best for | APIs, real-time | ML/Data, APIs | High perf | Enterprise |

### Database

| Consideration | PostgreSQL | MongoDB | DynamoDB |
|--------------|------------|---------|----------|
| Data model | Relational | Document | Key-value |
| Scalability | Vertical+ | Horizontal | Horizontal |
| Consistency | Strong | Tunable | Tunable |
| Best for | Complex queries | Flexible schema | Massive scale |

### Frontend Framework

| Consideration | React | Vue | Next.js | Svelte |
|--------------|-------|-----|---------|--------|
| Learning curve | Medium | Low | Medium | Low |
| Ecosystem | Largest | Large | Large | Growing |
| Performance | Good | Good | Good | Best |
| SSR/SSG | Via Next | Via Nuxt | Built-in | Via SvelteKit |

## Red Flags

Avoid technologies that:
- Have single maintainer / no corporate backing for critical paths
- Require significant rewrites to scale
- Have declining community activity
- Lock you into a specific vendor with no exit path
- Are "resume-driven" without solving a real problem

## "Boring Technology" Principle

Prefer established, well-understood technologies unless:
1. New tech solves a problem impossible with existing tools
2. The benefit significantly outweighs adoption cost
3. Team has capacity to become experts
4. There's a clear migration path if it fails

Innovation tokens are limited. Spend them wisely.
