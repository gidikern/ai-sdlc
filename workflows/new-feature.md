# New Feature Workflow

End-to-end workflow for implementing a new feature from idea to deployment.

## Workflow Diagram

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   Product    │────▶│  Architect   │────▶│  Developer   │────▶│   Reviewer   │
│   Manager    │     │              │     │              │     │              │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
      │                    │                    │                    │
      ▼                    ▼                    ▼                    ▼
   PRD.md              ADR-xxx.md           src/*              review.md
   user-stories/       tech-spec.md         tests/*            
```

## Phase 1: Product Definition

**Agent**: Product Manager
**Trigger**: "Let's add a new feature for..."

### Activities
1. Clarify requirements through conversation
2. Create/update PRD
3. Write user stories with acceptance criteria
4. Prioritize within backlog
5. Define MVP scope

### Deliverables
- `docs/product/prd.md` (updated)
- `docs/product/user-stories/FEAT-xxx.md`
- `docs/product/backlog.md` (updated)

### Handoff Criteria
- [ ] User stories have clear acceptance criteria
- [ ] MVP scope is defined
- [ ] Dependencies identified
- [ ] Stakeholder approval (if needed)

## Phase 2: Architecture & Design

**Agent**: Architect
**Trigger**: "Design the architecture for..."

### Activities
1. Review PRD and user stories
2. Design system/component architecture
3. Evaluate and select technologies
4. Document decisions in ADRs
5. Create technical specification

### Deliverables
- `docs/architecture/adr/ADR-xxx.md`
- `docs/architecture/tech-spec.md` (updated)
- `docs/architecture/diagrams/` (if needed)
- `docs/architecture/api/` (if new endpoints)

### Handoff Criteria
- [ ] Architecture fits within system design
- [ ] Technology choices documented
- [ ] API contracts defined
- [ ] Technical risks identified

## Phase 3: Implementation

**Agent**: Developer
**Trigger**: "Implement the feature..."

### Activities
1. Review tech spec and user stories
2. Set up development environment
3. Implement code following standards
4. Write unit and integration tests
5. Update documentation

### Deliverables
- Source code in `src/`
- Tests in `tests/` or `*.test.*`
- Updated README/docs if needed

### Handoff Criteria
- [ ] All acceptance criteria met
- [ ] Tests pass
- [ ] Code follows standards
- [ ] No linting errors
- [ ] Self-review completed

## Phase 4: Review

**Agent**: Reviewer
**Trigger**: "Review the implementation..."

### Activities
1. Review code changes
2. Run security checklist
3. Verify test coverage
4. Check documentation
5. Provide feedback

### Deliverables
- `reviews/YYYY-MM-DD-FEAT-xxx.md`
- PR comments (if using PR workflow)

### Outcomes
- **Approved**: Ready for merge
- **Changes Requested**: Return to Phase 3
- **Needs Discussion**: Escalate to Architect

## Iteration Loop

```
If review feedback requires changes:
  → Developer addresses feedback
  → Reviewer re-reviews
  → Repeat until approved

If review reveals design issues:
  → Escalate to Architect
  → Update design
  → Return to Developer
```

## Quick Start Command

```
User: "I want to add [feature description]"

AI SDLC will:
1. Product Manager: Gather requirements, write user stories
2. Architect: Design solution, create ADRs
3. Developer: Implement and test
4. Reviewer: Review and approve
```
