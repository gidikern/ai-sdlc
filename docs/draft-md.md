

1. Cost of change curve

Cost to fix
    │
    │                                    ████
    │                              ████
    │                        ████
    │                  ▓▓▓▓
    │            ░░░░
    │      ....
    └──────────────────────────────────────────
       Idea → PRD → Design → Code → Production

Mistakes caught in PRD cost almost nothing. Mistakes caught in production cost everything.


Strengthen the Product Manager → Architect pipeline before touching Developer/Reviewer:
┌─────────────────────────────────────────────────────────┐
│              PHASE 1: Foundation (Polish Now)           │
│  ┌──────────────┐         ┌──────────────┐              │
│  │   Product    │────────▶│  Architect   │              │
│  │   Manager    │         │              │              │
│  └──────────────┘         └──────────────┘              │
│        │                        │                       │
│        ▼                        ▼                       │
│   • Vision & Why           • How it works               │
│   • User needs             • Tech choices               │
│   • MVP scope              • Data model                 │
│   • Success metrics        • API contracts              │
└─────────────────────────────────────────────────────────┘
                         │
                         │ Only after foundation is solid
                         ▼
┌─────────────────────────────────────────────────────────┐
│              PHASE 2: Implementation (Later)            │
│  ┌──────────────┐         ┌──────────────┐              │
│  │  Developer   │────────▶│   Reviewer   │              │
│  └──────────────┘         └──────────────┘              │
└─────────────────────────────────────────────────────────┘


Split Product Manager into 2 Modes
Instead of 2 separate agents, make one Product agent with 2 distinct modes:
┌─────────────────────────────────────────────────────────┐
│                    Product Agent                        │
│  ┌─────────────────┐       ┌─────────────────┐          │
│  │  Discovery Mode │──────▶│ Definition Mode │          │
│  │                 │       │                 │          │
│  │  • Explore      │       │  • Document     │          │
│  │  • Question     │       │  • Specify      │          │
│  │  • Research     │       │  • Prioritize   │          │
│  │  • Challenge    │       │  • Scope        │          │
│  └─────────────────┘       └─────────────────┘          │
│           │                        │                    │
│           ▼                        ▼                    │
│     Discovery Doc              PRD + Stories            │
└─────────────────────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│                   Architect Agent                       │
│  • System design                                        │
│  • Tech decisions                                       │
│  • Data modeling                                        │
│  • API contracts                                        │
└─────────────────────────────────────────────────────────┘