# Jurisdiction Considerations Guide

Understanding where and how regulations apply based on business operations and user locations.

## Jurisdictional Triggers

### General Principles

1. **Location of Business**: Laws where you're incorporated/headquartered
2. **Location of Users**: Laws where your customers/users reside
3. **Location of Data**: Laws where data is stored and processed
4. **Target Market**: Laws of markets you actively target

### Common Misconceptions

| Misconception | Reality |
|---------------|---------|
| "We're a US company, EU law doesn't apply" | GDPR applies if you have EU users, regardless of company location |
| "We don't store data in California" | CCPA applies based on user residence, not data location |
| "We're B2B, privacy laws don't apply" | Employee/contact data is still personal data |
| "We're small, regulations don't apply" | Size thresholds exist but vary; some laws have no threshold |

## United States

### Federal vs State

The US has a patchwork approach:
- **Federal**: Sector-specific (healthcare, finance, children)
- **State**: Increasingly comprehensive privacy and AI laws
- **Key insight**: Must comply with the most restrictive applicable law

### State-by-State Privacy Laws

| State | Law | Key Trigger | Notable Requirements |
|-------|-----|-------------|---------------------|
| California | CCPA/CPRA | $25M revenue OR 100K consumers OR 50%+ revenue from data | Broadest rights, enforcement active |
| Virginia | VCDPA | 100K consumers OR 50%+ revenue from 25K+ consumers | Sensitive data consent |
| Colorado | CPA | 100K consumers OR 25K consumers + revenue from data | Universal opt-out mechanism |
| Connecticut | CTDPA | Similar to Virginia | Right to cure violations |
| Utah | UCPA | $25M revenue + thresholds | Business-friendly |

### Employment Law Variations

Employment law is highly state-specific:

| Topic | State Variations |
|-------|------------------|
| Ban-the-box | 37 states + localities have some form |
| Salary history | 21 states + localities ban inquiries |
| AI in hiring | NY (LL144), IL (AIPA), MD (facial recognition) |
| Non-compete | CA (banned), others (limited/banned) |
| Pay transparency | CA, CO, NY, WA require salary ranges |

## European Union

### GDPR Territorial Scope

GDPR applies if:
1. You have an establishment in the EU (regardless of where processing occurs)
2. You offer goods/services to EU residents (even if free)
3. You monitor behavior of EU residents

**"Targeting" indicators**:
- EU languages (non-English)
- EU currencies
- EU domain (.eu, .de, .fr)
- Marketing to EU
- EU customer references

### Member State Variations

While GDPR is uniform, member states have flexibility on:
- Age of consent for children (13-16)
- Employment data processing
- Health data requirements
- National security exemptions

### Post-Brexit UK

- UK GDPR mirrors EU GDPR (for now)
- Separate adequacy decisions
- May diverge over time
- Need to assess both regimes

## Canada

### PIPEDA and Provincial Laws

- **PIPEDA**: Federal private sector law
- **Provincial laws**: Quebec, Alberta, BC have their own
- Quebec's Law 25: Strongest, often called "Quebec's GDPR"

### Cross-Border Transfers

Canada has adequacy from EU, but:
- Separate consent may be needed for transfers
- Contractual protections still advisable

## Multi-Jurisdiction Strategy

### Approach 1: Comply with Strictest

**Pros**: Simpler to implement, future-proof
**Cons**: May over-engineer for some markets
**Best for**: Products with global user base

### Approach 2: Geo-Targeted Compliance

**Pros**: Optimized for each market
**Cons**: Complex to implement and maintain
**Best for**: Products with distinct regional offerings

### Approach 3: Market Limitation

**Pros**: Reduced compliance burden
**Cons**: Limits growth, may need future investment
**Best for**: Early-stage products with limited resources

## Decision Framework

```
┌─────────────────────────────────────────┐
│ Where are your users located?           │
├─────────────────────────────────────────┤
│ US Only → State-by-state analysis       │
│ US + EU → GDPR + strictest US states    │
│ Global  → GDPR as baseline + regional   │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ What's your business model?             │
├─────────────────────────────────────────┤
│ B2C  → Consumer privacy laws primary    │
│ B2B  → Data processing agreements key   │
│ Both → Full compliance landscape        │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ What industry are you in?               │
├─────────────────────────────────────────┤
│ Healthcare → HIPAA + privacy laws       │
│ Finance    → GLBA + SOX + privacy       │
│ HR Tech    → Employment + privacy + AI  │
│ EdTech     → FERPA + COPPA + privacy    │
│ General    → Privacy + FTC              │
└─────────────────────────────────────────┘
```

## Jurisdiction Assessment Template

```markdown
# Jurisdiction Analysis: [Product Name]

## Target Markets
- Primary: [Countries/regions]
- Secondary: [Planned expansion]
- Excluded: [Intentionally avoided jurisdictions]

## Regulatory Applicability by Jurisdiction

### [Jurisdiction 1]
**Applicable laws**: [List]
**Trigger**: [Why this applies - user location, data storage, etc.]
**Key requirements**: [Summarize]
**Local presence needed**: Yes/No

### [Jurisdiction 2]
[Same format]

## Cross-Border Data Flows
- Data storage location(s): [List]
- Transfer mechanisms needed: [SCCs, adequacy, etc.]
- Restrictions: [Any prohibited transfers]

## Compliance Approach
- [ ] Strictest standard globally
- [ ] Geo-targeted compliance
- [ ] Market limitation

## Recommendation
[Summary of recommended approach with rationale]
```

## Red Flags for Jurisdiction Issues

Watch for these indicators that jurisdiction analysis is needed:

- [ ] Users can sign up from any country
- [ ] Marketing in multiple languages
- [ ] Pricing in multiple currencies
- [ ] Data processors/servers in different countries
- [ ] Team members in different jurisdictions
- [ ] Partnerships with international companies
- [ ] Any EU, UK, or Canadian user touchpoints
