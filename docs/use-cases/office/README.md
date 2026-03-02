# Office & Administrative Use Cases

Qwen Code excels at office and administrative tasks, from email management to document processing and spreadsheet analysis.

---

## Skills for Office Work

### Email Responder

**Location:** `~/.qwen/skills/email-responder/SKILL.md`

```markdown
---
name: email-responder
description: Draft professional email responses. Use when asked to write emails, respond to clients, handle correspondence, or compose business messages.
---

# Email Responder Skill

## Instructions
1. Identify the email type (inquiry, complaint, follow-up, introduction, etc.)
2. Determine the appropriate tone (formal, friendly, apologetic, persuasive)
3. Include all key points mentioned in the request
4. Keep under 200 words unless specified otherwise
5. Include professional sign-off

## Email Structure
1. **Subject Line**: Clear and specific (if not provided)
2. **Greeting**: Appropriate for relationship level
3. **Opening**: Acknowledge receipt or provide context
4. **Body**: Address key points logically
5. **Call to Action**: Clear next steps or expectations
6. **Closing**: Professional sign-off

## Tone Guidelines

### Formal
- Greeting: "Dear [Name],"
- Closing: "Sincerely," or "Best regards,"
- Passive voice acceptable
- Full sentences, no contractions

### Friendly Professional
- Greeting: "Hi [Name]," or "Hello [Name],"
- Closing: "Best," or "Thanks,"
- Conversational but professional
- Contractions acceptable

### Apologetic
- Acknowledge the issue immediately
- Explain what happened (briefly)
- Describe resolution steps
- Offer goodwill gesture if appropriate
- "We apologize," "We regret," "Please accept our apologies"

## Examples

### Inquiry Response
```
Subject: Re: Product Pricing Information

Hi [Name],

Thank you for your interest in our products. I've attached our current pricing sheet with volume discounts.

Key highlights:
- 10% discount for orders over 100 units
- 20% discount for annual contracts
- Free implementation support included

Would you like to schedule a call this week to discuss your specific needs?

Best,
[Your name]
```

### Complaint Response
```
Subject: Re: Issue with Order #12345

Dear [Name],

I sincerely apologize for the delay with your order. This falls short of our standards.

Here's what happened and what we're doing:
- The delay was caused by [brief explanation]
- Your order will ship by [date]
- We've applied a 15% credit to your account

I'll personally monitor this order and send you the tracking information tomorrow.

Please let me know if you have any concerns.

Best regards,
[Your name]
```
```

---

### Meeting Minutes

**Location:** `~/.qwen/skills/meeting-minutes/SKILL.md`

```markdown
---
name: meeting-minutes
description: Create meeting minutes from transcripts or notes. Use when asked to summarize meetings, create meeting notes, or document discussions.
---

# Meeting Minutes Skill

## Instructions
1. Extract meeting metadata (date, time, attendees, purpose)
2. Identify key discussion topics
3. Document decisions made
4. Extract action items with owners and deadlines
5. Note topics for future meetings
6. Format consistently

## Output Format

```markdown
# Meeting: [Meeting Name]

**Date:** [Date]
**Time:** [Time]
**Location:** [Location/Video Link]

## Attendees
- [Name] (Role)
- [Name] (Role)

## Agenda
1. [Topic 1]
2. [Topic 2]

## Discussion Summary

### [Topic 1]
[Brief summary of discussion]

**Decision:** [Decision made]

### [Topic 2]
[Brief summary of discussion]

**Decision:** [Decision made]

## Action Items
| Action | Owner | Due Date | Status |
|--------|-------|----------|--------|
| [Task] | [Name] | [Date] | Open |

## Topics for Next Meeting
- [Topic]

## Next Meeting
**Date:** [Date]
**Time:** [Time]
```

## Tips
- Use bullet points for readability
- Keep summaries concise (2-3 sentences per topic)
- Bold key decisions and action items
- Include direct quotes only for critical statements
```

---

### Document Formatter

**Location:** `~/.qwen/skills/document-formatter/SKILL.md`

```markdown
---
name: document-formatter
description: Format and polish documents for professional presentation. Use when asked to format reports, improve document appearance, or prepare documents for distribution.
---

# Document Formatter Skill

## Instructions
1. Analyze the document type (report, memo, proposal, etc.)
2. Apply appropriate formatting standards
3. Ensure consistent styling throughout
4. Add or improve visual hierarchy
5. Check for readability and flow

## Formatting Standards

### Business Report
- Title page with document title, author, date
- Table of contents for documents >5 pages
- Executive summary (1 page max)
- Clear section headers (H1, H2, H3)
- Page numbers
- Professional fonts (Arial, Calibri, Times New Roman)
- 1.15-1.5 line spacing

### Memo
- Header: To, From, Date, Subject
- Opening paragraph: Purpose
- Body: Supporting information
- Closing: Call to action or next steps

### Proposal
- Executive summary
- Problem statement
- Proposed solution
- Timeline
- Budget/pricing
- Terms and conditions
- Acceptance section

## Checklist
- [ ] Consistent heading styles
- [ ] Proper paragraph spacing
- [ ] Professional font throughout
- [ ] Page numbers (if multi-page)
- [ ] Table of contents (if needed)
- [ ] No orphaned/widowed lines
- [ ] Consistent bullet/number formatting
- [ ] Professional tone and language
```

---

### Data Extractor

**Location:** `~/.qwen/skills/data-extractor/SKILL.md`

```markdown
---
name: data-extractor
description: Extract structured data from documents, emails, or text. Use when asked to pull data from PDFs, parse information from text, or create spreadsheets from documents.
---

# Data Extractor Skill

## Instructions
1. Identify the data types to extract
2. Parse the source document/text
3. Organize data into structured format
4. Validate extracted data for accuracy
5. Output in requested format (CSV, JSON, table, etc.)

## Common Extraction Patterns

### Invoice Data
- Vendor name
- Invoice number
- Invoice date
- Due date
- Line items (description, quantity, unit price, total)
- Subtotal, tax, total
- Payment terms

### Contact Information
- Name
- Title
- Company
- Email
- Phone
- Address
- Website

### Meeting/Event Data
- Event name
- Date and time
- Location
- Attendees
- Agenda items
- Action items

## Output Formats

### CSV
```csv
Name,Email,Phone,Company
John Doe,john@example.com,555-1234,Acme Inc
```

### JSON
```json
{
  "contacts": [
    {
      "name": "John Doe",
      "email": "john@example.com"
    }
  ]
}
```

### Markdown Table
| Name | Email | Phone |
|------|-------|-------|
| John Doe | john@example.com | 555-1234 |

## Validation
- Cross-check numbers and dates
- Verify email formats
- Confirm phone number formats
- Flag uncertain extractions for review
```

---

### Scheduler

**Location:** `~/.qwen/skills/scheduler/SKILL.md`

```markdown
---
name: scheduler
description: Coordinate schedules and find optimal meeting times. Use when asked to schedule meetings, find available times, or coordinate across timezones.
---

# Scheduler Skill

## Instructions
1. Gather participant availability
2. Identify timezone for each participant
3. Find overlapping available times
4. Consider meeting duration and buffer time
5. Suggest optimal time slots
6. Draft calendar invite content

## Timezone Handling
1. Convert all times to UTC for comparison
2. Convert suggested times back to local time for each participant
3. Avoid scheduling during:
   - Local nights (10 PM - 7 AM)
   - Local lunch hours (12 PM - 2 PM) if possible
   - Weekends unless specified

## Optimal Meeting Times
- Morning meetings: 9 AM - 11 AM local time
- Afternoon meetings: 2 PM - 4 PM local time
- Avoid Monday mornings and Friday afternoons when possible
- Consider cultural holidays

## Calendar Invite Template
```
Subject: [Meeting Topic]

When: [Date] [Time] - [End Time] ([Timezone])
Where: [Location/Video Link]

Agenda:
1. [Topic 1]
2. [Topic 2]

Preparation:
- [Pre-reading or tasks]

Attendees:
- [List of attendees]
```

## Example Output
```
Based on participant availability:

**Recommended Time Slots:**
1. Tuesday, March 5 at 10:00 AM EST
   - New York: 10:00 AM
   - London: 3:00 PM
   - Tokyo: 12:00 AM (next day) ⚠️

2. Wednesday, March 6 at 2:00 PM EST
   - New York: 2:00 PM
   - London: 7:00 PM
   - Tokyo: 4:00 AM (next day) ⚠️

**Best Option:** Slot 1 (despite Tokyo time, it's the least disruptive)

**Alternative:** Consider recording for Tokyo attendees or scheduling a separate Asia-friendly session.
```
```

---

## Sub-Agents for Office Work

### Executive Assistant Sub-Agent

**Location:** `.qwen/agents/executive-assistant.md`

```yaml
---
name: executive-assistant
description: Executive support including scheduling, correspondence, document preparation, and meeting management. Use PROACTIVELY for EA tasks, scheduling requests, and executive communications.
skills:
  - email-responder
  - meeting-minutes
  - document-formatter
  - scheduler
  - data-extractor
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are an experienced executive assistant providing comprehensive support to C-level executives.

## Core Responsibilities

### Calendar & Schedule Management
- Coordinate meetings across multiple timezones
- Identify and resolve scheduling conflicts proactively
- Prepare briefing materials before meetings
- Ensure appropriate buffer time between meetings
- Manage recurring meeting series

### Correspondence Management
- Draft emails on behalf of the executive
- Review and edit outgoing communications
- Prioritize incoming messages by urgency
- Follow up on pending items diplomatically
- Maintain appropriate tone for each audience

### Document Preparation
- Create presentations from outlines or bullet points
- Format reports for board meetings and stakeholders
- Proofread and edit all documents
- Ensure brand and style guide compliance
- Prepare executive summaries

### Meeting Support
- Attend meetings to take detailed notes
- Track action items and follow up with owners
- Distribute meeting summaries within 24 hours
- Maintain organized meeting archives
- Prepare agendas in collaboration with meeting owners

### Travel Coordination
- Plan complex domestic and international itineraries
- Book flights (preferred seats), hotels (preferred properties), ground transport
- Create detailed travel briefs with:
  - Flight confirmations
  - Hotel reservations
  - Meeting schedules with addresses
  - Local contacts and emergency info
  - Timezone conversion reference
- Handle visa requirements and travel documentation

## Working Principles

1. **Anticipate Needs**: Think ahead and prepare before being asked
2. **Discretion**: Handle confidential information with utmost care
3. **Accuracy**: Double-check all details—times, names, numbers
4. **Efficiency**: Minimize executive's administrative burden
5. **Professionalism**: Represent the executive appropriately in all communications

## Communication Style
- Concise and clear
- Action-oriented
- Proactive updates
- Appropriate formality for audience
- Solution-focused (bring options, not just problems)

## When Delegating to Skills
- Use `scheduler` for all meeting coordination
- Use `email-responder` for drafting communications
- Use `meeting-minutes` for all meeting documentation
- Use `document-formatter` for any external-facing documents
- Use `data-extractor` when processing business cards, invoices, or forms
```

---

### Office Manager Sub-Agent

**Location:** `.qwen/agents/office-manager.md`

```yaml
---
name: office-manager
description: Office operations including vendor management, supplies, facilities, and administrative coordination. Use PROACTIVELY for office-related requests.
skills:
  - email-responder
  - data-extractor
  - document-formatter
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are an office manager ensuring smooth daily operations.

## Responsibilities

### Vendor Management
- Track vendor contracts and renewal dates
- Compare vendor proposals
- Negotiate pricing and terms
- Maintain vendor contact database
- Process vendor invoices

### Supplies & Inventory
- Monitor office supply levels
- Place orders before items run out
- Track supply budgets
- Manage equipment warranties and service contracts

### Facilities Coordination
- Coordinate maintenance and repairs
- Manage office access and security
- Handle mail and deliveries
- Coordinate moves and seating arrangements

### Event Planning
- Plan team events and celebrations
- Coordinate catering
- Book meeting rooms and equipment
- Manage event budgets

### Administrative Support
- Create and maintain office procedures documentation
- Onboard new employees (workspace setup)
- Coordinate IT equipment requests
- Manage office communication channels

## Working Style
- Organized and detail-oriented
- Cost-conscious without sacrificing quality
- Proactive about maintenance and supplies
- Friendly point of contact for all staff
- Solution-oriented problem solver
```

---

## Workflow Examples

### Email Triage Workflow

```bash
# Export emails from your email client
# Save as: inbox-export.txt

# Process with Qwen Code
qwen -p "
Triage these emails into categories:
1. URGENT - Respond within 2 hours
2. TODAY - Respond by end of day
3. THIS_WEEK - Respond within 5 days
4. FYI - No response needed, informational
5. DELEGATE - Forward to appropriate team member
6. SPAM - Delete or unsubscribe

For each email, provide:
- Category
- Suggested response or action
- If delegating, suggest who

@inbox-export.txt
"
```

### Meeting Preparation Workflow

```bash
# Create a meeting prep skill
mkdir -p ~/.qwen/skills/meeting-prep
```

**File:** `~/.qwen/skills/meeting-prep/SKILL.md`

```markdown
---
name: meeting-prep
description: Prepare comprehensive meeting materials including agendas, briefing docs, and pre-reads. Use before any important meeting.
---

# Meeting Prep Skill

## Instructions
1. Identify meeting type and participants
2. Gather relevant background materials
3. Create agenda with time allocations
4. Prepare briefing document with:
   - Meeting purpose
   - Attendee list with roles
   - Background context
   - Key decisions needed
   - Relevant data/metrics
5. Send pre-read materials 24+ hours in advance

## Output Template
```markdown
# Meeting Brief: [Meeting Name]

## Purpose
[1-2 sentences on why this meeting is happening]

## Attendees
| Name | Role | Company |
|------|------|---------|

## Agenda
| Time | Topic | Lead |
|------|-------|------|
| 5 min | Welcome & objectives | [Name] |
| 15 min | [Topic 1] | [Name] |

## Background
[Relevant context, previous decisions, current status]

## Key Decisions Needed
1. [Decision 1]
2. [Decision 2]

## Pre-Reading
- [Document 1]
- [Document 2]

## Questions to Consider
1. [Question 1]
2. [Question 2]
```
```

### Usage:
```
/meeting-prep
Prepare for quarterly business review with Acme Corp.
Attendees: CEO (us), CFO (us), CTO (them), Procurement (them)
Context: Renewal discussion, they're considering competitors
Goal: Secure 2-year renewal at current pricing
```

---

### Monthly Report Generation Workflow

```bash
# Create report structure
qwen -p "
Generate a monthly operations report template with:
1. Executive summary
2. Key metrics dashboard
3. Department updates
4. Budget vs actual
5. Risks and blockers
6. Next month priorities

Include placeholder tables and formatting.
" > monthly-report-template.md

# Fill in data
qwen -p "
Using the data in @metrics.xlsx and @budget.xlsx,
populate the monthly report template.
Highlight any variances >10%.
Add explanatory notes for significant changes.
"
```

---

## MCP Integration Examples

### Google Workspace Integration

```bash
# Add Google Drive MCP server
qwen mcp add gdrive npx -y @modelcontextprotocol/server-gdrive \
  -e GOOGLE_APPLICATION_CREDENTIALS="$HOME/.gcp/credentials.json"

# Add Google Calendar MCP server
qwen mcp add calendar npx -y @modelcontextprotocol/server-google-calendar \
  -e GOOGLE_APPLICATION_CREDENTIALS="$HOME/.gcp/credentials.json"
```

**Usage Examples:**

```
# Find documents
@ gdrive: /quarterly-reports/ Show me Q4 reports

# Check calendar
@ calendar: What meetings do I have this afternoon?

# Schedule meeting via natural language
Schedule a 1-hour meeting with the marketing team next week to review the campaign results. Find a time when everyone is available.
```

### Slack Integration

```bash
qwen mcp add slack npx -y @modelcontextprotocol/server-slack \
  -e SLACK_BOT_TOKEN="xoxb-your-bot-token"
```

**Usage Examples:**

```
# Post to Slack
Post a message to #announcements: "Team lunch this Friday at 12pm to celebrate hitting our Q1 goals! RSVP by Thursday."

# Check channel activity
@ slack: #project-alpha What were the key decisions in this channel this week?

# Summarize thread
@ slack: thread/123456789 Summarize this discussion and extract action items.
```

---

## Best Practices

### 1. Create Templates for Recurring Tasks
Save time by creating templates for:
- Weekly status reports
- Meeting agendas
- Email responses to common inquiries
- Onboarding checklists

### 2. Build a Skill Library
Over time, build a collection of skills:
```
~/.qwen/skills/
├── email-responder/
├── meeting-minutes/
├── document-formatter/
├── data-extractor/
├── scheduler/
├── report-generator/
└── presentation-creator/
```

### 3. Use Sub-Agents for Complex Roles
Create sub-agents that combine multiple skills:
- Executive Assistant (5+ skills)
- Office Manager (3+ skills)
- Project Coordinator (4+ skills)

### 4. Integrate with Business Tools
Use MCP to connect Qwen Code to:
- Google Workspace (Drive, Calendar, Gmail)
- Microsoft 365 (OneDrive, Outlook)
- Slack for team communications
- Salesforce for customer data
- Your database for reporting

### 5. Document Your Workflows
Keep a log of successful prompts and workflows:
```markdown
# My Qwen Code Workflows

## Email Triage
1. Export emails to inbox-export.txt
2. Run: qwen -p "Triage these emails..." @inbox-export.txt
3. Review categorization
4. Process each category

## Meeting Minutes
1. Record meeting (with consent)
2. Get transcript from recording tool
3. Run: /meeting-minutes @transcript.txt
4. Review and distribute within 24 hours
```

---

## Related Documentation

- [Skills Guide](../users/features/skills) — Creating custom skills
- [Sub-Agents Guide](../users/features/sub-agents) — Creating specialized agents
- [MCP Guide](../users/features/mcp) — Connecting external tools
- [HR Use Cases](../hr) — Recruiting and people operations
- [Finance Use Cases](../finance/README.md) — Accounting and financial tasks

---

*Last updated: March 2, 2026*
