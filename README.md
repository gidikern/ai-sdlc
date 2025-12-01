# AI SDLC Framework

An AI-native Software Development Lifecycle framework powered by specialized Claude Code agents.

## Overview

This framework provides a structured approach to software development using AI agents with specialized roles. Each agent is a Claude Code skill with domain-specific knowledge, workflows, and tools.

## Agent Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      AI SDLC Workflow                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐ │
│  │ Product  │───▶│Architect │───▶│Developer │───▶│ Reviewer │ │
│  │ Manager  │    │          │    │          │    │          │ │
│  └──────────┘    └──────────┘    └──────────┘    └──────────┘ │
│       │              │               │               │         │
│       ▼              ▼               ▼               ▼         │
│    PRD.md        ADR/*.md        src/*           reviews/*     │
│    epics.md      architecture.md                              │
│    user-stories/ tech-spec.md                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Skills

| Skill | Role | Outputs |
|-------|------|---------|
| `product-manager` | Define vision, requirements, user stories | PRD, epics, user stories |
| `architect` | System design, tech decisions, API contracts | ADRs, architecture docs, tech specs |
| `developer` | Implementation, coding standards | Source code, tests |
| `reviewer` | Code review, quality assurance | Review reports, suggestions |

## Installation

Copy the `skills/` directory to your Claude Code skills location:

```bash
# For project-specific skills
cp -r skills/ /path/to/your/project/.claude/skills/

# Or for user-wide skills
cp -r skills/ ~/.claude/skills/
```

## Usage

Each skill is triggered by context. Examples:

```
User: "Let's define the product requirements for a health coaching app"
→ Triggers: product-manager skill

User: "Design the system architecture for this product"
→ Triggers: architect skill

User: "Implement the user authentication module"
→ Triggers: developer skill

User: "Review the authentication code"
→ Triggers: reviewer skill
```

## Project Structure

```
ai-sdlc/
├── README.md
├── skills/
│   ├── product-manager/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── prd-template.md
│   │       ├── user-story-template.md
│   │       └── prioritization.md
│   ├── architect/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── adr-template.md
│   │       ├── architecture-patterns.md
│   │       └── tech-evaluation.md
│   ├── developer/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── coding-standards.md
│   │       ├── testing-guide.md
│   │       └── commit-conventions.md
│   └── reviewer/
│       ├── SKILL.md
│       └── references/
│           ├── review-checklist.md
│           └── security-checklist.md
├── workflows/
│   ├── new-feature.md
│   ├── bug-fix.md
│   └── release.md
└── templates/
    └── project-init/
        ├── docs/
        └── .claude/
```

## Philosophy

1. **Agents are specialists** - Each agent focuses on their domain expertise
2. **Handoffs are explicit** - Clear deliverables between phases
3. **Documentation-driven** - All decisions and requirements are documented
4. **Iterative improvement** - The framework evolves with usage
