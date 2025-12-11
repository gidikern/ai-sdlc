# Changelog

All notable changes to ai-sdlc will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- (none yet)

### Changed
- (none yet)

### Fixed
- Directory context loss in `/init-project` command by consolidating mkdir and cd into chained commands
- Directory context loss in `/release` command when updating sibling projects

## [v1.2.0] - 2025-12-10

### Added
- Initial framework structure
- Product Manager skill with Discovery and Definition modes
- Architect skill with ADR, domain modeling, and tech evaluation support
- Developer skill with coding standards, testing guide, commit conventions
- Reviewer skill with review and security checklists
- **Legal Consultant skill** for early-stage legal risk assessment
  - Identifies regulatory concerns during product discovery/definition
  - Covers compliance domains: GDPR, CCPA, employment law, AI regulations
  - HR tech specific guidance (EEOC, disparate impact, ban-the-box, etc.)
  - Risk assessment templates with severity levels
  - Jurisdiction considerations for multi-market products
  - References: compliance-domains.md, legal-risk-template.md, jurisdiction-considerations.md
- Discovery-to-Architecture workflow
- New Feature workflow
- Commands: /new-skill, /validate-skill, /release, /init-project
- Child project template
- **Project management infrastructure**:
  - `projects/` directory for local projects (gitignored)
  - `.claude/siblings.json` for tracking projects and auto-update settings
  - `/update-sub-sdlc [version]` command to sync submodule (pull latest or checkout version)
  - `/init-project` now creates projects under `projects/` with submodule setup
  - `/release` now auto-updates all registered projects with `autoUpdate: true`
  - `/validate-skill` now checks skill is registered in settings.json.template
- `/prepare-release` command to review commits and update CHANGELOG before releases
- GitHub repository auto-creation in `/init-project` (with public/private option)

### Changed
- `/init-project` simplified to create projects under `projects/` directory
- `/init-project` now uses chained commands to maintain directory context
- `/release` enhanced to update all registered sibling projects
- `/validate-skill` now checks skill registration in both settings files
- Documentation structure updated with project management workflow

### Deprecated
- (none yet)

### Removed
- (none yet)

### Fixed
- Directory context loss in `/init-project` by using chained commands
- legal-consultant skill registration in `.claude/settings.json`

### Security
- (none yet)

## [v1.0.0] - TBD

Initial release.

### Skills
- **product-manager**: Discovery Mode (explore, question) → Definition Mode (document, decide)
- **architect**: System design, ADRs, domain modeling, tech evaluation
- **developer**: Implementation, coding standards, testing, commits
- **reviewer**: Code review, security review
- **legal-consultant**: Early-stage legal risk assessment, compliance guidance

### Workflows
- **discovery-to-architecture**: Full pre-implementation flow
- **new-feature**: Adding features to existing projects

### Commands
- `/new-skill <name>`: Scaffold a new skill
- `/validate-skill <path>`: Validate skill structure
- `/release <version>`: Create versioned release and update projects
- `/init-project <name>`: Initialize project under projects/ with ai-sdlc submodule
- `/update-sub-sdlc [version]`: Update ai-sdlc submodule in current project
