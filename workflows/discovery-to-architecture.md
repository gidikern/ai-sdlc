# Discovery to Architecture Workflow

The foundational workflow for starting any new product or major feature. Ensures solid thinking before any code is written.

## Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                    FOUNDATION PHASE                                  │
│                                                                      │
│   ┌─────────────┐      ┌─────────────┐      ┌─────────────┐        │
│   │  Discovery  │─────▶│ Definition  │─────▶│ Architecture│        │
│   │             │      │             │      │             │        │
│   │  Explore    │      │  Document   │      │  Design     │        │
│   │  Question   │      │  Decide     │      │  Specify    │        │
│   │  Learn      │      │  Scope      │      │  Plan       │        │
│   └─────────────┘      └─────────────┘      └─────────────┘        │
│         │                    │                    │                 │
│         ▼                    ▼                    ▼                 │
│    discovery.md          prd.md              architecture.md       │
│                       user-stories/          adr/*.md              │
│                                              tech-spec.md          │
│                                                                      │
│   ◀──────────────── ITERATE AS NEEDED ────────────────▶            │
└─────────────────────────────────────────────────────────────────────┘
                              │
                              │ Only when foundation is solid
                              ▼
                    ┌─────────────────┐
                    │ Implementation  │
                    │     Phase       │
                    └─────────────────┘
```

## Phase 1: Discovery

**Agent**: Product Manager (Discovery Mode)
**Trigger**: "Let's explore...", "I want to build...", "Help me think through..."
**Duration**: 1-3 sessions depending on complexity

### Objectives
- Understand the problem deeply
- Identify target users specifically  
- Explore solution approaches
- Surface assumptions and risks

### Activities

```
Session Flow:
1. Problem Framing (What? Who? Why?)
      ↓
2. User Deep-Dive (Context, needs, current behavior)
      ↓
3. Solution Exploration (Options, trade-offs)
      ↓
4. Risk Assessment (Assumptions, unknowns)
      ↓
5. Go/No-Go Decision
```

### Key Questions to Answer

| Question | Bad Answer | Good Answer |
|----------|------------|-------------|
| Who is this for? | "Anyone who wants to be healthy" | "Busy professionals 30-45 who want to lose weight but struggle with consistency" |
| What problem? | "Health tracking" | "Users forget to log meals and lose motivation after 2 weeks" |
| Why you/now? | "It's a good idea" | "AI can now provide personalized coaching at scale" |
| How do you win? | "Better features" | "Focus on habit formation, not just tracking" |

### Deliverable
`docs/product/discovery.md`

### Exit Criteria
- [ ] Problem statement is crisp (1-2 sentences)
- [ ] Target user is specific (not "everyone")
- [ ] Recommended approach selected
- [ ] Key assumptions identified
- [ ] Decision: GO / PIVOT / STOP

---

## Phase 2: Definition

**Agent**: Product Manager (Definition Mode)
**Trigger**: Discovery complete, "Let's define...", "Write the PRD..."
**Duration**: 1-2 sessions

### Objectives
- Document product requirements
- Define MVP scope ruthlessly
- Create actionable user stories
- Prioritize for implementation

### Activities

```
1. Vision & Goals
   └─▶ Problem statement, success metrics, non-goals
        ↓
2. MVP Scoping
   └─▶ In/Out list, must-have vs nice-to-have
        ↓
3. User Stories
   └─▶ Stories with acceptance criteria
        ↓
4. Prioritization
   └─▶ Ordered backlog for MVP
```

### MVP Scoping Framework

```
                    ┌─────────────────┐
                    │   MUST HAVE     │ ← Without this, product fails
                    │   (MVP Core)    │
                    ├─────────────────┤
                    │   SHOULD HAVE   │ ← Important, but can launch without
                    │   (MVP+)        │
                    ├─────────────────┤
                    │   COULD HAVE    │ ← Nice to have
                    │   (Future)      │
                    ├─────────────────┤
                    │   WON'T HAVE    │ ← Explicitly out of scope
                    │   (Not Now)     │
                    └─────────────────┘
```

### Deliverables
- `docs/product/prd.md`
- `docs/product/user-stories/*.md`
- `docs/product/backlog.md`

### Exit Criteria
- [ ] PRD complete
- [ ] MVP scope crystal clear (explicit in/out)
- [ ] User stories have acceptance criteria
- [ ] Stories are small enough (days, not weeks)
- [ ] Priority order defined
- [ ] Open questions for Architect listed

---

## Phase 3: Architecture

**Agent**: Architect
**Trigger**: PRD complete, "Design the architecture...", "How should we build..."
**Duration**: 1-3 sessions depending on complexity

### Objectives
- Design system architecture
- Make and document technology choices
- Define data models and APIs
- Identify technical risks

### Activities

```
1. Requirements Analysis
   └─▶ Review PRD, identify NFRs, clarify with PM
        ↓
2. High-Level Design
   └─▶ System context, major components, data flow
        ↓
3. Technology Decisions
   └─▶ Stack selection, ADRs for key decisions
        ↓
4. Detailed Design
   └─▶ Data models, API contracts, component specs
        ↓
5. Implementation Planning
   └─▶ Technical stories, dev environment, risks
```

### Architecture Checklist

| Area | Questions to Answer |
|------|---------------------|
| **Data** | What entities? How stored? How related? |
| **APIs** | What endpoints? Auth? Rate limits? |
| **Components** | What services/modules? How do they communicate? |
| **Infrastructure** | Where hosted? How deployed? How scaled? |
| **Security** | Auth method? Data encryption? Compliance? |
| **Integration** | External services? AI/ML? Third-party APIs? |

### Deliverables
- `docs/architecture/architecture.md`
- `docs/architecture/adr/*.md`
- `docs/architecture/tech-spec.md`
- `docs/architecture/data-models.md`
- `docs/architecture/api/` (OpenAPI specs if applicable)

### Exit Criteria
- [ ] Architecture documented and reviewed
- [ ] Key technology decisions made (with ADRs)
- [ ] Data model defined
- [ ] API contracts specified
- [ ] Security approach defined
- [ ] Development environment specified
- [ ] Technical risks identified

---

## Iteration & Feedback Loops

### Discovery ↔ Definition
```
If during Definition you realize:
- Problem isn't clear → Back to Discovery
- Scope is too big → Revisit MVP in Definition
- New user insight → Update Discovery doc
```

### Definition ↔ Architecture  
```
If during Architecture you discover:
- Technical impossibility → Back to Definition, adjust scope
- Compliance requirement → Update PRD constraints
- Simpler approach → Propose to PM, update stories
```

### The "One More Question" Rule
Before moving to next phase, ask: "What's the one thing that, if wrong, would derail everything?"

---

## Quick Reference

### Phase Triggers

| You say... | Phase |
|------------|-------|
| "I have an idea for..." | Discovery |
| "Help me understand if..." | Discovery |
| "Let's define what we're building" | Definition |
| "Write the PRD" | Definition |
| "How should we build this?" | Architecture |
| "What tech stack?" | Architecture |

### Time Investment (Typical)

| Product Size | Discovery | Definition | Architecture |
|--------------|-----------|------------|--------------|
| Small feature | 30 min | 1 hour | 1 hour |
| Medium feature | 1-2 hours | 2-3 hours | 2-4 hours |
| New product | 2-4 hours | 4-8 hours | 4-8 hours |

### Anti-Patterns to Avoid

| Anti-Pattern | Problem | Fix |
|--------------|---------|-----|
| Skipping Discovery | Building the wrong thing | Always start with "why" |
| Endless Discovery | Analysis paralysis | Set time box, force decision |
| Vague MVP | Scope creep | Explicit in/out list |
| Architecture Astronaut | Over-engineering | Start simple, evolve |
| No ADRs | Forgotten decisions | Document as you decide |
