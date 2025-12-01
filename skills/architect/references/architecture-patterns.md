# Architecture Patterns

## System Architecture Patterns

### Monolith

```
┌─────────────────────────────────┐
│           Monolith              │
│  ┌─────┐ ┌─────┐ ┌─────┐       │
│  │ UI  │ │ API │ │ BL  │       │
│  └─────┘ └─────┘ └─────┘       │
│         ┌─────────┐            │
│         │   DB    │            │
│         └─────────┘            │
└─────────────────────────────────┘
```

**When to use**: Starting out, small team, unclear boundaries
**Pros**: Simple, fast development, easy deployment
**Cons**: Scaling limitations, deployment coupling

### Modular Monolith

```
┌─────────────────────────────────────────┐
│              Modular Monolith           │
│  ┌──────────┐ ┌──────────┐ ┌─────────┐ │
│  │  Users   │ │  Orders  │ │ Payment │ │
│  │  Module  │ │  Module  │ │ Module  │ │
│  └────┬─────┘ └────┬─────┘ └────┬────┘ │
│       │            │            │       │
│       └────────────┼────────────┘       │
│                    ▼                    │
│              ┌─────────┐                │
│              │   DB    │                │
│              └─────────┘                │
└─────────────────────────────────────────┘
```

**When to use**: Growing product, preparing for potential split
**Pros**: Clear boundaries, easier to extract later
**Cons**: Discipline required, shared DB risks

### Microservices

```
┌─────────┐     ┌─────────┐     ┌─────────┐
│  Users  │     │ Orders  │     │ Payment │
│ Service │     │ Service │     │ Service │
└────┬────┘     └────┬────┘     └────┬────┘
     │               │               │
     ▼               ▼               ▼
┌─────────┐     ┌─────────┐     ┌─────────┐
│ Users   │     │ Orders  │     │ Payment │
│   DB    │     │   DB    │     │   DB    │
└─────────┘     └─────────┘     └─────────┘
```

**When to use**: Large teams, independent scaling needs, diverse tech requirements
**Pros**: Independent deployment, scaling, technology choice
**Cons**: Complexity, operational overhead, eventual consistency

## API Patterns

### REST

```
GET    /users          → List users
POST   /users          → Create user
GET    /users/{id}     → Get user
PUT    /users/{id}     → Update user
DELETE /users/{id}     → Delete user
```

**When to use**: CRUD operations, public APIs, broad compatibility
**Conventions**: Use nouns, HTTP verbs, status codes, HATEOAS for discoverability

### GraphQL

```graphql
type Query {
  user(id: ID!): User
  users(filter: UserFilter): [User!]!
}

type Mutation {
  createUser(input: CreateUserInput!): User!
}
```

**When to use**: Complex data requirements, multiple clients, flexible queries
**Considerations**: N+1 queries, caching complexity, learning curve

### Event-Driven

```
Service A ──publish──▶ Event Bus ──subscribe──▶ Service B
                                 ──subscribe──▶ Service C
```

**When to use**: Async workflows, decoupled services, audit trails
**Patterns**: Event sourcing, CQRS, saga pattern

## Data Patterns

### Single Database

Simple, consistent, good for most applications.

### Database per Service

Each service owns its data. Required for true microservices.

### CQRS (Command Query Responsibility Segregation)

```
Commands ──▶ Write Model ──▶ Write DB
                   │
                   ▼ (events)
Queries  ◀── Read Model  ◀── Read DB
```

**When to use**: Different read/write scaling, complex queries, event sourcing

## Frontend Patterns

### SPA (Single Page Application)

```
Browser ──API calls──▶ Backend
   │
   └── All rendering in browser
```

**When to use**: Interactive apps, offline capability, desktop-like experience

### SSR (Server-Side Rendering)

```
Browser ──request──▶ Server ──HTML──▶ Browser
                         │
                    API/DB access
```

**When to use**: SEO important, fast first paint, less JS

### Hybrid (Next.js, Nuxt)

Best of both: SSR for initial load, SPA for interactions.

## Recommended Starting Points

| Scenario | Recommendation |
|----------|----------------|
| MVP / Startup | Modular Monolith + PostgreSQL + Next.js |
| Enterprise | Microservices + Event-driven + GraphQL |
| High Traffic | CDN + Edge + Serverless + NoSQL |
| Data-heavy | CQRS + Event Sourcing + Time-series DB |
