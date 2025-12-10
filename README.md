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

## Quick Start

### Option 1: Create Project via Command (Recommended)

From within the ai-sdlc directory:
```bash
claude
> /init-project my-startup
```

This creates `projects/my-startup/` with ai-sdlc as a submodule.

### Option 2: Manual Setup

```bash
# Create your project
mkdir my-project && cd my-project
git init

# Add ai-sdlc as submodule
git submodule add https://github.com/YOUR_USERNAME/ai-sdlc.git

# Copy template files
cp ai-sdlc/templates/child-project/.claude/settings.json.template .claude/settings.json
cp ai-sdlc/templates/child-project/CLAUDE.md.template CLAUDE.md

# Start Claude Code
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
your-project/
├── ai-sdlc/                # Submodule - don't edit directly
├── .claude/
│   ├── settings.json       # Points to ai-sdlc skills
│   ├── commands/           # Project-specific commands
│   └── skills/             # Local skill overrides
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

When working in ai-sdlc (framework development):

| Command | Purpose |
|---------|---------|
| `/init-project <name>` | Create new project under projects/ |
| `/new-skill <name>` | Scaffold a new skill |
| `/validate-skill <path>` | Check skill structure |
| `/release <version>` | Create release, update all projects |

When working in a child project:

| Command | Purpose |
|---------|---------|
| `/update-sub-sdlc` | Pull latest ai-sdlc changes |
| `/update-sub-sdlc v1.2.0` | Checkout specific version |

## Updating ai-sdlc

In your project:
```bash
# Pull latest
/update-sub-sdlc

# Or checkout specific version
/update-sub-sdlc v1.2.0

# Commit the update
git add ai-sdlc
git commit -m "chore: update ai-sdlc to v1.2.0"
```

## Overriding Skills

To customize a skill for your project, create a local version:

```bash
# Create local skill directory
mkdir -p .claude/skills/product-manager

# Copy and modify
cp ai-sdlc/skills/product-manager/SKILL.md .claude/skills/product-manager/

# Edit to your needs
# The local version completely replaces the base
```

## License

MIT
