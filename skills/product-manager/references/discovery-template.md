# Discovery Document Template

## File Location
`docs/product/discovery.md`

## Template

```markdown
# Discovery: [Product/Feature Name]

**Date**: YYYY-MM-DD
**Status**: In Progress | Complete | Abandoned

---

## 1. Problem Space

### Problem Statement
[1-2 sentences: What problem are we solving?]

### Who Has This Problem?
[Specific user segment - not "everyone"]

### Problem Evidence
- [How do we know this is a real problem?]
- [Data, interviews, observations]

### Current Alternatives
| Alternative | Pros | Cons | Why Not Enough? |
|-------------|------|------|-----------------|
| [Option 1] | | | |
| [Option 2] | | | |
| Do nothing | | | |

---

## 2. User Understanding

### Primary User Persona
**Who**: [Specific description]
**Context**: [When/where do they experience this problem?]
**Goal**: [What are they trying to accomplish?]
**Frustration**: [What's painful about current state?]

### User Journey (Current State)
1. [Step 1 - what they do today]
2. [Step 2]
3. [Pain point / friction]
4. [Step 3]

### Key Insights
- [Insight 1 from research/conversations]
- [Insight 2]
- [Insight 3]

---

## 3. Solution Exploration

### Solution Hypotheses
| Approach | Description | Pros | Cons | Effort |
|----------|-------------|------|------|--------|
| [A] | | | | |
| [B] | | | | |
| [C] | | | | |

### Recommended Direction
[Which approach and why]

### What "Good" Looks Like
[How would we know the solution is working?]

---

## 4. Assumptions & Risks

### Key Assumptions
| Assumption | Confidence | How to Validate |
|------------|------------|-----------------|
| [Assumption 1] | High/Med/Low | [Test approach] |
| [Assumption 2] | | |

### Biggest Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| [Risk 1] | | |
| [Risk 2] | | |

---

## 5. Decision

### Recommendation
[ ] **GO** - Proceed to Definition
[ ] **PIVOT** - Explore different direction
[ ] **STOP** - Not worth pursuing

### Rationale
[Why this decision?]

### Open Questions for Definition
- [Question 1]
- [Question 2]

### Open Questions for Architect
- [Technical question 1]
- [Technical question 2]

---

## Appendix

### Research Notes
[Links to interviews, data, competitive analysis]

### Discarded Ideas
[Ideas considered but rejected, and why - useful for future reference]
```

## Guidance

### Length
- Discovery doc should be **concise** - 1-3 pages max
- It's a thinking tool, not a comprehensive report
- If it's too long, you're in Definition mode

### When to Stop Discovery
Stop exploring when you can confidently fill in:
1. Problem statement (1-2 sentences)
2. Target user (specific segment)
3. Recommended approach (with rationale)
4. Key risks (top 2-3)

### Common Mistakes
- **Too vague**: "Users want a better experience" → What users? Better how?
- **Solution-first**: Starting with "build X" before understanding the problem
- **Boiling the ocean**: Trying to solve everything at once
- **Analysis paralysis**: Researching forever instead of deciding
