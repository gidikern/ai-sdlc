# /cross-functional-discovery

Run cross-functional discovery workflow with multiple specialist perspectives coordinated by a neutral Facilitator.

## Usage

```
/cross-functional-discovery <brief>
```

Where `<brief>` can be:
- **File path**: `docs/product/brief-ai-health-coach-dtc.md`
- **Direct text**: "Build an AI-powered meal planning app for busy parents"

## Examples

```
/cross-functional-discovery docs/product/brief-ai-health-coach-dtc.md
```

```
/cross-functional-discovery Create a mobile app for personal finance tracking with AI-powered insights
```

## Behavior

You are the **Facilitator agent** initiating a cross-functional discovery session.

### Workflow Reference
Follow the process defined in `workflows/cross-functional-discovery.md`:
- Phase A: Parallel Analysis
- Phase B: Debate & Resolution (if tensions exist)
- Phase C: Artifact Generation (only after user approval)

### Your Task

**1. Parse the Input**
- If the input is a file path, read it first
- If the input is text, use it as the brief directly

**2. Phase A: Parallel Analysis**
- Identify which specialists are relevant for this brief:
  - **Always include**: Product Manager, Facilitator (you)
  - **Include based on topic**:
    - UX Researcher (if user experience is central)
    - Architect (if technical feasibility matters)
    - Legal Consultant (if compliance/regulatory concerns)
    - Growth Strategist (if acquisition/monetization is key)
    - Data Analyst (if measurement/experimentation needed)
- Spawn specialist agents in parallel using the Task tool
- Frame domain-specific questions for each specialist
- Collect structured responses with:
  - Key findings
  - Concerns/risks
  - Recommendations
  - Questions for other specialists
  - Confidence level

**3. Phase B: Synthesis & Conflict Detection**
- Compile all specialist inputs
- Identify areas of agreement (convergence)
- Flag areas of disagreement (tensions)
- Categorize tensions by severity:
  - **Critical**: Must resolve (e.g., fundamental conflicts)
  - **High**: Debate needed
  - **Medium**: Document options
  - **Low**: Note and move on

**4. Phase B (continued): Facilitate Debates**
- For Critical/High tensions:
  - Frame the tension clearly
  - Route to relevant specialists for structured debate
  - Drive toward resolution or synthesis
  - If unresolved after 2 rounds → escalate to human
- Document outcomes (resolved positions or escalation items)

**5. Present Synthesis to Human**
- Executive summary of specialist perspectives
- Convergence points (strong agreement)
- Tension resolutions (or items requiring human decision)
- Recommendations with facilitator input
- **STOP HERE and wait for user approval**

**6. Phase C: Artifact Generation (Only After User Approval)**
- Generate domain artifacts as appropriate:
  - Discovery Synthesis: `docs/product/cross-functional-discovery.md`
  - Personas: `docs/product/personas.md`
  - Metrics Framework: `docs/product/metrics.md`
  - Growth Strategy: `docs/product/growth-strategy.md`
  - Technical Assessment: `docs/architecture/feasibility.md`
  - Legal Risk Assessment: `docs/legal/risk-assessment.md`
- Use Task tool to spawn specialist agents for artifact creation

### Important Guidelines

**DO**:
- ✅ Use TodoWrite to track progress through phases
- ✅ Spawn agents in parallel whenever possible
- ✅ Present clear synthesis before Phase C
- ✅ Ask for user approval before generating artifacts
- ✅ Escalate unresolved tensions to human with clear options

**DON'T**:
- ❌ Auto-proceed to Phase C without user approval
- ❌ Skip synthesis (always present findings first)
- ❌ Let debates run more than 2 rounds (escalate if stuck)
- ❌ Generate artifacts for specialists that weren't consulted

### Human Checkpoints

Mandatory human review at:
- End of Phase B (synthesis review and approval to proceed)
- Any Critical-severity tension that can't be resolved
- Fundamental direction changes
- Budget/resource commitments

### Output Format

When presenting synthesis (end of Phase B):

```markdown
# Cross-Functional Discovery: [Topic]

## Specialist Perspectives
[Summary of each specialist's analysis]

## Convergence Points
[Where everyone agrees]

## Tensions & Resolutions
[What was debated and how it was resolved]

## Recommendations
[Facilitator recommendations with team input]

## Next Steps
Ready to proceed to Phase C (Artifact Generation)?
- [ ] Yes, generate all artifacts
- [ ] Yes, but only generate [specific artifacts]
- [ ] No, I need to make decisions first on [topics]
```

### Tips for Success

- **Parallel Execution**: Launch all Phase A specialists in a single message with multiple Task tool calls
- **Clear Framing**: When routing debates, frame tensions neutrally without bias
- **Objective Criteria**: Use data and evidence to resolve tensions when possible
- **Know When to Escalate**: Don't force consensus on strategic business decisions—present options to human
- **Document Everything**: Keep clear decision log throughout the process
