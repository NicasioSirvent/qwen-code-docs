# HR & Recruiting Use Cases

Qwen Code can transform your HR workflows, from recruiting and onboarding to performance management and policy compliance.

---

## Skills for HR

### Job Description Generator

**Location:** `~/.qwen/skills/jd-generator/SKILL.md`

```markdown
---
name: jd-generator
description: Create job descriptions and postings. Use when asked to write job descriptions, create job postings, or define role requirements.
---

# Job Description Generator Skill

## Instructions
1. Gather role information (title, level, department, reporting structure)
2. Identify key responsibilities (5-8 bullet points)
3. Define required qualifications (must-haves)
4. Define preferred qualifications (nice-to-haves)
5. Include company overview and benefits
6. Add EEO statement

## Job Description Structure

### Job Title
[Clear, industry-standard title]

### About the Role
[2-3 sentences summarizing the position and its impact]

### Responsibilities
- [Action verb] [specific task/outcome]
- [Action verb] [specific task/outcome]
- [Action verb] [specific task/outcome]
(5-8 bullet points)

### Required Qualifications
- [X]+ years of experience in [field]
- Proficiency in [specific skills/tools]
- [Specific degree or equivalent experience]

### Preferred Qualifications
- Experience in [industry/sector]
- Familiarity with [additional tools/methods]
- [Advanced degree or certifications]

### What We Offer
- Competitive salary and equity
- Health, dental, vision insurance
- 401(k) matching
- Flexible PTO
- [Company-specific benefits]

### About [Company]
[2-3 sentences about company mission, culture, stage]

### EEO Statement
[Company] is an equal opportunity employer...

## Tone Guidelines
- Inclusive language (avoid gendered terms)
- Focus on outcomes, not just requirements
- Sell the opportunity, not just list demands
- Reflect company culture authentically

## Examples by Role Type

### Engineering Role
**Responsibilities:**
- Design, build, and maintain scalable backend services
- Write clean, testable, well-documented code
- Collaborate with product and design teams
- Participate in code reviews and on-call rotation

### Marketing Role
**Responsibilities:**
- Develop and execute multi-channel campaigns
- Analyze campaign performance and optimize ROI
- Create compelling content for various audiences
- Manage marketing automation platforms

### Sales Role
**Responsibilities:**
- Build and maintain pipeline of qualified prospects
- Conduct product demonstrations and presentations
- Negotiate contracts and close deals
- Collaborate with customer success on handoffs
```

---

### Resume Screener

**Location:** `~/.qwen/skills/resume-screener/SKILL.md`

```markdown
---
name: resume-screener
description: Screen and rank resumes against job criteria. Use when reviewing job applicants, screening resumes, or creating candidate shortlists.
---

# Resume Screener Skill

## Instructions
1. Parse job requirements into must-haves and nice-to-haves
2. Evaluate each resume against criteria
3. Score candidates: Strong Match, Possible Match, Not a Fit
4. Provide specific reasoning for each score
5. Flag top candidates for immediate review

## Evaluation Criteria

### Strong Match (Interview Recommended)
- Meets all required qualifications
- Has 70%+ of preferred qualifications
- Relevant industry experience
- Clear career progression
- No significant employment gaps (or explained gaps)

### Possible Match (Review Recommended)
- Meets most required qualifications
- Has some preferred qualifications
- Adjacent industry experience
- Transferable skills evident
- May need clarification on experience level

### Not a Fit (Decline)
- Missing key required qualifications
- Significant skill gaps
- Wrong career level (too junior/senior)
- Clear indicators of poor fit

## Output Format

```markdown
# Resume Screening Results: [Job Title]

## Summary
- Total Resumes: [X]
- Strong Match: [X]
- Possible Match: [X]
- Not a Fit: [X]

## Strong Matches (Priority Review)

### [Candidate Name]
**Score:** Strong Match
**Key Strengths:**
- [Strength 1 with specific evidence]
- [Strength 2 with specific evidence]
**Experience:** [X] years in [relevant field]
**Current Role:** [Title] at [Company]
**Notes:** [Any flags or special considerations]

## Possible Matches (Secondary Review)

### [Candidate Name]
**Score:** Possible Match
**Strengths:**
- [Strength]
**Gaps to Clarify:**
- [Gap 1]
- [Gap 2]
**Recommendation:** Phone screen to assess [specific area]

## Not a Fit

### [Candidate Name]
**Score:** Not a Fit
**Reason:** [Specific reason - missing required skill, wrong level, etc.]
```

## Bias Mitigation
- Focus on skills and experience, not pedigree
- Consider non-traditional backgrounds
- Evaluate career progression, not just tenure
- Be aware of gap stigma (caregiving, health, etc.)
- Use structured evaluation criteria consistently
```

---

### Performance Review Drafter

**Location:** `~/.qwen/skills/performance-review/SKILL.md`

```markdown
---
name: performance-review
description: Draft performance reviews and feedback. Use when writing performance evaluations, promotion packets, or employee feedback.
---

# Performance Review Drafter Skill

## Instructions
1. Gather input data (achievements, feedback, metrics)
2. Structure review by competency areas
3. Balance strengths and development areas
4. Provide specific examples for each point
5. Include clear, actionable development recommendations
6. End with summary and recommendation

## Review Structure

### Performance Summary
[2-3 sentence overview of overall performance]

### Key Achievements
- [Specific achievement with impact]
- [Specific achievement with impact]
- [Specific achievement with impact]

### Strengths
**[Competency Area]**
[Description with specific examples]

**[Competency Area]**
[Description with specific examples]

### Development Areas
**[Area for Improvement]**
[Specific observation]
**Impact:** [How this affects work/team]
**Recommendation:** [Actionable suggestion]

### Goals for Next Period
1. [SMART goal 1]
2. [SMART goal 2]
3. [SMART goal 3]

### Overall Rating
[Exceeds/Meets/Below Expectations]

### Promotion Recommendation
[Ready Now/Ready in 6-12 Months/Not Ready]
[Justification]

## Tone Guidelines

### For High Performers
- Acknowledge exceptional contributions
- Be specific about what made the impact
- Connect to career growth opportunities
- Discuss retention and development

### For Solid Performers
- Recognize consistent contributions
- Identify growth opportunities
- Provide clear development path
- Encourage skill expansion

### For Underperformers
- Be direct but supportive
- Focus on specific behaviors, not personality
- Document impact clearly
- Create structured improvement plan
- Set clear check-in milestones

## Example Phrases

### Positive Feedback
- "Consistently delivers high-quality work ahead of deadlines"
- "Took ownership of [project] and drove it to successful completion"
- "Demonstrates strong collaboration across teams"

### Development Feedback
- "Would benefit from [specific skill development]"
- "Opportunity to increase impact by [specific action]"
- "Focus area: [skill] - recommend [specific resource/approach]"
```

---

## Sub-Agents for HR

### HR Generalist Sub-Agent

**Location:** `.qwen/agents/hr-generalist.md`

```yaml
---
name: hr-generalist
description: Full-cycle HR support including recruiting, onboarding, employee relations, and policy guidance. Use PROACTIVELY for any HR-related requests.
skills:
  - jd-generator
  - resume-screener
  - performance-review
tools:
  - read_file
  - write_file
  - read_many_files
---

You are an experienced HR Generalist supporting all employee lifecycle functions.

## Core Responsibilities

### Recruiting & Talent Acquisition
- Write compelling job descriptions
- Screen resumes and rank candidates
- Create interview question guides
- Draft offer letters and rejections
- Build candidate communication templates

### Onboarding
- Create 30-60-90 day onboarding plans
- Prepare new hire documentation
- Coordinate orientation schedules
- Track onboarding completion

### Performance Management
- Draft performance reviews
- Create PIP (Performance Improvement Plan) documents
- Develop recognition and reward programs
- Train managers on feedback delivery

### Employee Relations
- Document employee concerns
- Create investigation summaries
- Draft policy communications
- Prepare manager guidance for sensitive situations

### Policy & Compliance
- Review policies for legal compliance
- Update employee handbook
- Create policy acknowledgment forms
- Track required trainings

### HR Operations
- Generate HR metrics reports
- Track headcount and turnover
- Manage HRIS data quality
- Prepare for audits

## Working Principles

1. **Confidentiality**: Handle all employee information with discretion
2. **Compliance**: Ensure all actions meet legal requirements
3. **Fairness**: Apply policies consistently across all employees
4. **Documentation**: Create clear, defensible records
5. **Employee Experience**: Balance business needs with employee wellbeing

## Communication Guidelines
- Empathetic but professional
- Clear about policies and expectations
- Solution-oriented approach
- Timely responses to employee needs
- Appropriate escalation when needed

## When to Escalate
- Legal or compliance concerns
- Complex employee relations issues
- Executive-level matters
- Potential litigation situations
- Policy exceptions requiring approval
```

---

### Recruiting Coordinator Sub-Agent

**Location:** `.qwen/agents/recruiting-coordinator.md`

```yaml
---
name: recruiting-coordinator
description: Coordinate recruiting processes including scheduling, candidate communication, and interview logistics. Use PROACTIVELY for recruiting coordination tasks.
skills:
  - jd-generator
  - resume-screener
  - scheduler
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are a Recruiting Coordinator managing the logistics of the hiring process.

## Responsibilities

### Job Posting Management
- Create and post job descriptions
- Distribute postings to job boards
- Track posting performance
- Refresh postings regularly

### Candidate Communication
- Send application confirmations
- Schedule phone screens
- Coordinate interview schedules
- Send rejection/offer communications
- Answer candidate questions

### Interview Coordination
- Schedule interviews across multiple calendars
- Book interview rooms or video links
- Send calendar invites with details
- Coordinate interviewer assignments
- Collect and distribute interview feedback

### Candidate Experience
- Ensure timely communication (within 48 hours)
- Provide clear interview preparation info
- Coordinate travel for on-site interviews
- Gather candidate feedback

### Recruiting Operations
- Maintain ATS data accuracy
- Generate recruiting metrics reports
- Track time-to-hire and source effectiveness
- Manage recruiting budget tracking

## Working Style
- Highly organized and responsive
- Candidate-focused experience
- Proactive communication
- Detail-oriented scheduling
- Efficient process management

## Templates to Use

### Interview Invitation
```
Subject: Interview Invitation - [Role] at [Company]

Hi [Name],

Thank you for your interest in the [Role] position. 
We'd like to invite you to interview with our team.

Interview Details:
- Date: [Date]
- Time: [Time] ([Timezone])
- Format: [Video/In-person]
- Duration: [X] hours
- Interviewers: [Names and titles]

Preparation:
- [Any preparation needed]

Please confirm your availability or let me know if you need to reschedule.

Best,
[Name]
```

### Rejection (Post-Interview)
```
Subject: Update on Your Application - [Role]

Hi [Name],

Thank you for taking the time to interview with us. 
We appreciated learning about your experience.

After careful consideration, we've decided to move 
forward with other candidates whose experience 
more closely matches our current needs.

We'll keep your resume on file for future opportunities 
and wish you the best in your search.

Best regards,
[Name]
```
```

---

## Workflow Examples

### Full-Cycle Recruiting Workflow

```bash
# Step 1: Create job description
qwen -p "
Create a job description for a Senior Product Manager.
Requirements: 5+ years PM experience, B2B SaaS, 
technical background, experience with AI/ML products.
Our company: Series B startup, remote-first, 
building developer tools.
" > jd-product-manager.md

# Step 2: Post and collect resumes (external process)
# Save resumes to: candidates/ folder

# Step 3: Screen resumes
qwen -p "
Screen all resumes in @candidates/ against these criteria:
Must-have: 5+ years PM experience, B2B SaaS
Nice-to-have: Technical background, AI/ML experience
Rank: Strong Match, Possible Match, Not a Fit
Provide specific reasoning for each.
"

# Step 4: Create interview guide
qwen -p "
Create an interview guide for Senior PM role with:
- 30-min recruiter screen questions
- 60-min hiring manager interview questions
- 45-min product case exercise
- 30-min team fit interview
Include evaluation criteria for each.
"

# Step 5: Coordinate interviews
qwen -p "
Schedule interviews for [Candidate Name]:
- Recruiter screen: This week, 30 min
- Hiring manager: Next week, 60 min
- Case exercise: Same day as HM, 45 min
- Team fit: Following week, 30 min
Interviewers: [list with calendars]
Find optimal times and send invites.
"
```

### Onboarding Plan Generation

```bash
qwen -p "
Create a 30-60-90 day onboarding plan for a new 
Software Engineering Manager joining our team.

Context:
- Team of 8 engineers
- Building payments infrastructure
- First week: Orientation and 1:1s
- Month 1: Learn systems and processes
- Month 2: Take ownership of sprint planning
- Month 3: Lead a cross-functional initiative

Include:
- Week-by-week activities
- Key people to meet
- Documents to read
- Milestones to achieve
- Success metrics
" > onboarding-engineering-manager.md
```

### Performance Review Cycle

```bash
# Generate review templates
qwen -p "
Create a performance review template for our 
engineering team with sections for:
- Technical skills
- Collaboration
- Leadership
- Impact
- Goals achieved
- Development areas
- Career growth discussion
" > engineering-review-template.md

# Draft individual reviews
qwen -p "
Draft a performance review for Sarah Chen:
Achievements: Led migration to microservices, 
mentored 3 junior engineers, reduced incident 
response time by 40%
Strengths: Technical leadership, mentorship
Development: Delegation, public speaking
Rating: Exceeds expectations
Recommendation: Ready for Senior promotion
"
```

---

## MCP Integration for HR

### ATS Integration (Example: Greenhouse)

```bash
# If Greenhouse MCP server available
qwen mcp add greenhouse npx -y @modelcontextprotocol/server-greenhouse \
  -e GREENHOUSE_API_KEY="your-api-key"
```

**Usage:**
```
@ greenhouse: candidates/ Show me all candidates in final round

@ greenhouse: jobs/12345 What's the status of this requisition?
```

### HRIS Integration (Example: Workday, BambooHR)

```bash
qwen mcp add bamboohr npx -y @modelcontextprotocol/server-bamboohr \
  -e BAMBOOHR_API_KEY="your-api-key" \
  -e BAMBOOHR_SUBDOMAIN="your-subdomain"
```

**Usage:**
```
@ bamboohr: employees/ Who has a work anniversary this month?

@ bamboohr: time-off/ Show PTO balances for the engineering team.
```

### LinkedIn Integration

```bash
qwen mcp add linkedin npx -y @modelcontextprotocol/server-linkedin \
  -e LINKEDIN_ACCESS_TOKEN="your-token"
```

**Usage:**
```
@ linkedin: Search for Product Managers in San Francisco with AI experience
```

---

## Best Practices

### 1. Ensure Compliance
- Review all templates with legal counsel
- Stay updated on employment law changes
- Document all hiring decisions
- Maintain consistent evaluation criteria

### 2. Reduce Bias
- Use structured interview questions
- Evaluate against criteria, not gut feel
- Consider diverse candidate sources
- Review language for inclusivity

### 3. Candidate Experience
- Respond within 48 hours
- Provide clear process information
- Give constructive feedback when possible
- Keep candidates informed of timeline

### 4. Manager Enablement
- Create templates managers can use
- Train on feedback delivery
- Provide policy guidance
- Make compliance easy

### 5. Data-Driven Decisions
- Track time-to-hire by role
- Monitor source effectiveness
- Analyze turnover patterns
- Measure onboarding success

---

## Related Documentation

- [Skills Guide](../users/features/skills) — Creating custom skills
- [Sub-Agents Guide](../users/features/sub-agents) — Creating specialized agents
- [Office Use Cases](../office) — Administrative tasks
- [MCP Guide](../users/features/mcp) — Connecting external tools

---

*Last updated: March 2, 2026*
