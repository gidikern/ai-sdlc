# Prioritization Frameworks

## RICE Scoring

Calculate priority score for each feature:

```
RICE Score = (Reach × Impact × Confidence) / Effort
```

| Factor | Scale | Description |
|--------|-------|-------------|
| **Reach** | Number of users affected per quarter | How many users will this impact? |
| **Impact** | 0.25 (minimal) to 3 (massive) | How much will it impact each user? |
| **Confidence** | 0-100% | How confident are we in estimates? |
| **Effort** | Person-months | How much work is required? |

### Impact Scale
- 3 = Massive impact
- 2 = High impact
- 1 = Medium impact
- 0.5 = Low impact
- 0.25 = Minimal impact

### Example

| Feature | Reach | Impact | Confidence | Effort | Score |
|---------|-------|--------|------------|--------|-------|
| Social login | 5000 | 1 | 80% | 1 | 4000 |
| Dark mode | 3000 | 0.5 | 90% | 0.5 | 2700 |
| AI chat | 2000 | 2 | 50% | 3 | 667 |

## MoSCoW Method

Categorize requirements into:

| Category | Definition | Guideline |
|----------|------------|-----------|
| **Must** | Critical for launch, non-negotiable | ~60% of effort |
| **Should** | Important but not critical | ~20% of effort |
| **Could** | Nice to have, low impact if omitted | ~20% of effort |
| **Won't** | Explicitly excluded from this release | Documented for future |

### Usage Rules
1. Must-haves define MVP
2. If a Must can't be delivered, project fails
3. Shoulds are first candidates for scope reduction
4. Coulds only if time permits
5. Won'ts prevent scope creep

## Value vs Effort Matrix

```
         High Value
              │
    Quick     │    Strategic
    Wins      │    Priorities
              │
Low ──────────┼────────── High
Effort        │           Effort
              │
    Fill-ins  │    Reconsider
    (Maybe)   │    (Avoid)
              │
         Low Value
```

### Quadrant Actions

| Quadrant | Action |
|----------|--------|
| Quick Wins (High Value, Low Effort) | Do first |
| Strategic (High Value, High Effort) | Plan carefully |
| Fill-ins (Low Value, Low Effort) | Do if time permits |
| Reconsider (Low Value, High Effort) | Usually avoid |

## Kano Model

Classify features by user satisfaction:

| Type | Description | Strategy |
|------|-------------|----------|
| **Basic** | Expected, absence causes dissatisfaction | Must include |
| **Performance** | More is better, linear satisfaction | Prioritize high-impact |
| **Delighters** | Unexpected, creates excitement | Include some for differentiation |

## Recommended Approach

1. Use **MoSCoW** for initial categorization
2. Apply **RICE** within Must/Should categories
3. Use **Value/Effort matrix** for visualization
4. Consider **Kano** for user experience balance
