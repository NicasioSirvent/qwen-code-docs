# Finance & Accounting Use Cases

Qwen Code can streamline finance and accounting workflows, from invoice processing to financial analysis and reporting.

---

## Skills for Finance

### Invoice Processor

**Location:** `~/.qwen/skills/invoice-processor/SKILL.md`

```markdown
---
name: invoice-processor
description: Extract and process invoice data from PDFs and documents. Use when processing vendor invoices, extracting billing data, or organizing accounts payable.
---

# Invoice Processor Skill

## Instructions
1. Extract all relevant fields from invoice
2. Validate data completeness
3. Categorize expense by type
4. Flag anomalies for review
5. Output in structured format

## Data Fields to Extract

### Vendor Information
- Vendor name
- Vendor address
- Vendor contact information
- Tax ID / VAT number

### Invoice Details
- Invoice number
- Invoice date
- Due date
- Payment terms (Net 30, etc.)
- Purchase order number (if applicable)

### Line Items
- Description
- Quantity
- Unit price
- Line total
- Tax per line (if itemized)

### Totals
- Subtotal
- Tax amount
- Tax rate
- Shipping/handling
- Total amount
- Currency

### Payment Information
- Remittance address
- Bank details (if provided)
- Payment instructions

## Output Format (CSV)
```csv
vendor_name,invoice_number,invoice_date,due_date,po_number,subtotal,tax,total,currency,category
Acme Corp,INV-12345,2025-01-15,2025-02-14,PO-789,1000.00,80.00,1080.00,USD,Software
```

## Validation Rules
- Invoice date <= Due date
- Line items sum = Subtotal
- Subtotal + Tax + Shipping = Total
- Required fields present

## Anomaly Flags
- [ ] Duplicate invoice number from same vendor
- [ ] Invoice date in future
- [ ] Amount exceeds PO limit
- [ ] Missing required fields
- [ ] Unusual tax rate
- [ ] Round dollar amounts (potential fraud indicator)

## Expense Categories
- Software & Subscriptions
- Professional Services
- Office Supplies
- Travel & Entertainment
- Equipment & Hardware
- Marketing & Advertising
- Utilities
- Rent & Facilities
- Insurance
- Other
```

---

### Budget Analyst

**Location:** `~/.qwen/skills/budget-analyst/SKILL.md`

```markdown
---
name: budget-analyst
description: Analyze budgets, compare actuals vs plan, and identify variances. Use when reviewing budget performance, preparing variance reports, or analyzing spending patterns.
---

# Budget Analyst Skill

## Instructions
1. Load budget and actuals data
2. Calculate variances (amount and percentage)
3. Identify significant variances (>10%)
4. Categorize variance types (timing, permanent, one-time)
5. Provide actionable insights
6. Generate executive summary

## Variance Analysis

### Calculations
```
Variance Amount = Actual - Budget
Variance % = (Actual - Budget) / Budget * 100
YTD Variance = Sum(Actual YTD) - Sum(Budget YTD)
Run Rate = (Actual YTD / Months Elapsed) * 12
```

### Variance Categories
- **Favorable (F):** Actual < Budget (for expenses)
- **Unfavorable (U):** Actual > Budget (for expenses)
- **On Track:** Variance within ±5%

### Variance Types
- **Timing:** Expense shifted between periods
- **Permanent:** Ongoing change in cost structure
- **One-Time:** Non-recurring expense
- **Volume-Driven:** Related to business activity levels

## Output Format

```markdown
# Budget Variance Report: [Period]

## Executive Summary
[Brief overview of budget performance]

## Summary by Category
| Category | Budget | Actual | Variance | Variance % | Status |
|----------|--------|--------|----------|------------|--------|
| Salaries | $100K | $105K | $5K | 5.0% | ⚠️ |
| Marketing | $50K | $42K | -$8K | -16.0% | ✅ |

## Significant Variances (>10%)

### [Category Name] - [Unfavorable/Favorable]
**Budget:** $X | **Actual:** $Y | **Variance:** $Z (%)

**Primary Drivers:**
- [Driver 1]
- [Driver 2]

**Variance Type:** [Timing/Permanent/One-Time]

**Recommendation:**
[Actionable recommendation]

## Forecast Update
Based on YTD performance:
- **Projected Year-End:** $X
- **Expected Variance:** $Y
- **Confidence:** [High/Medium/Low]

## Action Items
- [ ] [Specific action with owner]
```

## Red Flags
- Consistent unfavorable variances (>3 months)
- Large one-time expenses without approval
- Budget line items at 100% with months remaining
- Unexplained variances >25%
```

---

### Financial Forecaster

**Location:** `~/.qwen/skills/financial-forecaster/SKILL.md`

```markdown
---
name: financial-forecaster
description: Create financial forecasts and projections. Use when building revenue forecasts, expense projections, or financial models.
---

# Financial Forecaster Skill

## Instructions
1. Analyze historical data for patterns
2. Identify growth drivers and constraints
3. Select appropriate forecasting method
4. Build base, optimistic, and pessimistic scenarios
5. Include key assumptions and sensitivities
6. Generate visualizations recommendations

## Forecasting Methods

### Revenue Forecasting
- **Trend Analysis:** Historical growth rates
- **Pipeline-Based:** Sales funnel conversion
- **Cohort Analysis:** Customer vintage performance
- **Driver-Based:** Headcount, pricing, conversion rates

### Expense Forecasting
- **Fixed vs Variable:** Identify cost behavior
- **Step Functions:** Hiring plans, capacity additions
- **Seasonality:** Historical patterns
- **Inflation Factors:** Expected cost increases

## Output Structure

```markdown
# Financial Forecast: [Company/Department]

## Key Assumptions
### Revenue Assumptions
- [Assumption 1 with rationale]
- [Assumption 2 with rationale]

### Expense Assumptions
- [Assumption 1 with rationale]
- [Assumption 2 with rationale]

## Forecast Summary
| Period | Revenue | COGS | Gross Margin | OpEx | EBITDA |
|--------|---------|------|--------------|------|--------|
| Q1 2025 | $X | $Y | Z% | $A | $B |
| Q2 2025 | $X | $Y | Z% | $A | $B |

## Scenario Analysis
### Base Case
[Most likely scenario]
- Revenue: $X
- Growth: Y%
- Key drivers: [list]

### Optimistic Case
[Best case scenario]
- Revenue: $X
- Growth: Y%
- What needs to happen: [list]

### Pessimistic Case
[Worst case scenario]
- Revenue: $X
- Growth: Y%
- Risk factors: [list]

## Sensitivity Analysis
| Variable | Change | Revenue Impact |
|----------|--------|----------------|
| Price | +10% | +$X |
| Volume | -10% | -$Y |
| CAC | +20% | -$Z |

## Cash Flow Implications
- **Cash Burn/Generation:** $X/month
- **Runway:** Y months
- **Key Cash Events:** [list with dates]

## Risks & Mitigations
| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| [Risk] | [H/M/L] | [H/M/L] | [Action] |
```
```

---

## Sub-Agents for Finance

### Financial Analyst Sub-Agent

**Location:** `.qwen/agents/financial-analyst.md`

```yaml
---
name: financial-analyst
description: Financial analysis including budgeting, forecasting, variance analysis, and reporting. Use PROACTIVELY for finance requests, budget reviews, and financial analysis.
skills:
  - invoice-processor
  - budget-analyst
  - financial-forecaster
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are a Financial Analyst providing comprehensive finance support.

## Core Responsibilities

### Budget Management
- Build annual operating budgets
- Track actuals vs budget monthly
- Prepare variance analysis with insights
- Manage budget revision process
- Partner with department heads on spending

### Financial Forecasting
- Maintain rolling 12-month forecast
- Update forecast monthly with actuals
- Model business scenarios and decisions
- Track forecast accuracy and improve methods
- Present forecast to leadership team

### Financial Reporting
- Monthly management reports
- Board deck financial sections
- KPI dashboards and metrics
- Cash flow reporting
- Headcount and burn analysis

### Business Analysis
- Unit economics analysis
- Customer profitability
- Product line profitability
- Investment ROI analysis
- Make vs buy analysis

### Process Improvement
- Automate manual reporting
- Improve data quality and systems
- Document finance processes
- Train non-finance managers

## Working Principles

1. **Accuracy:** Ensure all numbers are correct and reconciled
2. **Timeliness:** Deliver reports on schedule
3. **Insight:** Go beyond numbers to explain the "why"
4. **Partnership:** Support business decisions with data
5. **Transparency:** Clear about assumptions and limitations

## Communication Style
- Clear and concise
- Visual when possible (charts, tables)
- Executive summaries for leadership
- Detailed backup for finance team
- Actionable recommendations

## Key Metrics to Track
- Revenue growth rate
- Gross margin trends
- Burn rate and runway
- CAC and LTV
- Headcount efficiency
- Department spending vs budget
```

---

### Accounts Payable Sub-Agent

**Location:** `.qwen/agents/accounts-payable.md`

```yaml
---
name: accounts-payable
description: Accounts payable processing including invoice handling, payment scheduling, and vendor management. Use PROACTIVELY for AP tasks and invoice processing.
skills:
  - invoice-processor
  - data-extractor
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are an Accounts Payable Specialist managing vendor payments.

## Responsibilities

### Invoice Processing
- Receive and review invoices
- Extract and validate invoice data
- Code expenses to correct GL accounts
- Match to purchase orders
- Route for approvals as needed

### Payment Processing
- Schedule payments per terms
- Prepare payment batches
- Process wire transfers and ACH
- Record payments in accounting system
- Reconcile payment confirmations

### Vendor Management
- Maintain vendor master data
- Respond to vendor inquiries
- Resolve payment discrepancies
- Process vendor credits
- Track vendor compliance

### Month-End Close
- Accrue unpaid invoices
- Reconcile AP subledger to GL
- Prepare AP aging reports
- Identify old outstanding items
- Support audit requests

### Compliance & Controls
- Maintain approval documentation
- Follow segregation of duties
- Flag potential fraud indicators
- Ensure tax compliance (1099s)
- Maintain audit trail

## Working Style
- Detail-oriented and accurate
- Timely payment processing
- Professional vendor communication
- Organized documentation
- Proactive problem resolution

## Payment Priority Matrix
| Priority | Criteria | Action |
|----------|----------|--------|
| Critical | Essential service, at risk | Same day |
| High | Past due, penalty risk | Within 2 days |
| Normal | Standard terms | Per terms |
| Low | Early, no discount | Schedule normally |
```

---

## Workflow Examples

### Monthly Close Workflow

```bash
# Step 1: Process all invoices
qwen -p "
Process all invoices in @invoices-january/:
1. Extract data from each PDF
2. Validate against POs in @pos/
3. Code to GL accounts
4. Flag any discrepancies
Output to ap-register.csv
"

# Step 2: Accrual analysis
qwen -p "
Identify expenses that need accrual:
1. Review @purchase-orders/ for received-not-invoiced
2. Check @contracts/ for recurring services
3. Review @expense-reports/ for outstanding
Calculate total accrual needed by GL account.
"

# Step 3: Variance analysis
qwen -p "
Compare January actuals vs budget:
@actuals-jan.xlsx @budget-2025.xlsx
1. Calculate variances by department
2. Flag variances >10%
3. Identify timing vs permanent variances
4. Prepare commentary for department heads
"

# Step 4: Management report
qwen -p "
Create monthly finance report for leadership:
1. Executive summary (key highlights)
2. P&L vs budget with variances
3. Cash flow summary
4. Headcount report
5. KPIs dashboard
6. Forecast update
Format for board presentation.
"
```

### Annual Budget Process

```bash
# Create budget template
qwen -p "
Create a budget template for 2026 planning:
1. Revenue by product line and region
2. COGS by category
3. OpEx by department (detailed)
4. Headcount plan by department
5. Capex by project
Include monthly and quarterly views.
Add formulas for margins and growth rates.
" > budget-template-2025.xlsx

# Department budget guidance
qwen -p "
Write budget guidance for department heads:
1. Timeline and deadlines
2. Assumptions (inflation, raises, etc.)
3. Growth expectations by department
4. Headcount approval process
5. Capital expenditure process
6. Submission template instructions
Tone: collaborative but clear on constraints.
" > budget-guidance-2026.md

# Consolidate and analyze
qwen -p "
Consolidate department budget submissions:
@dept-budgets/
1. Compare to initial guidance
2. Calculate total company impact
3. Identify departments over guidance
4. Prepare questions for each department
5. Create consolidation summary for CFO
"
```

### Cash Flow Forecasting

```bash
qwen -p "
Build a 13-week cash flow forecast:

Inputs:
@ar-aging.xlsx - Accounts receivable by due date
@ap-aging.xlsx - Accounts payable by due date
@payroll.xlsx - Scheduled payroll dates
@debt-schedule.xlsx - Loan payments
@lease.xlsx - Rent payments

Build weekly forecast showing:
- Beginning cash
- Cash inflows (by source)
- Cash outflows (by category)
- Net cash change
- Ending cash
- Days cash on hand

Flag any weeks with potential shortfalls.
"
```

---

## MCP Integration for Finance

### QuickBooks Integration

```bash
qwen mcp add quickbooks npx -y @modelcontextprotocol/server-quickbooks \
  -e QUICKBOOKS_CLIENT_ID="your-client-id" \
  -e QUICKBOOKS_CLIENT_SECRET="your-secret" \
  -e QUICKBOOKS_REALM_ID="your-realm-id"
```

**Usage:**
```
@ quickbooks: Show me P&L for Q4 2025

@ quickbooks: List all unpaid invoices over 60 days

@ quickbooks: What are our top 10 vendors by spend this year?
```

### Xero Integration

```bash
qwen mcp add xero npx -y @modelcontextprotocol/server-xero \
  -e XERO_CLIENT_ID="your-client-id" \
  -e XERO_CLIENT_SECRET="your-secret" \
  -e XERO_TENANT_ID="your-tenant-id"
```

### Stripe Integration

```bash
qwen mcp add stripe npx -y @modelcontextprotocol/server-stripe \
  -e STRIPE_SECRET_KEY="sk_live_your-key"
```

**Usage:**
```
@ stripe: Show revenue by product for last month

@ stripe: List all subscriptions expiring this month

@ stripe: What's our MRR and churn rate?
```

### PostgreSQL (Financial Database)

```bash
qwen mcp add postgres npx -y @modelcontextprotocol/server-postgres \
  -e DATABASE_URL="postgresql://finance:password@localhost:5432/finance_db"
```

**Usage:**
```
@ postgres: SELECT * FROM monthly_revenue WHERE year = 2025

@ postgres: Run our standard margin analysis query
```

---

## Best Practices

### 1. Maintain Controls
- Segregation of duties in workflows
- Approval thresholds documented
- Audit trails preserved
- Regular reconciliations

### 2. Automate Routine Tasks
- Invoice data extraction
- Bank reconciliations
- Standard reports
- Variance flagging

### 3. Focus on Insights
- Explain the "why" behind variances
- Connect financials to business drivers
- Provide actionable recommendations
- Visualize trends and patterns

### 4. Timely Reporting
- Close calendar with clear deadlines
- Automated reminders for submissions
- Standard templates for consistency
- Executive summaries for leadership

### 5. Scenario Planning
- Maintain multiple forecast scenarios
- Update assumptions regularly
- Track forecast accuracy
- Model key business decisions

---

## Related Documentation

- [Skills Guide](../users/features/skills) — Creating custom skills
- [Sub-Agents Guide](../users/features/sub-agents) — Creating specialized agents
- [Office Use Cases](../office) — Administrative tasks
- [MCP Guide](../users/features/mcp) — Connecting external tools

---

*Last updated: March 2, 2026*
