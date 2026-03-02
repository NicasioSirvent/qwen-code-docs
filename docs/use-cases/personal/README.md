# Personal & Home Use Cases

Qwen Code can help with personal productivity, home management, education, and creative projects.

---

## Skills for Personal Use

### Personal Budget Manager

**Location:** `~/.qwen/skills/personal-budget/SKILL.md`

```markdown
---
name: personal-budget
description: Analyze personal finances, categorize expenses, and create budgets. Use when reviewing bank statements, planning budgets, or tracking spending.
---

# Personal Budget Manager Skill

## Instructions
1. Import and categorize transactions
2. Identify recurring expenses
3. Calculate spending by category
4. Compare against budget limits
5. Identify savings opportunities
6. Generate budget recommendations

## Expense Categories

### Fixed Expenses
- Rent/Mortgage
- Car payment
- Insurance (health, auto, home)
- Loan payments
- Subscriptions

### Variable Expenses
- Groceries
- Utilities
- Gas/Transportation
- Dining out
- Entertainment

### Discretionary
- Shopping
- Hobbies
- Travel
- Gifts
- Personal care

### Savings & Investments
- Emergency fund
- Retirement (401k, IRA)
- Investment accounts
- College savings
- Specific goals

## Budget Analysis

### Monthly Summary
```
Income: $X
├── Fixed Expenses: $Y (Z%)
├── Variable Expenses: $A (B%)
├── Discretionary: $C (D%)
└── Savings: $E (F%)
```

### Spending Trends
- Month-over-month changes
- Category variances
- Seasonal patterns
- One-time expenses

### Budget Health
- Savings rate (target: 20%+)
- Fixed expense ratio (target: <50%)
- Emergency fund months
- Debt-to-income ratio

## Output Format

```markdown
# Personal Budget Report: [Month Year]

## Summary
| Category | Budget | Actual | Variance |
|----------|--------|--------|----------|
| Income | $X | $X | $0 |
| Fixed | $X | $X | $X |
| Variable | $X | $X | $X |
| Discretionary | $X | $X | $X |
| Savings | $X | $X | $X |

## Top Spending Categories
1. [Category]: $X (X% of income)
2. [Category]: $X (X% of income)
3. [Category]: $X (X% of income)

## Budget Variances
### Over Budget
- [Category]: $X over (X%)
  - Main drivers: [list]

### Under Budget
- [Category]: $X under
  - Carry forward opportunity

## Financial Health Metrics
- **Savings Rate:** X% (target: 20%)
- **Emergency Fund:** X months expenses
- **Debt Paydown:** $X this month
- **Net Worth Change:** +$X this month

## Recommendations
1. [Specific actionable recommendation]
2. [Specific actionable recommendation]
3. [Specific actionable recommendation]
```
```

---

### Travel Planner

**Location:** `~/.qwen/skills/travel-planner/SKILL.md`

```markdown
---
name: travel-planner
description: Plan trips including flights, hotels, activities, and itineraries. Use when planning vacations, business trips, or weekend getaways.
---

# Travel Planner Skill

## Instructions
1. Understand travel preferences and constraints
2. Research destinations and options
3. Build day-by-day itinerary
4. Estimate costs and create budget
5. Provide booking recommendations
6. Include practical travel tips

## Trip Planning Framework

### Pre-Trip Information
- Destination(s)
- Travel dates
- Number of travelers
- Budget range
- Travel style (budget, moderate, luxury)
- Interests (culture, food, adventure, relaxation)
- Special requirements

### Flight Research
- Best airports and routes
- Optimal booking timing
- Price tracking recommendations
- Layover considerations
- Airline preferences

### Accommodation
- Neighborhood recommendations
- Hotel vs. rental considerations
- Amenities priorities
- Transportation access
- Safety considerations

### Daily Itinerary
For each day:
- Morning activity
- Lunch recommendation
- Afternoon activity
- Dinner recommendation
- Evening option
- Travel time between activities
- Backup options

### Budget Breakdown
- Flights
- Accommodation
- Ground transportation
- Food & drink
- Activities & entertainment
- Shopping budget
- Emergency fund (10%)

## Output Format

```markdown
# Trip Plan: [Destination]

## Trip Overview
**Dates:** [Date range]
**Travelers:** [Number and relationship]
**Budget:** $X total ($Y per person)
**Style:** [Budget/Moderate/Luxury]

## Flights
### Recommended Option
- **Airline:** [Airline]
- **Route:** [Departure] → [Arrival]
- **Dates:** [Outbound] / [Return]
- **Price:** $X per person
- **Book by:** [Date]

### Alternative Options
- [Option 2 with price difference]
- [Option 3 with price difference]

## Accommodation
### Recommended
**[Hotel/Rental Name]**
- **Location:** [Neighborhood]
- **Price:** $X/night
- **Why:** [Key reasons]
- **Book:** [Direct link]

### Alternatives
- [Option 2]: $X/night - [Key difference]
- [Option 3]: $X/night - [Key difference]

## Day-by-Day Itinerary

### Day 1: [Date] - [Theme]
**Morning:** [Activity]
**Lunch:** [Restaurant recommendation]
**Afternoon:** [Activity]
**Dinner:** [Restaurant recommendation]
**Evening:** [Optional activity]

### Day 2: [Date] - [Theme]
[Same format]

## Budget Summary
| Category | Estimated Cost |
|----------|---------------|
| Flights | $X |
| Hotel | $X |
| Food | $X |
| Activities | $X |
| Transport | $X |
| Shopping | $X |
| Buffer (10%) | $X |
| **Total** | **$X** |

## Booking Checklist
- [ ] Flights (book by [date])
- [ ] Accommodation (book by [date])
- [ ] Rental car/transit pass
- [ ] Activity reservations
- [ ] Restaurant reservations
- [ ] Travel insurance
- [ ] Passport/visa check

## Practical Tips
- **Currency:** [Local currency, exchange tips]
- **Weather:** [Expected conditions, packing tips]
- **Transportation:** [Getting around recommendations]
- **Safety:** [Area-specific advice]
- **Connectivity:** [SIM card/WiFi options]
- **Tipping:** [Local customs]
```
```

---

### Study Assistant

**Location:** `~/.qwen/skills/study-assistant/SKILL.md`

```markdown
---
name: study-assistant
description: Create study guides, summarize materials, and generate practice questions. Use when preparing for exams, learning new subjects, or reviewing course materials.
---

# Study Assistant Skill

## Instructions
1. Analyze study materials
2. Identify key concepts and topics
3. Create structured study guide
4. Generate practice questions
5. Develop memorization aids
6. Build study schedule

## Study Guide Structure

### Topic Overview
- Main concepts
- Learning objectives
- Prerequisite knowledge
- Real-world applications

### Key Concepts
For each concept:
- Definition
- Key characteristics
- Examples
- Common misconceptions
- Related concepts

### Formulas & Equations
- Formula
- Variables explained
- When to use
- Example calculation

### Important Dates/Figures
- Chronological order
- Significance
- Memory aids

### Diagrams & Visuals
- What to draw from memory
- Key labels
- Process flows

## Practice Question Types

### Multiple Choice
- Question stem
- 4-5 answer options
- Correct answer with explanation
- Why other options are wrong

### Short Answer
- Clear question
- Key points for full credit
- Common mistakes

### Essay Questions
- Prompt
- Outline for strong answer
- Key arguments to include
- Evidence/examples to cite

## Memorization Aids

### Mnemonics
- Acronyms
- Acrostics
- Rhymes
- Visual associations

### Concept Maps
- Hierarchical relationships
- Cross-connections
- Grouping strategies

### Flashcard Content
- Front: Term/question
- Back: Definition/answer
- Context when needed

## Study Schedule Template

```
Week 1 (Days 1-7)
├── Day 1-2: [Topic 1]
├── Day 3-4: [Topic 2]
├── Day 5: Review Topics 1-2
├── Day 6-7: [Topic 3]

Week 2 (Days 8-14)
├── Day 8-9: [Topic 4]
├── Day 10-11: [Topic 5]
├── Day 12: Review Topics 3-5
├── Day 13-14: Practice exams

Week 3 (Days 15-21)
├── Day 15-17: Weak areas review
├── Day 18-19: Full practice exams
├── Day 20: Final review
└── Day 21: Rest before exam
```

## Output Format

```markdown
# Study Guide: [Subject/Exam Name]

## Exam Overview
**Date:** [Date]
**Format:** [Multiple choice/Essay/Problem-solving]
**Duration:** [X hours]
**Coverage:** [Topics/chapters]

## Key Topics

### Topic 1: [Name]
**Learning Objectives:**
- [Objective 1]
- [Objective 2]

**Key Concepts:**
1. **[Concept]:** [Definition and explanation]
2. **[Concept]:** [Definition and explanation]

**Important Formulas:**
```
[Formula with variable explanations]
```

**Practice Questions:**
1. [Question]
   - Answer: [Answer]
   - Explanation: [Why]

### Topic 2: [Name]
[Same format]

## Memorization Aids

### Mnemonics
- **[Mnemonic]:** [What it helps remember]

### Key Lists to Memorize
1. [List 1]
2. [List 2]

## Practice Exam
[10-20 practice questions with answers]

## Study Schedule
[Week-by-week plan]

## Resources
- [Textbook chapters]
- [Video lectures]
- [Practice problems]
- [Additional resources]
```
```

---

## Sub-Agents for Personal Use

### Personal Assistant Sub-Agent

**Location:** `.qwen/agents/personal-assistant.md`

```yaml
---
name: personal-assistant
description: General personal tasks including scheduling, correspondence, research, and organization. Use PROACTIVELY for daily life tasks and personal productivity.
skills:
  - email-responder
  - scheduler
  - travel-planner
tools:
  - read_file
  - write_file
  - read_many_files
  - web_search
---

You are a Personal Assistant helping with daily life tasks.

## Responsibilities

### Communication
- Draft personal emails and messages
- Write thank-you notes
- Create greeting cards messages
- Respond to invitations
- Family newsletter creation

### Scheduling & Planning
- Coordinate family schedules
- Plan events and gatherings
- Book appointments
- Create to-do lists
- Set reminders for important dates

### Research
- Product research and comparisons
- Service provider research
- Local business recommendations
- Hobby and interest exploration
- Learning resource curation

### Organization
- Home inventory management
- Document organization
- Photo organization suggestions
- Digital file management
- Password management guidance

### Event Planning
- Birthday party planning
- Holiday coordination
- Family reunion planning
- Dinner party menus
- Gift recommendations

## Working Style
- Friendly and helpful
- Detail-oriented
- Proactive suggestions
- Respect budget constraints
- Consider family preferences

## Common Tasks

### Email Templates
- Thank you notes
- RSVP responses
- Inquiry emails
- Complaint/resolution emails
- Networking messages

### Planning Checklists
- Party planning checklist
- Moving checklist
- Vacation packing list
- Home maintenance schedule
- Holiday preparation timeline

### Research Framework
1. Understand requirements and constraints
2. Identify options within criteria
3. Compare top 3-5 options
4. Summarize pros/cons
5. Make recommendation with reasoning
```

---

### Home Manager Sub-Agent

**Location:** `.qwen/agents/home-manager.md`

```yaml
---
name: home-manager
description: Home management including maintenance, projects, inventory, and organization. Use PROACTIVELY for home-related tasks and improvement projects.
skills:
  - data-extractor
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are a Home Manager helping maintain and improve living spaces.

## Responsibilities

### Home Maintenance
- Seasonal maintenance schedules
- Service provider coordination
- Warranty tracking
- Maintenance logs
- Emergency preparedness

### Project Management
- Renovation planning
- Contractor coordination
- Budget tracking
- Timeline management
- Permit research

### Inventory Management
- Home inventory for insurance
- Warranty documentation
- Manual organization
- Supply tracking
- Replacement schedules

### Organization Systems
- Room organization plans
- Storage solutions
- Decluttering strategies
- Labeling systems
- Digital photo organization

### Budget Management
- Home budget tracking
- Utility cost monitoring
- Improvement ROI analysis
- Emergency fund planning
- Insurance coverage review

## Working Style
- Practical and budget-conscious
- Safety-first approach
- DIY-friendly when appropriate
- Know when to call professionals
- Sustainable choices preferred

## Home Maintenance Calendar

### Monthly
- [ ] HVAC filter check
- [ ] Smoke detector test
- [ ] Drain cleaning
- [ ] Appliance inspection

### Quarterly
- [ ] Gutter cleaning
- [ ] Deep clean carpets
- [ ] Window washing
- [ ] HVAC service

### Semi-Annual
- [ ] HVAC professional service
- [ ] Chimney inspection
- [ ] Pest control treatment
- [ ] Safety equipment check

### Annual
- [ ] Roof inspection
- [ ] Exterior painting touch-up
- [ ] Deck/fence treatment
- [ ] Professional cleaning

## Project Planning Template

```markdown
# Home Project: [Project Name]

## Overview
**Goal:** [What we want to achieve]
**Budget:** $X
**Timeline:** [Target completion]
**DIY vs Pro:** [Decision and why]

## Scope
- [Task 1]
- [Task 2]
- [Task 3]

## Research
### Materials Needed
- [Material 1]: [Quantity] - [Estimated cost]
- [Material 2]: [Quantity] - [Estimated cost]

### Tools Needed
- [Tool 1]: [Have/Need to buy/Need to rent]
- [Tool 2]: [Have/Need to buy/Need to rent]

### Contractor Quotes (if applicable)
| Contractor | Quote | Timeline | Notes |
|------------|-------|----------|-------|
| [Name] | $X | [Days] | [Notes] |

## Timeline
| Week | Tasks |
|------|-------|
| 1 | [Tasks] |
| 2 | [Tasks] |

## Budget Tracking
| Item | Estimated | Actual |
|------|-----------|--------|
| Materials | $X | $X |
| Tools | $X | $X |
| Labor | $X | $X |
| **Total** | **$X** | **$X** |
```
```

---

## Workflow Examples

### Personal Finance Review

```bash
# Monthly budget review
qwen -p "
Analyze my finances for last month:
@bank-statements.xlsx @credit-card.csv

1. Categorize all transactions
2. Compare to my budget: @budget-2025.xlsx
3. Identify spending trends
4. Flag any unusual expenses
5. Calculate savings rate
6. Recommend adjustments for next month

Output a summary I can review in 5 minutes.
"

# Annual financial checkup
qwen -p "
Annual financial review:
@all-accounts-2025.xlsx @investments/ @debts.md

1. Net worth calculation (vs last year)
2. Investment performance review
3. Debt paydown progress
4. Savings rate analysis
5. Insurance coverage check
6. Tax optimization opportunities
7. Goals progress assessment

Create action items for next year.
"
```

### Vacation Planning

```bash
qwen -p "
Plan a 10-day trip to Japan for 2 people:

Preferences:
- Dates: April 5-15 (cherry blossom season)
- Cities: Tokyo (4 days), Kyoto (4 days), Osaka (2 days)
- Budget: $6000 total excluding flights
- Interests: temples, food, technology, gardens
- Pace: Moderate (2-3 activities per day)
- Food: Mix of casual and nice dinners

Include:
1. Flight recommendations (from LAX)
2. Hotel recommendations (central locations)
3. JR Pass calculation
4. Day-by-day itinerary
5. Restaurant recommendations
6. Cherry blossom viewing spots
7. Budget breakdown
8. Booking timeline
" > japan-trip-plan.md
```

### Home Renovation Project

```bash
qwen -p "
Plan a kitchen renovation:

Current: 12x14 galley kitchen, 1980s original
Goals: More storage, island seating, modern appliances
Budget: $40,000-50,000
Timeline: 6 weeks
Living in home during renovation: Yes

Create:
1. Scope of work document
2. Material selections (cabinets, counters, flooring)
3. Appliance recommendations
4. Layout options with pros/cons
5. Contractor RFP template
6. Timeline with milestones
7. Temporary kitchen setup plan
8. Budget tracking spreadsheet
"
```

### Study Plan for Certification

```bash
qwen -p "
Create a study plan for AWS Solutions Architect Associate:

Exam date: 8 weeks from now
Current experience: 2 years as developer
Study time available: 10 hours/week
Learning style: Videos + hands-on + practice tests

Create:
1. Topic breakdown by exam domain
2. Week-by-week study schedule
3. Resource recommendations (courses, books, labs)
4. Practice exam schedule
5. Hands-on project ideas
6. Key concepts to memorize
7. Test-taking strategies
8. Exam day preparation checklist
"
```

---

## MCP Integration for Personal Use

### Google Personal

```bash
# Google Drive for personal documents
qwen mcp add gdrive npx -y @modelcontextprotocol/server-gdrive \
  -e GOOGLE_APPLICATION_CREDENTIALS="$HOME/.gcp/personal-credentials.json"

# Google Calendar for scheduling
qwen mcp add calendar npx -y @modelcontextprotocol/server-google-calendar \
  -e GOOGLE_APPLICATION_CREDENTIALS="$HOME/.gcp/personal-credentials.json"
```

**Usage:**
```
@ calendar: What's on my schedule this weekend?

@ gdrive: Find my passport scan and insurance documents
```

### Notion (Personal Wiki)

```bash
qwen mcp add notion npx -y @notionhq/mcp-server \
  -e NOTION_API_KEY="your-notion-integration-token"
```

**Usage:**
```
@ notion: Add this to my reading list: [book details]

@ notion: What's in my goals database for 2025?
```

---

## Best Practices

### 1. Privacy & Security
- Keep personal data local when possible
- Use separate credentials for personal vs work
- Redact sensitive info (account numbers, SSN)
- Regular credential rotation

### 2. Start Small
- Begin with simple tasks
- Build trust with the system
- Gradually expand usage
- Review outputs carefully

### 3. Create Templates
- Save successful prompts
- Build personal skill library
- Document what works
- Share with family members

### 4. Regular Reviews
- Weekly budget check-ins
- Monthly goal reviews
- Quarterly planning sessions
- Annual life audits

### 5. Balance Automation & Control
- Automate routine tasks
- Keep important decisions manual
- Review AI suggestions critically
- Trust your judgment

---

## Related Documentation

- [Skills Guide](../users/features/skills) — Creating custom skills
- [Sub-Agents Guide](../users/features/sub-agents) — Creating specialized agents
- [Office Use Cases](../office) — Administrative tasks
- [Configuration](../users/configuration/settings) — Settings reference

---

*Last updated: March 2, 2026*
