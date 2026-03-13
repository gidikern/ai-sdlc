# AI-SDLC Framework

This project IS the AI-native Software Development Lifecycle framework. These instructions guide development of the framework itself.

## Project Purpose

Provide reusable AI agent skills, workflows, and commands that other projects inherit via relative paths in a simple parent/child directory structure.

## Architecture

```
ai-sdlc/                      # Framework (this repo)
├── .claude/
│   ├── settings.json         # Framework's own skill configuration
│   ├── siblings.json         # Tracks child projects for sync
│   ├── skills/               # 10 specialist agent definitions
│   │   ├── product-manager/
│   │   ├── architect/
│   │   ├── developer/
│   │   ├── reviewer/
│   │   ├── legal-consultant/
│   │   ├── facilitator/
│   │   ├── ux-researcher/
│   │   ├── growth-strategist/
│   │   ├── data-analyst/
│   │   └── performance-marketer/
│   ├── commands/             # Framework + workflow commands
│   │   ├── init-project.md          # Framework: Create new project
│   │   ├── release.md               # Framework: Tag release & sync
│   │   ├── new-skill.md             # Framework: Scaffold skill
│   │   ├── validate-skill.md        # Framework: Check skill quality
│   │   ├── prepare-release.md       # Framework: Update CHANGELOG
│   │   └── cross-functional-discovery.md  # Workflow: Synced to projects
│   └── workflows/            # Workflow files (synced to projects)
│       ├── cross-functional-discovery.md
│       ├── discovery-to-architecture.md
│       └── new-feature.md
├── templates/
│   └── child-project/        # Templates for /init-project
└── projects/                 # Child projects (gitignored)
    ├── my-startup/           # Each has own git repo
    └── another-app/

Child Project Structure:
projects/my-startup/
├── .claude/
│   ├── settings.json         # References ../../.claude/skills/
│   ├── commands/             # Workflow commands (synced from parent)
│   ├── workflows/            # Workflow files (synced from parent)
│   └── skills/               # Local overrides — prefix _ = local only
│       └── _my-local-skill/
├── docs/
│   ├── product/
│   ├── architecture/
│   └── legal/
├── src/
└── tests/
```

### `_` Prefix Convention

Everything lives under `.claude/` — skills, commands, and workflows follow the same rule:

| | Shared (synced to siblings) | Local only (never synced) |
|---|---|---|
| Skills | `.claude/skills/name/` | `.claude/skills/_name/` |
| Commands | `.claude/commands/name.md` | `.claude/commands/_name.md` |
| Workflows | `.claude/workflows/name.md` | `.claude/workflows/_name.md` |

## Project Management

### Creating Projects

Use `/init-project <name>` to create a new child project:

```bash
/init-project my-startup
```

This creates `projects/my-startup/` with:
- Own git repo and GitHub remote
- Skills inherited via relative paths (`../../.claude/skills/`)
- Workflow commands copied to `.claude/commands/`
- Workflow files copied to `.claude/workflows/`
- Registered in `.claude/siblings.json` for future syncing

**Key distinction:**
- **Framework commands** (`/init-project`, `/release`, etc.) stay in parent only
- **Workflow commands** (`/cross-functional-discovery`, etc.) are copied to child projects

### Syncing to Projects

When you add/update skills, workflow commands, or workflows:

1. **Make changes** in ai-sdlc
2. **Commit and push** to GitHub
3. **Run `/release v1.x.x`** to tag the release
4. **Sync happens automatically:**
   - Checks each project with `autoUpdate: true`
   - Identifies missing/updated items across THREE categories:
     - **Skills**: Missing skill paths in `.claude/settings.json`
     - **Workflow commands**: Missing/updated `.md` files in `.claude/commands/`
     - **Workflow files**: Missing/updated `.md` files in `.claude/workflows/`
   - Asks for approval per project
   - Updates and commits changes to approved projects

**Important:** Sync is cumulative - it checks for ALL missing items, not just newly added ones.

### siblings.json

Located at `.claude/siblings.json`, this file tracks child projects for syncing:

```json
{
  "description": "Projects managed by ai-sdlc. Used by /release to sync skills, commands, and workflows.",
  "projects": [
    { "path": "./projects/my-startup", "autoUpdate": true },
    { "path": "./projects/experimental", "autoUpdate": false }
  ]
}
```

- **`autoUpdate: true`**: Check for missing/updated items during `/release` and ask to sync
- **`autoUpdate: false`**: Skip this project during release (manual updates only)
- Automatically maintained by `/init-project` (adds new projects with `autoUpdate: true`)

## Development Guidelines

### Modifying Skills

1. Skills are in `.claude/skills/<name>/SKILL.md`
2. Keep SKILL.md under 500 lines - use `references/` for details
3. Test changes on a real project before committing
4. Update CHANGELOG.md
5. Run `/validate-skill` to check structure

### Creating New Skills

Use command: `/new-skill <name>`

This will:
1. Create `.claude/skills/<name>/SKILL.md` with template
2. Create `.claude/skills/<name>/references/` directory
3. Remind you to register in settings files

After creation, you must manually:
1. Fill in SKILL.md content
2. Add to `.claude/settings.json` (framework)
3. Add to `templates/child-project/.claude/settings.json.template` (for new projects)
4. Update CHANGELOG.md
5. Update README.md (agents table)
6. Update this file (CLAUDE.md) if the skill list in Architecture section needs updating

**Note:** Existing projects get new skills via `/release` sync, not retroactively.

### Creating Commands

Commands go in `.claude/commands/<name>.md`. There are two types:

#### Framework Commands
Management commands that stay in parent only:
- `/init-project` - Create new project
- `/release` - Tag release and sync to projects
- `/new-skill` - Scaffold new skill
- `/validate-skill` - Check skill structure
- `/prepare-release` - Review commits, update CHANGELOG

These are NOT synced to child projects during `/release`.

#### Workflow Commands
Process commands that get synced to child projects:
- `/cross-functional-discovery` - Multi-agent discovery workflow
- (Add more workflow commands here)

These ARE synced to child projects during `/init-project` and `/release`.

**Command Template:**
```markdown
# /command-name

Description of what this command does.

## Usage
/command-name <args>

## Behavior
[Instructions for Claude when command is invoked]
```

**Syncing new workflow commands:**
1. Create `.claude/commands/my-workflow.md` in parent
2. Commit and push
3. Run `/release v1.x.x` to sync to all projects with `autoUpdate: true`

### Creating Workflows

Workflow files document multi-phase processes and go in `workflows/<name>.md`:
- `discovery-to-architecture.md` - Full pre-implementation flow
- `new-feature.md` - Adding features to existing projects
- `cross-functional-discovery.md` - Multi-specialist discovery process

**Workflow files vs Workflow commands:**
- **Workflow files** (`workflows/*.md`): Documentation/reference for processes
- **Workflow commands** (`.claude/commands/*.md`): Executable commands that may reference workflow files

Both are synced to child projects via `/init-project` and `/release`:
- Workflow files → `projects/my-app/.claude/workflows/`
- Workflow commands → `projects/my-app/.claude/commands/`

### Versioning

We use semantic versioning with git tags:

- **MAJOR** (v2.0.0): Breaking changes to skill interfaces
- **MINOR** (v1.1.0): New skills, workflows, or backward-compatible changes
- **PATCH** (v1.0.1): Bug fixes, documentation updates

To release:
```bash
# 1. Prepare CHANGELOG (review commits, update [Unreleased])
/prepare-release

# 2. Create release (moves [Unreleased] to version, tags, pushes, updates projects)
/release v1.x.x
```

### Quality Checklist

Before committing skill changes:
- [ ] SKILL.md has valid frontmatter (name, description)
- [ ] Description clearly states when to trigger
- [ ] Instructions are actionable, not vague
- [ ] References exist for detailed content
- [ ] Tested on real project usage
- [ ] Registered in both settings files (`.claude/settings.json` and `templates/.../settings.json.template`)
- [ ] CHANGELOG.md updated
- [ ] README.md agents table updated (if new skill)
- [ ] CLAUDE.md Architecture section updated (if needed)

Before committing workflow/command changes:
- [ ] Workflow files placed in `workflows/`
- [ ] Workflow commands placed in `.claude/commands/`
- [ ] Framework vs workflow distinction clear
- [ ] CHANGELOG.md updated
- [ ] Tested on at least one child project

## Commands

### Framework Commands (Parent Only)

| Command | Purpose | Location |
|---------|---------|----------|
| `/init-project <name>` | Create new project under projects/ | ai-sdlc only |
| `/release <version>` | Tag release and sync to child projects | ai-sdlc only |
| `/new-skill <name>` | Scaffold a new skill | ai-sdlc only |
| `/validate-skill <path>` | Check skill structure and quality | ai-sdlc only |
| `/prepare-release` | Review commits and update CHANGELOG | ai-sdlc only |

### Workflow Commands (Synced to Projects)

| Command | Purpose | Location |
|---------|---------|----------|
| `/cross-functional-discovery` | Multi-agent discovery process | Synced to projects |

**Note:** Workflow commands are copied to child projects during `/init-project` and kept in sync via `/release`.

## Documentation Responsibilities

| File | Updated By | When |
|------|------------|------|
| `CHANGELOG.md` | Manual or `/prepare-release` | Before every release |
| `README.md` | Manual | New skills, workflow changes |
| `CLAUDE.md` | Manual | Framework structure changes, new skills |
| `.claude/settings.json` | Manual | New skills (framework config) |
| `templates/.../settings.json.template` | Manual | New skills (for new projects) |
| `.claude/siblings.json` | `/init-project` (auto) | New projects added |
| `workflows/*.md` | Manual | New/updated workflow files |

## Available Skills

The framework currently provides 10 specialist agent skills:

| Skill | Purpose |
|-------|---------|
| `product-manager` | Discovery Mode → Definition Mode, PRDs, user stories |
| `architect` | System design, ADRs, tech evaluation, domain modeling |
| `developer` | Implementation, coding standards, testing |
| `reviewer` | Code review, security review, quality assurance |
| `legal-consultant` | Legal risk assessment, compliance, regulations |
| `facilitator` | Meeting coordination, collaboration, decision facilitation |
| `ux-researcher` | User research, usability testing, persona development |
| `growth-strategist` | Marketing strategy, growth tactics, metrics |
| `data-analyst` | Data analysis, metrics, reporting, insights |
| `performance-marketer` | Growth-first optimization, rapid experiments, conversion |

All skills are inherited by child projects via relative paths (`../../.claude/skills/`) in `.claude/settings.json`.

## Key Architecture Principles

1. **Simple parent/child structure** - No git submodules, just relative paths
2. **Centralized skills** - All skills live in parent, inherited by children
3. **Synced workflows** - Workflow files and commands automatically synced to projects
4. **Local overrides** - Projects can override any skill in `.claude/skills/`
5. **Cumulative sync** - `/release` checks for ALL missing items, not just new ones
6. **Two command types** - Framework commands (parent only) vs workflow commands (synced)
