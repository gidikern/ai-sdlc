# Cross-Functional Discovery Workflow

A structured workflow for running collaborative discovery across multiple specialist perspectives, orchestrated by a neutral Facilitator.

## Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    CROSS-FUNCTIONAL DISCOVERY                                │
│                                                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                      PHASE A: PARALLEL ANALYSIS                      │   │
│  │                                                                       │   │
│  │   ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐                  │   │
│  │   │ PM  │ │ UX  │ │Arch │ │Legal│ │Growth│ │Data │                  │   │
│  │   └──┬──┘ └──┬──┘ └──┬──┘ └──┬──┘ └──┬──┘ └──┬──┘                  │   │
│  │      │       │       │       │       │       │                       │   │
│  │      └───────┴───────┴───────┴───────┴───────┘                       │   │
│  │                          │                                            │   │
│  │                          ▼                                            │   │
│  │                    FACILITATOR                                        │   │
│  │                    (Collects & Synthesizes)                          │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                │                                            │
│                                ▼                                            │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                    PHASE B: DEBATE & RESOLUTION                      │   │
│  │                         (If tensions exist)                          │   │
│  │                                                                       │   │
│  │     Facilitator identifies tensions → Routes to relevant specialists │   │
│  │     Specialists debate → Facilitator drives toward resolution        │   │
│  │     Unresolved items → Escalate to human                            │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                │                                            │
│                                ▼                                            │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                    PHASE C: ARTIFACT GENERATION                      │   │
│  │                                                                       │   │
│  │     Discovery Synthesis → Recommendations → Human Checkpoints        │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

## When to Use This Workflow

Use Cross-Functional Discovery when:
- Starting a new product or major initiative
- The problem space spans multiple disciplines (UX, tech, legal, business)
- You need diverse perspectives before committing to a direction
- Stakes are high enough to warrant thorough analysis

Don't use when:
- Simple feature addition with clear requirements
- Problem is well-understood and single-domain
- Time pressure requires quick decision (use standard discovery instead)

## Participants

### Required
| Role | Skill | Responsibility |
|------|-------|----------------|
| **Facilitator** | `facilitator` | Orchestrate, synthesize, escalate |
| **Product Manager** | `product-manager` | User needs, product strategy, MVP scope |

### Optional (Include Based on Topic)
| Role | Skill | Include When |
|------|-------|--------------|
| **UX Researcher** | `ux-researcher` | User experience is central |
| **Architect** | `architect` | Technical feasibility matters |
| **Legal Consultant** | `legal-consultant` | Compliance/regulatory concerns |
| **Growth Strategist** | `growth-strategist` | Acquisition/monetization is key |
| **Data Analyst** | `data-analyst` | Measurement/experimentation needed |

## Phase A: Parallel Analysis

### Objective
Get each specialist's independent perspective on the brief/topic before any cross-pollination.

### Process

1. **Facilitator parses the input**
   - Understand the brief/context
   - Identify which specialists are relevant
   - Frame domain-specific questions for each

2. **Route to specialists (in parallel)**
   ```
   For each relevant specialist:
   - Share the brief/context
   - Ask domain-specific questions
   - Request structured response (see skill templates)
   ```

3. **Collect structured responses**
   Each specialist returns:
   - Key findings
   - Concerns/risks
   - Recommendations
   - Questions for other specialists
   - Confidence level

### Example Specialist Prompts

**To Product Manager**:
> Review this brief from a product strategy perspective. What's the core value proposition? Who's the target user? What should be in/out of MVP scope? What are the key product risks?

**To UX Researcher**:
> Analyze the user experience implications. Who are the personas? What are their journeys? What are the key usability considerations? Where might users struggle?

**To Architect**:
> Assess technical feasibility. What are the major technical components? What are the key technical decisions? What are the technical risks and constraints?

**To Legal Consultant**:
> Evaluate legal and compliance risks. What regulations apply? What are the critical risks? What compliant alternatives exist?

**To Growth Strategist**:
> Analyze growth and monetization potential. What's the market opportunity? How should we acquire users? What's the monetization strategy?

**To Data Analyst**:
> Design the measurement approach. What should the North Star metric be? What experiments should we plan? What analytics infrastructure is needed?

### Output
Raw specialist analyses collected by Facilitator.

---

## Phase B: Debate & Resolution

### Objective
Identify tensions between specialists and drive toward resolution (or clear escalation).

### Process

1. **Facilitator synthesizes Phase A outputs**
   - Compile all specialist inputs
   - Identify areas of agreement (convergence)
   - Flag areas of disagreement (tensions)

2. **Categorize tensions by severity**

   | Severity | Example | Action |
   |----------|---------|--------|
   | Critical | "UX says feature X is essential, Legal says it's prohibited" | Must resolve |
   | High | "Growth wants aggressive monetization, PM wants free-first" | Debate needed |
   | Medium | "Different approaches, both could work" | Document options |
   | Low | "Minor emphasis differences" | Note and move on |

3. **Facilitate targeted debates (for Critical/High)**

   For each tension:
   ```
   a. Frame the tension clearly to relevant specialists
   b. Ask each party to:
      - Acknowledge the other's concern
      - Propose a compromise
      - State what would change their position
   c. Drive toward resolution or synthesis
   d. If no resolution after 2 rounds → escalate to human
   ```

4. **Document outcomes**
   - Resolved tensions with agreed position
   - Unresolved tensions for human review

### Debate Protocol

```markdown
## Tension: [Brief description]

**Specialists involved**: [List]

### Position A: [Specialist]
[Their position and rationale]

### Position B: [Specialist]
[Their position and rationale]

### Facilitator Frame
[How the facilitator frames the core conflict]

### Round 1
[Each party responds to the other, proposes compromise]

### Round 2 (if needed)
[Further refinement or impasse]

### Resolution
[Agreed position] OR [Escalate to human: reason]
```

### Output
Tensions resolved or clearly documented for human review.

---

## Phase C: Artifact Generation

### Objective
Produce the final discovery synthesis and actionable artifacts.

### Process

1. **Compile Discovery Synthesis**
   - Executive summary
   - Specialist perspectives (summarized)
   - Convergence points
   - Resolved tensions
   - Unresolved items (for human)
   - Recommendations

2. **Generate domain artifacts** (as appropriate)
   - Personas and journeys (UX)
   - Technical architecture sketch (Architect)
   - Risk assessment (Legal)
   - Metrics framework (Data)
   - Growth strategy (Growth)
   - PRD draft (PM)

3. **Human checkpoint**
   - Present synthesis
   - Request decisions on unresolved items
   - Get approval to proceed

### Output Artifacts

| Artifact | Location | Owner |
|----------|----------|-------|
| Discovery Synthesis | `docs/product/cross-functional-discovery.md` | Facilitator |
| Personas | `docs/product/personas/` | UX Researcher |
| Technical Assessment | `docs/architecture/feasibility.md` | Architect |
| Legal Risk Assessment | `docs/legal/risk-assessment.md` | Legal |
| Metrics Framework | `docs/product/metrics.md` | Data Analyst |
| Growth Strategy | `docs/product/growth-strategy.md` | Growth Strategist |

---

## Human Checkpoints

### Mandatory Checkpoints
Human review required at:
- End of Phase C (synthesis review)
- Any Critical-severity tension that can't be resolved
- Fundamental direction changes
- Budget/resource commitments

### Configurable Thresholds
```yaml
# discovery-config.yaml (conceptual)
human_escalation:
  confidence_threshold: 0.7  # Escalate if specialist confidence < this
  max_debate_rounds: 2       # Escalate if unresolved after N rounds
  always_escalate:
    - legal_red_flags
    - scope_changes_major
    - safety_concerns
```

### Escalation Format

```markdown
## Human Decision Required

### Context
[Brief summary]

### Decision Needed
[Specific question for human]

### Options

**Option A**: [Description]
- Supported by: [Specialists]
- Pros: [Benefits]
- Cons: [Drawbacks]

**Option B**: [Description]
- Supported by: [Specialists]
- Pros: [Benefits]
- Cons: [Drawbacks]

### Facilitator Recommendation
[If appropriate]

### Impact of Delay
[What happens if we don't decide now]
```

---

## Example: Running Discovery on Health Coach Brief

### Setup
```
Input: brief-ai-health-coach-dtc.md
Specialists: PM, UX, Architect, Legal, Growth, Data
```

### Phase A Prompts

**PM**: "Review this health coach brief. What's the core product vision? Who's the primary user? What's MVP scope?"

**UX**: "Analyze the user experience. What personas emerge? What's the critical user journey? Where are the UX risks?"

**Architect**: "Assess technical feasibility. What's the AI architecture? What are the integration needs? Technical risks?"

**Legal**: "Evaluate legal risks. This is a health app - what regulations apply? What are the compliance must-haves?"

**Growth**: "Analyze growth potential. What's the acquisition strategy for a DTC health app? Monetization model?"

**Data**: "Design measurement framework. What's the North Star? What experiments should we run? Analytics needs?"

### Potential Tensions to Anticipate

1. **UX vs Legal**: Minimal onboarding vs. required consent flows
2. **Growth vs PM**: Aggressive monetization vs. value-first free tier
3. **PM vs Architect**: Feature scope vs. technical complexity
4. **Legal vs Growth**: Health claims restrictions vs. marketing messaging

---

## Quick Reference

### Phase Triggers

| Situation | Phase |
|-----------|-------|
| Starting discovery, have brief | A (Parallel Analysis) |
| Have specialist inputs, need synthesis | B (Debate) or C (Artifacts) |
| Specialists disagree | B (Debate) |
| Ready to document | C (Artifacts) |
| Need human decision | Escalate |

### Typical Duration

| Complexity | Phase A | Phase B | Phase C | Total |
|------------|---------|---------|---------|-------|
| Simple | 30 min | 0 | 30 min | 1 hour |
| Medium | 1 hour | 30 min | 1 hour | 2.5 hours |
| Complex | 2 hours | 1 hour | 2 hours | 5 hours |

### Anti-Patterns

| Pattern | Problem | Fix |
|---------|---------|-----|
| Skipping Phase A | Groupthink, missed perspectives | Always do parallel analysis |
| Endless Phase B | Analysis paralysis | Time-box debates, escalate |
| No human checkpoints | Risky decisions made without oversight | Build in mandatory reviews |
| Too many specialists | Slow, unfocused | Only include relevant ones |
