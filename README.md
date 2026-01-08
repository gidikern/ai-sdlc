# AI SDLC Framework

An AI-native Software Development Lifecycle framework powered by specialized Claude Code agents.

## Philosophy

1. **Think before you build** - Strong discovery and definition before any code
2. **Agents are specialists** - Each agent focuses on their domain expertise
3. **Explicit handoffs** - Clear deliverables between phases
4. **Documentation-driven** - All decisions and requirements are documented
5. **Iterative improvement** - The framework evolves with real usage

## Core Workflow

```
┌─────────────────────────────────────────────────────────────────────┐
│                    FOUNDATION PHASE                                  │
│                                                                      │
│   Product Manager         Legal Consultant        Architect          │
│   ┌─────────────┐         ┌─────────────┐      ┌─────────────┐      │
│   │  Discovery  │────────▶│    Risk     │─────▶│ Architecture│      │
│   │   Mode      │         │  Assessment │      │             │      │
│   └─────────────┘         └─────────────┘      └─────────────┘      │
│         │                       │                    │               │
│         ▼                       ▼                    ▼               │
│    discovery.md           risk-assessment.md    architecture.md     │
│    prd.md                                       adr/*.md            │
│    user-stories/                                tech-spec.md        │
└─────────────────────────────────────────────────────────────────────┘
                              │
                              │ Only when foundation is solid
                              ▼
┌─────────────────────────────────────────────────────────────────────┐
│                  IMPLEMENTATION PHASE                                │
│                                                                      │
│   ┌─────────────┐                          ┌─────────────┐          │
│   │  Developer  │─────────────────────────▶│  Reviewer   │          │
│   └─────────────┘                          └─────────────┘          │
│         │                                        │                  │
│         ▼                                        ▼                  │
│      src/*                                   reviews/*              │
│      tests/*                                                        │
└─────────────────────────────────────────────────────────────────────┘
```

## Agents

| Agent | Role | Focus Areas |
|-------|------|-------------|
| **Product Manager** | Define what to build and why | Discovery Mode → Definition Mode |
| **Legal Consultant** | Identify legal risks early | Compliance, regulations, jurisdictions |
| **Architect** | Design how to build it | System design, tech decisions, APIs |
| **Developer** | Implement the solution | Code, tests, documentation |
| **Reviewer** | Ensure quality | Code review, security, standards |
| **Facilitator** | Coordinate collaboration | Meetings, decision-making, alignment |
| **UX Researcher** | Understand users | Research, testing, personas |
| **Growth Strategist** | Drive growth | Marketing, metrics, strategy |
| **Data Analyst** | Extract insights | Analysis, reporting, metrics |
| **Performance Marketer** | Growth-first optimization | Rapid experiments, conversion, paid acquisition |

## Quick Start

### Create a New Project

From within the ai-sdlc directory:
```bash
claude
> /init-project my-startup
```

This creates `projects/my-startup/` with:
- Own git repo and GitHub remote
- Skills inherited via relative paths (`../../skills/`)
- Workflow commands and files synced from parent
- Registered for automatic updates during `/release`

Then start working:
```bash
cd projects/my-startup
claude
```

### Start Building

```bash
# 1. Discovery
> "I want to build a health coaching app"
→ Product Manager explores problem, users, market

# 2. Legal Review (especially for regulated domains)
> "Review this concept for legal risks"
→ Legal Consultant identifies compliance concerns

# 3. Definition
> "Let's define what we're building"
→ Product Manager creates PRD, user stories

# 4. Architecture
> "Design the architecture"
→ Architect creates system design, ADRs

# 5. Implementation
> "Implement the user authentication"
→ Developer writes code, tests
```

## Project Structure

```
ai-sdlc/                    # Framework (parent)
├── skills/                 # 9 specialist agents
├── workflows/              # Multi-phase workflows
├── .claude/
│   ├── commands/           # Framework + workflow commands
│   └── siblings.json       # Tracks child projects
└── projects/               # Your projects (gitignored)
    └── your-project/
        ├── .claude/
        │   ├── settings.json    # References ../../skills/
        │   ├── commands/        # Workflow commands (synced)
        │   ├── workflows/       # Workflow files (synced)
        │   └── skills/          # Local skill overrides
        ├── docs/
        │   ├── product/
        │   │   ├── discovery.md    # Problem exploration
        │   │   ├── prd.md          # Product requirements
        │   │   └── user-stories/   # Detailed stories
        │   ├── architecture/
        │   │   ├── architecture.md # System design
        │   │   ├── tech-spec.md    # Technical details
        │   │   └── adr/            # Decision records
        │   ├── legal/
        │   │   ├── risk-assessment.md
        │   │   └── compliance-checklist.md
        │   └── reviews/            # Code review reports
        ├── src/                    # Source code
        └── tests/                  # Test files
```

## Commands

### Framework Management (ai-sdlc directory only)

| Command | Purpose |
|---------|---------|
| `/init-project <name>` | Create new project under projects/ |
| `/release <version>` | Tag release and sync to child projects |
| `/new-skill <name>` | Scaffold a new skill |
| `/validate-skill <path>` | Check skill structure |
| `/prepare-release` | Review commits and update CHANGELOG |

### Workflow Commands (available in all projects)

| Command | Purpose |
|---------|---------|
| `/cross-functional-discovery` | Multi-agent discovery process |

## Getting Updates

Child projects automatically receive updates when you run `/release` in the ai-sdlc directory:
- New/updated skills added to `.claude/settings.json`
- New/updated workflow commands synced to `.claude/commands/`
- New/updated workflow files synced to `.claude/workflows/`

The `/release` command asks for approval before updating each project.

## Overriding Skills

To customize a skill for your project, create a local version in `.claude/skills/`:

```bash
# From your project directory (e.g., projects/my-startup/)
mkdir -p .claude/skills/product-manager

# Copy from parent
cp ../../skills/product-manager/SKILL.md .claude/skills/product-manager/

# Edit to your needs
# The local version completely replaces the inherited one
```

Skills are inherited via relative paths in `.claude/settings.json`:
```json
{
  "skills": [
    { "path": "../../skills/product-manager" },
    { "path": "./.claude/skills" }  // Local overrides
  ]
}
```

## License

MIT
