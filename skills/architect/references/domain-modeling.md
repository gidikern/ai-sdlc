# Domain Modeling Guide

## Purpose

Define the core business concepts (entities) and their relationships before writing code. A good domain model makes everything else easier.

## Process

```
1. Identify Entities    → What "things" exist in the system?
2. Define Attributes    → What data does each entity have?
3. Map Relationships    → How do entities relate?
4. Identify Aggregates  → What changes together?
5. Define Boundaries    → What belongs where?
```

## Entity Identification

### Questions to Ask
- What are the key nouns in the PRD/user stories?
- What does the user create, read, update, delete?
- What needs to be tracked over time?
- What has its own identity (vs. being just an attribute)?

### Example: Health Coaching App
```
Nouns from PRD:
- User → Entity (has identity, lifecycle)
- Health Goal → Entity (tracked over time)
- Meal → Entity (individual records)
- Weight → Value Object (just a measurement)
- Coach → Could be entity or role
```

## Entity Template

```markdown
## [Entity Name]

**Description**: [What is this thing?]

**Identity**: [How is it uniquely identified?]

### Attributes
| Attribute | Type | Required | Notes |
|-----------|------|----------|-------|
| id | UUID | Yes | Primary key |
| ... | | | |

### Relationships
- [Relationship description]

### Lifecycle
- Created when: [trigger]
- Updated when: [triggers]
- Deleted when: [trigger or "never"]

### Business Rules
- [Rule 1]
- [Rule 2]
```

## Relationship Types

```
One-to-One (1:1)
User ──────── Profile
"Each user has exactly one profile"

One-to-Many (1:N)
User ──────<< Meal
"A user has many meals"

Many-to-Many (M:N)
User >>────<< Goal
"Users can have many goals, goals can be shared"
```

### Notation in Diagrams

```
──────    One
─────<    Many
─────o    Optional (zero or one)
─────||   Exactly one (required)

Examples:
User ||────o< Profile     # User has zero or one profile
User ||────<< Meal        # User has many meals (required)
Meal }o────|| Category    # Meal optionally has one category
```

## Aggregate Design

Aggregates = clusters of entities that change together and are accessed as a unit.

### Rules
1. One entity is the "aggregate root" - the entry point
2. External references only point to the root
3. Changes within aggregate are transactional
4. Keep aggregates small

### Example

```
┌─────────────────────────────────┐
│  User Aggregate                 │
│  ┌─────────────────┐           │
│  │     User        │ ← Root    │
│  │  (aggregate     │           │
│  │   root)         │           │
│  └────────┬────────┘           │
│           │                     │
│  ┌────────┴────────┐           │
│  │    Profile      │           │
│  └─────────────────┘           │
└─────────────────────────────────┘

┌─────────────────────────────────┐
│  Health Tracking Aggregate      │
│  ┌─────────────────┐           │
│  │   HealthLog     │ ← Root    │
│  └────────┬────────┘           │
│           │                     │
│  ┌────────┼────────┐           │
│  ▼        ▼        ▼           │
│ Meal    Weight   Activity      │
└─────────────────────────────────┘
```

## Domain Model Document

Create `docs/architecture/domain-model.md`:

```markdown
# Domain Model: [Product Name]

## Overview Diagram

[Mermaid or ASCII diagram showing all entities and relationships]

## Aggregates

### [Aggregate Name]
**Root**: [Entity name]
**Entities**: [List]
**Purpose**: [Why grouped together]

## Entities

### [Entity 1]
[Use entity template]

### [Entity 2]
[Use entity template]

## Value Objects
[Things without identity - just values]

## Domain Events
[Important things that happen]
- UserRegistered
- GoalCreated
- MealLogged

## Glossary
| Term | Definition |
|------|------------|
| | |
```

## Example: Health App Domain Model

```
┌─────────────────────────────────────────────────────────────┐
│                     DOMAIN MODEL                             │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────┐         ┌──────────┐         ┌──────────┐    │
│  │   User   │────────<│   Goal   │         │ AICoach  │    │
│  └────┬─────┘         └──────────┘         └────┬─────┘    │
│       │                                         │           │
│       │ 1:1                                     │           │
│       ▼                                         │           │
│  ┌──────────┐                                   │           │
│  │ Profile  │                                   │           │
│  └──────────┘                                   │           │
│       │                                         │           │
│       │ 1:N                                     │ 1:N       │
│       ▼                                         ▼           │
│  ┌──────────┐    ┌──────────┐    ┌────────────────┐        │
│  │HealthLog │───<│  Meal    │    │ Conversation   │        │
│  │          │───<│  Weight  │    │    Message     │        │
│  │          │───<│ Activity │    └────────────────┘        │
│  └──────────┘    └──────────┘                              │
│                                                              │
└─────────────────────────────────────────────────────────────┘

Entities:
- User: The person using the app
- Profile: User preferences, demographics
- Goal: Health objectives (lose weight, build muscle)
- HealthLog: Daily tracking container
- Meal: Food intake record
- Weight: Body weight measurement
- Activity: Exercise/movement record
- AICoach: Personalized coaching persona
- Conversation: Chat history with AI coach
```

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Too many entities | Complexity explosion | Start with 5-7 core entities |
| Anemic models | No business logic | Put behavior with data |
| God entity | One entity does everything | Split by responsibility |
| Missing aggregates | Transaction issues | Group what changes together |
| Premature optimization | Tables before understanding | Model domain first, schema second |
