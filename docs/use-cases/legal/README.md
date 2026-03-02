# Legal & Compliance Use Cases

Qwen Code can assist with legal document review, compliance audits, contract analysis, and regulatory research.

> ⚠️ **Important Disclaimer:** Qwen Code provides assistance with legal tasks but does not replace qualified legal counsel. All outputs should be reviewed by licensed attorneys before use in legal matters.

---

## Skills for Legal

### Contract Reviewer

**Location:** `~/.qwen/skills/contract-reviewer/SKILL.md`

```markdown
---
name: contract-reviewer
description: Review contracts and identify risky clauses, missing terms, and negotiation points. Use when reviewing vendor agreements, customer contracts, employment agreements, or any legal document.
---

# Contract Reviewer Skill

## Instructions
1. Identify contract type and parties
2. Extract key terms and dates
3. Flag risky or unusual clauses
4. Compare against standard positions
5. Identify missing standard protections
6. Summarize negotiation priorities

## Key Terms to Extract

### Basic Information
- Contract type
- Effective date
- Term/Duration
- Renewal terms
- Termination rights
- Governing law

### Financial Terms
- Payment amounts
- Payment schedule
- Late fees
- Price adjustment terms
- Tax responsibilities

### Risk Allocation
- Limitation of liability
- Indemnification obligations
- Insurance requirements
- Warranty terms
- Disclaimer of warranties

### Operational Terms
- Service levels (SLAs)
- Performance standards
- Acceptance criteria
- Change procedures
- Dispute resolution

## Risk Flag Categories

### 🔴 Critical (Deal Breakers)
- Unlimited liability
- One-sided indemnification
- Automatic renewal without notice
- Unilateral modification rights
- Overly broad IP assignment

### 🟡 High (Needs Negotiation)
- Liability cap below reasonable level
- Narrow termination rights
- Vague performance standards
- Missing data protection terms
- Unfavorable dispute resolution

### 🟢 Medium (Note for Discussion)
- Non-standard notice periods
- Unusual insurance requirements
- Restrictive covenant scope
- Ambiguous language

## Output Format

```markdown
# Contract Review: [Contract Name]

## Summary
**Parties:** [Party A] ↔ [Party B]
**Type:** [Contract Type]
**Term:** [Duration]
**Value:** [Amount if stated]

## Key Terms
| Term | Provision |
|------|-----------|
| Effective Date | [Date] |
| Initial Term | [X years] |
| Renewal | [Auto/manual, notice period] |
| Termination | [For cause/for convenience] |
| Governing Law | [State/Country] |

## Risk Analysis

### Critical Issues 🔴
1. **[Issue Name]** (Section X.X)
   - **Text:** "[Relevant excerpt]"
   - **Risk:** [Explanation of risk]
   - **Recommendation:** [Suggested revision]

### High Priority 🟡
1. **[Issue Name]** (Section X.X)
   - **Text:** "[Relevant excerpt]"
   - **Risk:** [Explanation]
   - **Recommendation:** [Suggested approach]

### Notes 🟢
- [Item 1]
- [Item 2]

## Missing Standard Protections
- [ ] Data protection/privacy terms
- [ ] Security requirements
- [ ] Business continuity
- [ ] Subcontractor restrictions
- [ ] Audit rights

## Negotiation Priorities
1. [Top priority item]
2. [Second priority]
3. [Nice to have]

## Recommended Actions
- [ ] Legal review of critical issues
- [ ] Business review of commercial terms
- [ ] Security review of data terms
- [ ] Proceed to signature with changes
```

## Standard Positions Reference

### Limitation of Liability
- **Favorable:** Mutual cap at contract value
- **Market:** Mutual cap at 12 months fees
- **Unfavorable:** No cap or one-sided cap

### Indemnification
- **Favorable:** Mutual indemnification
- **Market:** Each party indemnifies their breach
- **Unfavorable:** One-sided indemnification

### Termination
- **Favorable:** 30-day for convenience, immediate for cause
- **Market:** 30-60 day notice periods
- **Unfavorable:** No for-cause termination or auto-renewal
```

---

### Clause Extractor

**Location:** `~/.qwen/skills/clause-extractor/SKILL.md`

```markdown
---
name: clause-extractor
description: Extract specific clauses from contracts and legal documents. Use when building clause libraries, comparing contract terms, or auditing contract portfolios.
---

# Clause Extractor Skill

## Instructions
1. Identify clause types to extract
2. Locate and extract relevant text
3. Normalize formatting
4. Tag with metadata
5. Organize by category

## Clause Types

### Commercial Terms
- Payment terms
- Pricing and fees
- Price adjustment
- Invoicing procedures
- Expense reimbursement

### Risk & Liability
- Limitation of liability
- Indemnification
- Insurance requirements
- Warranty terms
- Disclaimers

### Term & Termination
- Initial term
- Renewal provisions
- Termination for cause
- Termination for convenience
- Effect of termination

### Intellectual Property
- IP ownership
- License grants
- IP indemnification
- Moral rights
- Publicity rights

### Confidentiality
- Definition of confidential info
- Obligations
- Exceptions
- Return/destruction
- Duration

### Data & Privacy
- Data processing terms
- Security requirements
- Privacy obligations
- Data breach notification
- International transfers

### Dispute Resolution
- Governing law
- Venue/jurisdiction
- Arbitration provisions
- Class action waiver
- Attorney fees

### General Provisions
- Amendment procedures
- Assignment rights
- Force majeure
- Severability
- Entire agreement
- Waiver

## Output Format

### Individual Clause
```json
{
  "clause_type": "limitation_of_liability",
  "contract_name": "Vendor Agreement - Acme Corp",
  "section": "Section 8.2",
  "text": "Neither party shall be liable for...",
  "summary": "Mutual cap at contract value, excludes IP indemnity",
  "risk_level": "market",
  "tags": ["liability", "cap", "mutual"]
}
```

### Clause Comparison
```markdown
# Clause Comparison: [Clause Type]

| Contract | Key Terms | Risk Level |
|----------|-----------|------------|
| Contract A | [Summary] | 🟢 Favorable |
| Contract B | [Summary] | 🟡 Market |
| Contract C | [Summary] | 🔴 Unfavorable |

## Analysis
[Summary of variations and patterns]
```

## Batch Processing
For contract portfolio reviews:
1. Process all contracts
2. Group by clause type
3. Identify outliers
4. Flag for remediation
```

---

### Compliance Auditor

**Location:** `~/.qwen/skills/compliance-auditor/SKILL.md`

```markdown
---
name: compliance-auditor
description: Audit policies and practices for regulatory compliance. Use when checking GDPR, SOC 2, HIPAA, or other regulatory compliance, or reviewing internal policies.
---

# Compliance Auditor Skill

## Instructions
1. Identify applicable regulations
2. Map requirements to controls
3. Review documentation for compliance
4. Identify gaps
5. Prioritize remediation
6. Generate compliance report

## Regulatory Frameworks

### GDPR (General Data Protection Regulation)
**Key Requirements:**
- Lawful basis for processing
- Consent management
- Data subject rights
- Data protection impact assessments
- Breach notification (72 hours)
- Data processing agreements
- International transfer safeguards

### SOC 2 (Service Organization Control)
**Trust Service Criteria:**
- Security (required)
- Availability
- Confidentiality
- Processing integrity
- Privacy

### HIPAA (Health Insurance Portability)
**Key Requirements:**
- Privacy Rule
- Security Rule
- Breach notification
- Business associate agreements
- Patient rights

### CCPA/CPRA (California Privacy)
**Key Requirements:**
- Consumer disclosure
- Right to delete
- Right to opt-out
- Non-discrimination
- Service provider agreements

## Audit Process

### Document Review
- Privacy policies
- Terms of service
- Data processing agreements
- Security policies
- Incident response plans
- Training materials

### Control Assessment
- Access controls
- Encryption standards
- Logging and monitoring
- Vendor management
- Incident response
- Data retention

### Gap Analysis
For each requirement:
- **Compliant:** Evidence meets requirement
- **Partial:** Some evidence, gaps exist
- **Non-compliant:** No evidence or inadequate

## Output Format

```markdown
# Compliance Audit Report: [Framework]

## Executive Summary
**Overall Status:** [Compliant/Partial/Non-compliant]
**Critical Gaps:** [Number]
**High Priority:** [Number]
**Audit Date:** [Date]

## Requirements Assessment

### [Requirement Category]
| Requirement | Status | Evidence | Gap |
|-------------|--------|----------|-----|
| [Req 1.1] | ✅ Compliant | [Document] | None |
| [Req 1.2] | ⚠️ Partial | [Document] | [Description] |
| [Req 1.3] | ❌ Non-compliant | Missing | [Description] |

## Critical Gaps
1. **[Gap Name]**
   - **Requirement:** [Regulation reference]
   - **Risk:** [Description of risk]
   - **Remediation:** [Specific action]
   - **Priority:** [Critical/High/Medium]
   - **Owner:** [Recommended owner]
   - **Timeline:** [Recommended deadline]

## Remediation Roadmap
### Immediate (0-30 days)
- [Action 1]
- [Action 2]

### Short-term (30-90 days)
- [Action 1]
- [Action 2]

### Long-term (90+ days)
- [Action 1]
- [Action 2]

## Evidence Checklist
- [ ] [Document 1]
- [ ] [Document 2]
```
```

---

## Sub-Agents for Legal

### Contract Analyst Sub-Agent

**Location:** `.qwen/agents/contract-analyst.md`

```yaml
---
name: contract-analyst
description: Analyze contracts for risk, compliance, and negotiation preparation. Use PROACTIVELY for contract review, vendor agreements, and legal document analysis.
skills:
  - contract-reviewer
  - clause-extractor
tools:
  - read_file
  - write_file
  - read_many_files
---

You are a Contract Analyst supporting legal and business teams.

## Core Responsibilities

### Contract Review
- Review incoming contracts for risk
- Flag non-standard terms
- Compare against playbook positions
- Summarize key terms for stakeholders
- Route to appropriate reviewers

### Contract Analysis
- Extract key terms and dates
- Identify obligations and deadlines
- Map contract relationships
- Track renewal and termination dates
- Maintain contract database

### Negotiation Support
- Prepare negotiation briefs
- Suggest alternative language
- Track changes through redlines
- Document negotiated positions
- Support closing process

### Contract Lifecycle
- Intake and triage
- Drafting assistance
- Review coordination
- Signature workflow
- Post-execution management

## Working Principles

1. **Risk-Aware:** Identify and escalate material risks
2. **Business-Enabled:** Support deal velocity while managing risk
3. **Consistent:** Apply playbook standards uniformly
4. **Documented:** Maintain clear audit trail
5. **Collaborative:** Work with legal, security, and business teams

## Risk Escalation Matrix
| Risk Level | Action |
|------------|--------|
| Critical | Escalate to General Counsel immediately |
| High | Legal review required before proceeding |
| Medium | Business approval with legal notice |
| Low | Note for records, proceed |

## Contract Types You Handle
- Vendor/supplier agreements
- Customer contracts
- NDAs (mutual and unilateral)
- Employment agreements
- Contractor agreements
- SaaS terms of service
- Data processing agreements
- Partnership agreements
```

---

### Compliance Officer Sub-Agent

**Location:** `.qwen/agents/compliance-officer.md`

```yaml
---
name: compliance-officer
description: Monitor and ensure regulatory compliance across privacy, security, and industry regulations. Use PROACTIVELY for compliance audits, policy reviews, and regulatory research.
skills:
  - compliance-auditor
  - contract-reviewer
tools:
  - read_file
  - write_file
  - read_many_files
  - web_search
---

You are a Compliance Officer ensuring regulatory adherence.

## Responsibilities

### Privacy Compliance
- GDPR compliance monitoring
- CCPA/CPRA compliance
- Data mapping and inventory
- Privacy impact assessments
- Data subject request handling
- Consent management oversight

### Security Compliance
- SOC 2 preparation and maintenance
- Security policy reviews
- Vendor security assessments
- Incident response planning
- Security training coordination

### Industry Regulations
- HIPAA (if healthcare)
- PCI-DSS (if payments)
- FINRA/SEC (if financial)
- Industry-specific requirements

### Policy Management
- Policy creation and updates
- Policy acknowledgment tracking
- Exception management
- Annual review coordination

### Vendor Compliance
- DPA review and execution
- Vendor risk assessments
- Right to audit coordination
- Subprocessor monitoring

### Training & Awareness
- Compliance training development
- Role-based training assignment
- Training completion tracking
- Awareness communications

## Working Principles

1. **Proactive:** Identify issues before they become problems
2. **Thorough:** Comprehensive documentation and tracking
3. **Practical:** Balance compliance with business needs
4. **Current:** Stay updated on regulatory changes
5. **Transparent:** Clear communication of requirements

## Compliance Calendar
| Month | Activity |
|-------|----------|
| January | Annual policy review |
| March | Q1 vendor assessments |
| June | Mid-year compliance check |
| September | SOC 2 preparation |
| October | Annual privacy assessment |
| December | Year-end compliance report |

## Key Metrics
- Policy acknowledgment rate
- Training completion rate
- Vendor DPA execution rate
- Audit findings resolved
- Data subject request SLA
- Incident response time
```

---

## Workflow Examples

### Vendor Contract Review Workflow

```bash
# Step 1: Initial review
qwen -p "
Review this vendor agreement for our SaaS procurement:
@vendor-agreement.pdf

Focus on:
1. Data security and privacy terms
2. Liability and indemnification
3. Service levels and uptime commitments
4. Termination and data return
5. Pricing and renewal terms

Flag anything that differs from our standard positions.
"

# Step 2: Extract key terms
qwen -p "
Extract all key terms from @vendor-agreement.pdf:
- Contract duration and renewal
- Pricing and payment terms
- Termination rights
- Liability caps
- Data processing terms
- Security commitments

Create a summary table for the procurement team.
"

# Step 3: Compare against playbook
qwen -p "
Compare this contract against our vendor playbook:
@vendor-playbook.md @vendor-agreement.pdf

For each playbook position, indicate:
✅ Compliant
⚠️ Needs negotiation
❌ Non-compliant

List specific sections that need redlining.
"

# Step 4: Generate negotiation brief
qwen -p "
Create a negotiation brief for the legal team:
1. Executive summary of key risks
2. Priority negotiation points (top 5)
3. Suggested alternative language for each
4. Business impact of each issue
5. Recommended fallback positions
"
```

### GDPR Compliance Audit

```bash
qwen -p "
Conduct a GDPR compliance audit:

Review these documents:
@privacy-policy.md
@terms-of-service.md
@data-processing-agreements/
@security-policies/
@incident-response-plan.md
@data-retention-schedule.md

Assess against GDPR requirements:
1. Lawful basis documentation
2. Consent mechanisms
3. Data subject rights process
4. Breach notification procedure
5. International transfer safeguards
6. DPA requirements with vendors

Generate compliance report with gap analysis
and remediation priorities.
"
```

### Contract Portfolio Analysis

```bash
qwen -p "
Analyze our entire contract portfolio for renewal risk:
@contracts/customer-agreements/
@contracts/vendor-agreements/

For each contract:
1. Extract renewal date and notice period
2. Calculate notice deadline
3. Flag auto-renewal contracts
4. Identify contracts up for renewal in next 90 days
5. Flag any with unfavorable renewal terms

Create a renewal calendar with action deadlines.
Output to: contract-renewal-calendar.csv
"
```

---

## MCP Integration for Legal

### Legal Research (Westlaw/LexisNexis alternative)

```bash
# If legal research MCP server available
qwen mcp add legal-research npx -y @modelcontextprotocol/server-legal-research \
  -e LEGAL_API_KEY="your-api-key"
```

**Usage:**
```
@ legal-research: Find cases about software licensing disputes in California

@ legal-research: What are the recent GDPR enforcement actions?
```

### Document Management (iManage/NetDocuments)

```bash
qwen mcp add imanager npx -y @modelcontextprotocol/server-imanager \
  -e IMANAGE_URL="https://your-instance.imanage.net" \
  -e IMANAGE_CREDENTIALS="your-credentials"
```

**Usage:**
```
@ imanager: Find all NDAs executed in 2025

@ imanager: Show me the latest version of the MSA template
```

### E-Signature (DocuSign)

```bash
qwen mcp add docusign npx -y @modelcontextprotocol/server-docusign \
  -e DOCUSIGN_ACCOUNT_ID="your-account-id" \
  -e DOCUSIGN_ACCESS_TOKEN="your-token"
```

**Usage:**
```
@ docusign: List all envelopes pending signature

@ docusign: Send this contract for signature: @final-contract.pdf
Recipients: legal@vendor.com, cfo@ourcompany.com
```

---

## Best Practices

### 1. Always Have Legal Review
- AI assistance is not legal advice
- Licensed attorney must review all outputs
- Document AI use in legal workflows
- Maintain attorney-client privilege

### 2. Maintain Confidentiality
- Use secure environments
- Redact sensitive information when possible
- Follow data handling policies
- Use appropriate access controls

### 3. Document Everything
- Keep records of all reviews
- Document decisions and rationale
- Track changes through versions
- Maintain audit trails

### 4. Stay Current
- Regulations change frequently
- Update playbooks regularly
- Monitor enforcement trends
- Continuous compliance education

### 5. Risk-Based Approach
- Prioritize high-risk items
- Allocate resources appropriately
- Document risk acceptance
- Regular risk reassessment

---

## Related Documentation

- [Skills Guide](../users/features/skills) — Creating custom skills
- [Sub-Agents Guide](../users/features/sub-agents) — Creating specialized agents
- [Office Use Cases](../office) — Administrative tasks
- [MCP Guide](../users/features/mcp) — Connecting external tools

---

*Last updated: March 2, 2026*
