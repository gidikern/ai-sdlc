# Legal Risk Documentation Template

Use this template to document individual legal risks identified during product review.

## Individual Risk Entry

```markdown
## Risk: [Descriptive Title]

**ID**: LEGAL-NNN
**Severity**: Critical | High | Medium | Low
**Category**: Privacy | Employment | Consumer | Industry-Specific | AI/Algorithmic
**Status**: Identified | Under Review | Mitigated | Accepted

### Description
[Clear explanation of the legal risk in plain language]

### Applicable Regulations
- [Law/Regulation 1]: [Specific section or requirement]
- [Law/Regulation 2]: [Specific section or requirement]

### Affected Features
- [Feature or functionality that triggers this risk]

### Potential Consequences
- **Legal**: [Fines, lawsuits, regulatory action]
- **Business**: [Operational impact, market limitations]
- **Reputation**: [Brand and trust implications]

### Mitigation Options

#### Option A: [Name]
- **Approach**: [Description]
- **Pros**: [Benefits]
- **Cons**: [Drawbacks]
- **Effort**: Low | Medium | High

#### Option B: [Name]
- **Approach**: [Description]
- **Pros**: [Benefits]
- **Cons**: [Drawbacks]
- **Effort**: Low | Medium | High

### Recommendation
[Recommended approach with rationale]

### Professional Counsel Needed
- [ ] Yes - [Specify area of expertise needed]
- [ ] No - Can proceed with documented approach

### References
- [Link to regulation]
- [Link to guidance document]
- [Link to relevant case or enforcement action]
```

## Example: HR Tech Risk Entry

```markdown
## Risk: AI Resume Screening May Cause Disparate Impact

**ID**: LEGAL-001
**Severity**: Critical
**Category**: Employment | AI/Algorithmic
**Status**: Identified

### Description
Using AI/ML to screen resumes and rank candidates may result in disparate impact discrimination against protected classes, even without intentional bias. The EEOC has issued guidance treating such tools as "selection procedures" subject to Title VII.

### Applicable Regulations
- Title VII of Civil Rights Act: Disparate impact liability
- EEOC Uniform Guidelines on Employee Selection Procedures
- NY Local Law 144: Requires annual bias audits for automated employment decision tools
- Illinois AIPA: Requires consent for AI analysis in video interviews

### Affected Features
- Resume parsing and ranking
- Candidate matching algorithm
- Skills assessment scoring

### Potential Consequences
- **Legal**: EEOC investigation, class action lawsuits, NY fines up to $1,500/day
- **Business**: Product may be unusable in certain jurisdictions without compliance
- **Reputation**: Public disclosure of bias findings damages brand

### Mitigation Options

#### Option A: Remove AI Ranking
- **Approach**: Use AI only for keyword extraction, not ranking decisions
- **Pros**: Eliminates algorithmic bias liability
- **Cons**: Reduces core value proposition
- **Effort**: High (product redesign)

#### Option B: Implement Bias Testing Framework
- **Approach**: Regular adverse impact analysis, third-party audits, explainability
- **Pros**: Maintains functionality while demonstrating compliance efforts
- **Cons**: Ongoing cost, doesn't eliminate all risk
- **Effort**: Medium

#### Option C: Human-in-the-Loop Requirement
- **Approach**: AI provides suggestions only, all decisions require human review
- **Pros**: Shifts liability, demonstrates human oversight
- **Cons**: May slow hiring process
- **Effort**: Low

### Recommendation
Implement Option B (Bias Testing Framework) combined with Option C (Human-in-the-Loop). This maintains product value while demonstrating good faith compliance efforts and providing defensible documentation.

### Professional Counsel Needed
- [x] Yes - Employment law attorney for bias testing methodology validation
- [x] Yes - Review of vendor agreements for compliance liability allocation

### References
- EEOC Technical Assistance Document on AI (2023)
- NY Local Law 144 Final Rules
- Four-Fifths Rule (29 CFR 1607.4D)
```

## Risk Register Summary Format

Maintain a summary table for executive visibility:

```markdown
# Legal Risk Register

| ID | Risk | Severity | Category | Status | Owner | Due Date |
|----|------|----------|----------|--------|-------|----------|
| LEGAL-001 | AI screening disparate impact | Critical | Employment | Mitigating | [Name] | [Date] |
| LEGAL-002 | GDPR consent mechanism | High | Privacy | In Review | [Name] | [Date] |
| LEGAL-003 | CCPA opt-out missing | Medium | Privacy | Identified | [Name] | [Date] |
```

## Severity Guidelines

### Critical
- Regulatory prohibition of core business activity
- Potential fines exceeding $1M or 2%+ revenue
- Class action lawsuit exposure
- Criminal liability risk
- **Timeline**: Must address before any launch

### High
- Likely regulatory investigation if discovered
- Potential fines $100K-$1M
- Individual lawsuit exposure
- Significant market access limitations
- **Timeline**: Should address before public launch

### Medium
- Best practice gap that may draw scrutiny
- Potential fines under $100K
- Compliance audit findings likely
- Minor market limitations
- **Timeline**: Address within 6 months of launch

### Low
- Industry best practice not yet adopted
- Minimal enforcement risk
- Competitive disadvantage only
- **Timeline**: Consider for future roadmap
