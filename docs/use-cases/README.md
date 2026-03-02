# Qwen Code Use Cases Beyond Software Development

Qwen Code is a versatile AI agent that extends far beyond code assistance. Its agentic capabilities, skills system, sub-agents, and MCP integration make it powerful for office work, business operations, creative projects, and personal tasks.

---

## Quick Start by Role

| Role | Start Here | Key Features |
|------|------------|--------------|
| **Office Admin** | [Office & Administrative](./office) | Email, documents, spreadsheets, scheduling |
| **HR Professional** | [HR & Recruiting](./hr) | Job descriptions, resume screening, onboarding |
| **Finance Team** | [Finance & Accounting](./finance) | Invoices, budgets, forecasts, audits |
| **Marketing** | [Marketing & Content](./marketing) | Content creation, social media, SEO |
| **Legal & Compliance** | [Legal & Compliance](./legal) | Contract review, policy audits, compliance |
| **Sales & CS** | [Sales & Customer Success](./sales) | Proposals, health scoring, churn analysis |
| **Personal Use** | [Personal & Home](./personal) | Finance, travel, education, creative projects |

---

## Core Concepts

### Skills

**Skills** are modular capabilities that Qwen Code autonomously invokes when relevant. They're perfect for recurring tasks.

**Example Skill Structure:**
```
my-skill/
├── SKILL.md           # Required: Definition and instructions
├── templates/         # Optional: Reusable templates
└── scripts/           # Optional: Helper scripts
```

### Sub-Agents

**Sub-Agents** are specialized AI assistants configured for specific roles. They maintain isolated context and can be configured with specific tools and skills.

**Example Sub-Agent:**
```yaml
---
name: hr-assistant
description: HR tasks including job descriptions, resume screening, performance reviews
tools:
  - read_file
  - write_file
  - read_many_files
---

You are an HR assistant specializing in recruitment and employee management...
```

### Sub-Agents Using Skills

Sub-agents can be configured to use specific skills, creating powerful specialized workflows:

```yaml
---
name: contract-analyst
description: Legal contract review and analysis. Use PROACTIVELY for any contract-related requests.
skills:
  - contract-review
  - clause-extractor
  - risk-assessor
tools:
  - read_file
  - write_file
  - read_many_files
---

You are a legal contract analyst...
```

---

## Use Case Categories

### 🏢 Office & Administrative

| Task | Skill/Agent | Example |
|------|-------------|---------|
| Email Management | `email-drafter` skill | Draft professional responses |
| Document Processing | `document-analyzer` sub-agent | Review contracts, extract terms |
| Spreadsheet Analysis | `data-analyst` sub-agent | Budget variance, sales reports |
| Meeting Minutes | `meeting-assistant` skill | Transcribe and summarize |
| Scheduling | `scheduler` skill | Coordinate meetings across timezones |

[Learn more →](./office)

### 👥 HR & Recruiting

| Task | Skill/Agent | Example |
|------|-------------|---------|
| Job Descriptions | `jd-generator` skill | Create role-specific postings |
| Resume Screening | `resume-screener` sub-agent | Rank candidates by criteria |
| Performance Reviews | `review-drafter` skill | Write balanced evaluations |
| Onboarding Plans | `onboarding-planner` sub-agent | 30-60-90 day plans |
| Policy Documents | `policy-reviewer` skill | Compliance checking |

[Learn more →](./hr)

### 💰 Finance & Accounting

| Task | Skill/Agent | Example |
|------|-------------|---------|
| Invoice Processing | `invoice-processor` skill | Extract data from PDFs |
| Budget Analysis | `budget-analyst` sub-agent | Variance reports |
| Financial Forecasting | `forecaster` sub-agent | Revenue projections |
| Expense Auditing | `expense-auditor` skill | Policy compliance |
| Tax Preparation | `tax-organizer` skill | Document categorization |

[Learn more →](./finance)

### 📢 Marketing & Content

| Task | Skill/Agent | Example |
|------|-------------|---------|
| Content Calendar | `content-planner` sub-agent | Quarterly planning |
| Social Media | `social-media-manager` skill | Multi-platform posts |
| SEO Optimization | `seo-optimizer` skill | Content optimization |
| Press Releases | `pr-writer` skill | AP Style drafts |
| Blog Writing | `blog-writer` sub-agent | Long-form content |

[Learn more →](./marketing)

### ⚖️ Legal & Compliance

| Task | Skill/Agent | Example |
|------|-------------|---------|
| Contract Review | `contract-reviewer` sub-agent | Risk flagging |
| Policy Audits | `compliance-auditor` sub-agent | GDPR, SOC2 checks |
| Clause Library | `clause-extractor` skill | Standard language |
| Legal Research | `legal-researcher` skill | Case law summaries |
| Document Discovery | `ediscovery` sub-agent | Case preparation |

[Learn more →](./legal)

### 💼 Sales & Customer Success

| Task | Skill/Agent | Example |
|------|-------------|---------|
| Proposal Generation | `proposal-writer` sub-agent | RFP responses |
| Health Scoring | `health-scorer` skill | Customer risk assessment |
| Churn Analysis | `churn-analyst` sub-agent | Retention insights |
| Account Plans | `account-planner` skill | Strategic planning |
| Case Studies | `case-study-writer` skill | Success stories |

[Learn more →](./sales)

### 🏠 Personal & Home

| Task | Skill/Agent | Example |
|------|-------------|---------|
| Budget Planning | `personal-budget` skill | Expense categorization |
| Travel Planning | `travel-planner` sub-agent | Full itineraries |
| Study Guides | `study-assistant` skill | Exam preparation |
| Home Inventory | `inventory-manager` skill | Insurance documentation |
| Creative Writing | `creative-writer` sub-agent | Stories, novels |

[Learn more →](./personal)

---

## Configuration Examples

### Creating a Business Skill

**File:** `~/.qwen/skills/email-responder/SKILL.md`

```markdown
---
name: email-responder
description: Draft professional email responses. Use when asked to write emails, respond to clients, or handle email communication.
---

# Email Responder Skill

## Instructions
1. Identify the email type (inquiry, complaint, follow-up, etc.)
2. Determine the appropriate tone (formal, friendly, apologetic)
3. Include all key points mentioned in the request
4. Keep under 200 words unless specified
5. Include professional sign-off

## Email Structure
- Subject line (if not provided)
- Greeting
- Opening (acknowledge receipt/context)
- Body (address key points)
- Call to action
- Closing

## Tone Guidelines
- Formal: "Dear," "Sincerely," passive voice acceptable
- Friendly: "Hi," "Best," conversational but professional
- Apologetic: Acknowledge issue, explain resolution, offer goodwill
```

### Creating a Sub-Agent with Skills

**File:** `.qwen/agents/marketing-manager.md`

```yaml
---
name: marketing-manager
description: Marketing tasks including content creation, social media, SEO, and campaign planning. Use PROACTIVELY for any marketing-related requests.
skills:
  - email-responder
  - content-calendar
  - social-media-posts
  - seo-optimizer
tools:
  - read_file
  - write_file
  - read_many_files
  - web_search
---

You are a marketing manager with expertise in:

## Content Marketing
- Blog posts and articles
- Whitepapers and case studies
- Email newsletters
- Social media content

## SEO Best Practices
- Keyword research and integration
- Meta descriptions and titles
- Internal linking strategies
- Content optimization

## Campaign Planning
- Multi-channel campaigns
- Audience segmentation
- A/B testing recommendations
- Performance metrics

## Brand Voice
- Consistent messaging across channels
- Platform-appropriate tone adjustments
- Visual content descriptions

When given a marketing task:
1. Clarify the target audience and goal
2. Recommend the best channels and formats
3. Create content following brand guidelines
4. Include measurement recommendations
```

### Sub-Agent Using Multiple Skills

**File:** `.qwen/agents/executive-assistant.md`

```yaml
---
name: executive-assistant
description: Executive support including scheduling, correspondence, document preparation, and meeting management. Use PROACTIVELY for EA tasks.
skills:
  - email-responder
  - meeting-minutes
  - travel-planner
  - document-formatter
  - scheduler
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are an executive assistant providing comprehensive support.

## Responsibilities

### Calendar Management
- Schedule and coordinate meetings across timezones
- Identify and resolve scheduling conflicts
- Prepare meeting agendas and materials
- Send calendar invites with all details

### Correspondence
- Draft and review emails on behalf of executive
- Prioritize incoming communications
- Follow up on pending items
- Maintain professional tone

### Document Preparation
- Create presentations from outlines
- Format reports and documents
- Proofread and edit content
- Ensure brand consistency

### Meeting Support
- Take detailed meeting minutes
- Track action items and owners
- Send follow-up summaries
- Maintain meeting archives

### Travel Coordination
- Plan domestic and international trips
- Book flights, hotels, and ground transport
- Create detailed itineraries
- Handle visa and documentation needs

## Working Style
- Proactive: Anticipate needs before asked
- Discreet: Handle confidential information appropriately
- Efficient: Minimize executive's administrative burden
- Thorough: Double-check all details
```

---

## MCP Integration for Business Tools

Connect Qwen Code to your business systems:

### Google Workspace
```bash
# Google Drive
qwen mcp add gdrive npx -y @modelcontextprotocol/server-gdrive \
  -e GOOGLE_APPLICATION_CREDENTIALS="~/.gcp/credentials.json"

# Gmail
qwen mcp add gmail npx -y @modelcontextprotocol/server-gmail \
  -e GOOGLE_APPLICATION_CREDENTIALS="~/.gcp/credentials.json"

# Google Calendar
qwen mcp add calendar npx -y @modelcontextprotocol/server-google-calendar \
  -e GOOGLE_APPLICATION_CREDENTIALS="~/.gcp/credentials.json"
```

### Salesforce
```bash
qwen mcp add salesforce npx -y @modelcontextprotocol/server-salesforce \
  -e SALESFORCE_INSTANCE_URL="https://your-instance.salesforce.com" \
  -e SALESFORCE_ACCESS_TOKEN="your-token"
```

### Slack
```bash
qwen mcp add slack npx -y @modelcontextprotocol/server-slack \
  -e SLACK_BOT_TOKEN="xoxb-your-token"
```

### GitHub (for project management)
```bash
qwen mcp add github npx -y @modelcontextprotocol/server-github \
  -e GITHUB_PERSONAL_ACCESS_TOKEN="ghp_your-token"
```

### PostgreSQL (for business data)
```bash
qwen mcp add postgres npx -y @modelcontextprotocol/server-postgres \
  -e DATABASE_URL="postgresql://user:pass@localhost:5432/analytics"
```

---

## Best Practices

### 1. Start with Skills
Skills are easier to create and test. Start with skills for common tasks, then combine them into sub-agents.

### 2. Use Descriptive Names
```yaml
# Good
name: contract-reviewer
description: Review contracts and flag risky clauses. Use PROACTIVELY for vendor agreements and legal documents.

# Bad
name: legal-helper
description: Helps with legal stuff.
```

### 3. Limit Tool Access
Give sub-agents only the tools they need:
```yaml
# Resume screener doesn't need shell access
tools:
  - read_file
  - read_many_files
  - write_file
```

### 4. Create Skill Libraries
Build a library of reusable skills:
```
~/.qwen/skills/
├── email-responder/
├── document-formatter/
├── data-analyzer/
├── meeting-minutes/
└── travel-planner/
```

### 5. Test Iteratively
1. Test skill in isolation
2. Test sub-agent with single skill
3. Test sub-agent with multiple skills
4. Refine based on results

### 6. Document Your Configurations
Keep a README in your `.qwen/` folder:
```markdown
# My Qwen Code Configuration

## Sub-Agents
- `marketing-manager` - Used for all content creation
- `finance-analyst` - Budget and forecast reviews
- `hr-assistant` - Recruiting and onboarding

## Key Skills
- `email-responder` - Daily email drafting
- `meeting-minutes` - All team meetings
- `data-analyzer` - Spreadsheet analysis

## MCP Servers
- `gdrive` - Company documents
- `slack` - Team communications
- `salesforce` - Customer data
```

---

## Getting Started Checklist

- [ ] Install Qwen Code: `npm install -g @qwen-code/qwen-code@latest`
- [ ] Authenticate: Run `qwen` and follow login prompts
- [ ] Create your first skill (see [Skills Guide](../users/features/skills))
- [ ] Create your first sub-agent (see [Sub-Agents Guide](../users/features/sub-agents))
- [ ] Set up MCP servers for your business tools (see [MCP Guide](../users/features/mcp))
- [ ] Test with a simple task
- [ ] Iterate and expand your configuration

---

## Related Documentation

- [Skills](../users/features/skills) — Create custom AI capabilities
- [Sub-Agents](../users/features/sub-agents) — Specialized AI assistants
- [MCP](../users/features/mcp) — Connect external tools
- [Commands](../users/features/commands) — Slash, @, ! commands
- [Configuration](../users/configuration/settings) — All settings reference

---

*Last updated: March 2, 2026*
