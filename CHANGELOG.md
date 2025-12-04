# Changelog

All notable changes to ai-sdlc will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial framework structure
- Product Manager skill with Discovery and Definition modes
- Architect skill with ADR, domain modeling, and tech evaluation support
- Developer skill with coding standards, testing guide, commit conventions
- Reviewer skill with review and security checklists
- Discovery-to-Architecture workflow
- New Feature workflow
- Commands: /new-skill, /validate-skill, /release, /init-project
- Child project template

### Changed
- (none yet)

### Deprecated
- (none yet)

### Removed
- (none yet)

### Fixed
- (none yet)

### Security
- (none yet)

## [v1.0.0] - TBD

Initial release.

### Skills
- **product-manager**: Discovery Mode (explore, question) → Definition Mode (document, decide)
- **architect**: System design, ADRs, domain modeling, tech evaluation
- **developer**: Implementation, coding standards, testing, commits
- **reviewer**: Code review, security review

### Workflows
- **discovery-to-architecture**: Full pre-implementation flow
- **new-feature**: Adding features to existing projects

### Commands
- `/new-skill <name>`: Scaffold a new skill
- `/validate-skill <path>`: Validate skill structure
- `/release <version>`: Create versioned release
- `/init-project <name>`: Initialize child project with ai-sdlc
