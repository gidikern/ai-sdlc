# Compliance Domains Reference

Quick reference for identifying applicable regulatory frameworks based on product characteristics.

## Data Privacy Regulations

### GDPR (General Data Protection Regulation)
- **Applies to**: Any product processing EU resident data
- **Key requirements**:
  - Lawful basis for processing
  - Data minimization
  - Right to erasure, portability, access
  - Data Protection Impact Assessments (DPIA)
  - 72-hour breach notification
  - Data Processing Agreements (DPA) with vendors
- **Penalties**: Up to 4% global annual revenue or €20M

### CCPA/CPRA (California Consumer Privacy Act)
- **Applies to**: Businesses with CA customers meeting thresholds
- **Key requirements**:
  - Right to know, delete, opt-out of sale
  - Privacy policy disclosures
  - "Do Not Sell" link requirement
  - Service provider contracts
- **Penalties**: $2,500-$7,500 per violation

### Other US State Privacy Laws
- Virginia (VCDPA)
- Colorado (CPA)
- Connecticut (CTDPA)
- Utah (UCPA)
- More states adopting similar frameworks

## Industry-Specific Regulations

### Healthcare (HIPAA)
- **Applies to**: Covered entities and business associates handling PHI
- **Key requirements**:
  - Privacy Rule compliance
  - Security Rule safeguards
  - Business Associate Agreements
  - Minimum necessary standard
- **Red flags**: Health data, patient information, medical records

### Financial Services
- **SOX**: Public company financial controls
- **GLBA**: Financial institution data protection
- **PCI-DSS**: Payment card data handling
- **Red flags**: Payment processing, financial data, investment advice

### Education (FERPA)
- **Applies to**: Educational institutions and their vendors
- **Key requirements**:
  - Student record privacy
  - Parental consent requirements
  - Limited disclosure rules

## Employment & HR Regulations

### US Federal
- **Title VII**: Prohibits discrimination based on race, color, religion, sex, national origin
- **ADEA**: Age discrimination (40+)
- **ADA**: Disability discrimination and accommodation
- **FCRA**: Background check requirements
- **EEOC Guidelines**: AI/algorithmic hiring scrutiny

### State-Specific Employment Laws
- **New York Local Law 144**: AI hiring tool audits required
- **Illinois AIPA**: Video interview AI consent requirements
- **Maryland**: Facial recognition consent in hiring
- **California**: Extensive employee privacy rights

### Key HR Tech Risks
| Feature | Risk Area | Requirement |
|---------|-----------|-------------|
| Resume screening | Disparate impact | Bias testing, validation |
| Skills assessment | ADA compliance | Accommodation process |
| Background checks | FCRA | Adverse action notices |
| Video interviews | State consent laws | Explicit consent |
| Salary recommendations | Pay equity laws | Audit trail |

## Consumer Protection

### FTC Act (Section 5)
- Prohibits unfair or deceptive practices
- Applies to: All businesses
- Key focus: Truth in advertising, data practices matching promises

### CAN-SPAM
- Commercial email requirements
- Opt-out mechanisms
- Accurate header information

### TCPA
- Telemarketing and text message consent
- Do-not-call compliance
- Prior express written consent for marketing

### COPPA
- **Applies to**: Services directed at or knowingly collecting from children under 13
- **Requirements**: Verifiable parental consent, data minimization

## Accessibility

### ADA (Americans with Disabilities Act)
- Digital accessibility increasingly enforced
- WCAG 2.1 AA as de facto standard

### Section 508
- Federal contractor requirements
- Often adopted as private sector benchmark

## AI-Specific Regulations (Emerging)

### EU AI Act
- Risk-based categorization
- High-risk AI systems (including HR/employment)
- Transparency requirements
- Human oversight mandates

### US State AI Laws
- Growing patchwork of AI-specific requirements
- Focus on employment, consumer protection

## Jurisdiction Quick Reference

| Jurisdiction | Key Regulations | Notes |
|--------------|-----------------|-------|
| US (Federal) | FTC, FCRA, EEOC, HIPAA | Industry-specific focus |
| US (California) | CCPA/CPRA, CalOPPA | Strongest state privacy |
| US (New York) | LL144, Shield Act | AI hiring, breach notification |
| EU | GDPR, AI Act | Comprehensive, extraterritorial |
| UK | UK GDPR, DPA 2018 | Post-Brexit framework |
| Canada | PIPEDA, provincial laws | Federal and provincial layers |

## Determining Applicability Checklist

When assessing a product, determine:

1. **Geography**
   - [ ] Where is the business located?
   - [ ] Where are users/customers located?
   - [ ] Where is data stored/processed?

2. **Industry**
   - [ ] Healthcare involvement?
   - [ ] Financial services?
   - [ ] Education?
   - [ ] Children as users?

3. **Data Types**
   - [ ] Personal information?
   - [ ] Sensitive categories (health, financial, biometric)?
   - [ ] Employee data?

4. **Technology**
   - [ ] AI/ML decision-making?
   - [ ] Automated profiling?
   - [ ] Biometric processing?

5. **Business Model**
   - [ ] B2B or B2C?
   - [ ] Data monetization?
   - [ ] Third-party data sharing?
