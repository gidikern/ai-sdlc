# /validate-skill

Validate a skill's structure and quality.

## Usage
```
/validate-skill <path-to-skill>
```

## Validation Checks

### Structure (Required)
- [ ] `SKILL.md` exists
- [ ] YAML frontmatter present with `name` and `description`
- [ ] Description includes trigger conditions

### Quality (Recommended)
- [ ] SKILL.md under 500 lines
- [ ] Role section defines clear expertise areas
- [ ] Workflow section has numbered steps
- [ ] Behaviors section covers main scenarios
- [ ] Output artifacts are specified
- [ ] Interaction style is defined

### References
- [ ] If SKILL.md > 300 lines, content should be split to references/
- [ ] References are linked from SKILL.md
- [ ] No orphaned reference files

### Registration
- [ ] Skill is listed in `.claude/settings.json` (ai-sdlc's own settings)
- [ ] Skill is listed in `templates/child-project/.claude/settings.json.template` (for child projects)

## Output

Report validation results:

```markdown
## Skill Validation: [skill-name]

### ✅ Passed
- [Check 1]
- [Check 2]

### ❌ Failed
- [Issue 1]: [How to fix]
- [Issue 2]: [How to fix]

### ⚠️ Warnings
- [Recommendation 1]
- [Recommendation 2]

### Summary
[VALID | INVALID | NEEDS ATTENTION]
```
