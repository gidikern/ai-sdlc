# Project Initialization Template

Use this template when starting a new project with AI SDLC.

## Directory Structure

```
project-name/
├── .claude/
│   └── settings.json          # Claude Code settings
├── docs/
│   ├── product/
│   │   ├── prd.md             # Product Requirements Document
│   │   ├── epics.md           # Epic definitions
│   │   ├── backlog.md         # Prioritized backlog
│   │   └── user-stories/      # Individual user stories
│   ├── architecture/
│   │   ├── architecture.md    # System architecture
│   │   ├── tech-spec.md       # Technical specification
│   │   ├── adr/               # Architecture Decision Records
│   │   │   └── README.md      # ADR index
│   │   ├── api/               # API specifications
│   │   └── diagrams/          # Architecture diagrams
│   └── reviews/               # Code review reports
├── src/                       # Source code
├── tests/                     # Test files
├── scripts/                   # Build/utility scripts
└── README.md                  # Project overview
```

## Setup Commands

```bash
# Create project structure
mkdir -p project-name/{.claude,docs/{product/user-stories,architecture/{adr,api,diagrams},reviews},src,tests,scripts}

# Create initial files
touch project-name/docs/product/{prd.md,epics.md,backlog.md}
touch project-name/docs/architecture/{architecture.md,tech-spec.md}
touch project-name/docs/architecture/adr/README.md
touch project-name/README.md
```

## Claude Code Settings

Create `.claude/settings.json`:

```json
{
  "skills": [
    {
      "path": "/path/to/ai-sdlc/skills/product-manager",
      "enabled": true
    },
    {
      "path": "/path/to/ai-sdlc/skills/architect",
      "enabled": true
    },
    {
      "path": "/path/to/ai-sdlc/skills/developer",
      "enabled": true
    },
    {
      "path": "/path/to/ai-sdlc/skills/reviewer",
      "enabled": true
    }
  ]
}
```

## Initial PRD Template

Create `docs/product/prd.md`:

```markdown
# Product Requirements Document: [Project Name]

**Version**: 0.1
**Date**: YYYY-MM-DD
**Status**: Draft

## Executive Summary
[To be filled by Product Manager agent]

## Problem Statement
[What problem are we solving?]

## Goals & Success Metrics
[How do we measure success?]

## Target Users
[Who are we building for?]

## Scope
### In Scope (MVP)
- TBD

### Out of Scope
- TBD

## Requirements
[To be elaborated with Product Manager agent]
```

## ADR Index Template

Create `docs/architecture/adr/README.md`:

```markdown
# Architecture Decision Records

| ADR | Title | Status | Date |
|-----|-------|--------|------|
| - | No decisions yet | - | - |
```
