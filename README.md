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
│   Product Manager                          Architect                 │
│   ┌─────────────┐      ┌─────────────┐      ┌─────────────┐        │
│   │  Discovery  │─────▶│ Definition  │─────▶│ Architecture│        │
│   │   Mode      │      │   Mode      │      │             │        │
│   └─────────────┘      └─────────────┘      └─────────────┘        │
│         │                    │                    │                 │
│         ▼                    ▼                    ▼                 │
│    discovery.md          prd.md              architecture.md       │
│                       user-stories/          adr/*.md              │
│                                              tech-spec.md          │
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

| Agent | Role | Modes/Focus |
|-------|------|-------------|
| **Product Manager** | Define what to build and why | Discovery Mode → Definition Mode |
| **Architect** | Design how to build it | System design, tech decisions, APIs |
| **Developer** | Implement the solution | Code, tests, documentation |
| **Reviewer** | Ensure quality | Code review, security, standards |

## Workflows

| Workflow | When to Use |
|----------|-------------|
| `discovery-to-architecture.md` | Starting a new product or major feature |
| `new-feature.md` | Adding features to existing product |

## Quick Start

### 1. Start Discovery
```
"I want to build a health coaching app"
→ Product Manager (Discovery Mode) activates
→ Explores problem, users, solution space
→ Creates discovery.md
```

### 2. Define Product
```
"Let's define what we're building"
→ Product Manager (Definition Mode) activates
→ Creates PRD, user stories, backlog
→ Hands off to Architect
```

### 3. Design Architecture
```
"Design the architecture"
→ Architect activates
→ Creates architecture docs, ADRs, tech spec
→ Ready for implementation
```

## Project Structure

```
your-project/
├── .claude/
│   └── settings.json       # Points to ai-sdlc skills
├── docs/
│   ├── product/
│   │   ├── discovery.md    # Problem exploration
│   │   ├── prd.md          # Product requirements
│   │   ├── backlog.md      # Prioritized work
│   │   └── user-stories/   # Detailed stories
│   ├── architecture/
│   │   ├── architecture.md # System design
│   │   ├── tech-spec.md    # Technical details
│   │   ├── adr/            # Decision records
│   │   └── api/            # API specs
│   └── reviews/            # Code review reports
├── src/                    # Source code
└── tests/                  # Test files
```

## Installation

```bash
# Clone this repo
git clone https://github.com/YOUR_USERNAME/ai-sdlc.git

# In your project, create .claude/settings.json:
{
  "skills": [
    { "path": "/path/to/ai-sdlc/skills/product-manager" },
    { "path": "/path/to/ai-sdlc/skills/architect" },
    { "path": "/path/to/ai-sdlc/skills/developer" },
    { "path": "/path/to/ai-sdlc/skills/reviewer" }
  ]
}
```
