# Agent Skills

## What Are Agent Skills?

**Agent Skills** are modular capabilities that extend Qwen Code's effectiveness. Each skill packages expertise into a discoverable format consisting of:

- A `SKILL.md` file with instructions the model can load when relevant
- Optional supporting files (scripts, templates, documentation)

### Key Distinction: Skills vs. Slash Commands

| Skills | Slash Commands |
|--------|----------------|
| **Model-invoked** — the model autonomously decides when to use them based on your request and the skill's description | **User-invoked** — you explicitly type `/command` |
| Discovered automatically when relevant | Must be manually triggered |

### How to Invoke Skills

Skills are typically auto-invoked by the model. To invoke explicitly:

```bash
/skills <skill-name>
```

Use autocomplete to browse available skills and descriptions.

---

## How Skills Work

### Discovery Locations

Qwen Code discovers skills from three sources:

1. **Personal Skills**: `~/.qwen/skills/` — Available across all projects
2. **Project Skills**: `.qwen/skills/` — Shared with team via git
3. **Extension Skills**: Provided by installed extensions

### Skill Structure

```
my-skill/
├── SKILL.md              # Required: Main skill definition
├── reference.md          # Optional: Additional documentation
├── examples.md           # Optional: Usage examples
├── scripts/
│   └── helper.py         # Optional: Utility scripts
└── templates/
    └── template.txt      # Optional: Templates
```

---

## Creating Custom Skills

### Step 1: Choose Skill Type

**Personal Skills** (individual use across all projects):
```bash
mkdir -p ~/.qwen/skills/my-skill-name
```

**Project Skills** (shared with team via git):
```bash
mkdir -p .qwen/skills/my-skill-name
```

### Step 2: Write SKILL.md

Create a `SKILL.md` file with YAML frontmatter:

```markdown
---
name: your-skill-name
description: Brief description of what this skill does and when to use it
---

# Your Skill Name

## Instructions
Provide clear, step-by-step guidance for Qwen Code.

## Examples
Show concrete examples of using this skill.
```

### Field Requirements

| Field | Requirement |
|-------|-------------|
| `name` | Non-empty string (required) |
| `description` | Non-empty string (required) |

**Recommended conventions:**
- Use lowercase letters, numbers, and hyphens in `name`
- Make `description` specific: include both what the skill does **and** when to use it (keywords users will naturally mention)

### Referencing Supporting Files

You can reference other files in your skill directory:

```markdown
For advanced usage, see [reference.md](reference.md).

Run the helper script:

```bash
python scripts/helper.py input.txt
```
```

---

## Examples

### Good vs. Bad Descriptions

**Too vague:**
```yaml
description: Helps with documents
```

**Specific (recommended):**
```yaml
description: Extract text and tables from PDF files, fill forms, merge documents. Use when working with PDFs, forms, or document extraction.
```

### Complete Skill Example

```markdown
---
name: pdf-processor
description: Extract text and tables from PDF files, fill forms, merge documents. Use when working with PDFs, forms, or document extraction.
---

# PDF Processor

## Instructions
1. Identify the PDF operation requested (extract, merge, fill form)
2. Use appropriate tools for the operation
3. Return structured output

## Examples
- "Extract text from this PDF"
- "Merge these PDF documents"
- "Fill out this PDF form"
```

### Testing Skill Example

```markdown
---
name: unit-test-generator
description: Writes comprehensive unit tests for any code file. Use when asked to write tests, add test coverage, or create test suites.
---

# Unit Test Generator

## Instructions
1. Analyze the code structure and identify all functions/methods
2. Identify edge cases, error conditions, and boundary values
3. Create comprehensive test suites with descriptive names
4. Include proper setup/teardown and meaningful assertions
5. Add comments explaining complex test scenarios

## Examples
- "Write tests for the authentication module"
- "Add unit tests to this file"
- "Create a test suite for the payment processor"
```

---

## Configuration & Management

### View Available Skills

Ask Qwen Code directly:
```
What skills are available?
```

Or inspect the filesystem:
```bash
# List personal skills
ls ~/.qwen/skills/

# List project skills
ls .qwen/skills/

# View specific skill content
cat ~/.qwen/skills/my-skill/SKILL.md
```

### Extension Skills

Extensions can provide custom skills automatically. To check which extensions provide skills, examine the extension's `qwen-extension.json` file for a `skills` field.

### Testing a Skill

After creating a skill, test it by asking questions matching your description:

```
Can you help me extract text from this PDF?
```

The model should autonomously decide to use your skill if it matches the request.

### Debugging Issues

If Qwen Code doesn't use your skill, check:

1. **Description specificity** — Is it detailed enough with trigger keywords?
2. **File path** — Verify correct location:
   ```bash
   # Personal
   ls ~/.qwen/skills/my-skill/SKILL.md
   
   # Project
   ls .qwen/skills/my-skill/SKILL.md
   ```
3. **YAML syntax** — Ensure valid frontmatter:
   ```bash
   cat SKILL.md | head -n 15
   ```
   - Opening `---` on line 1
   - Closing `---` before Markdown content
   - No tabs, correct indentation
4. **View errors** — Run with debug mode:
   ```bash
   qwen --debug
   ```

### Updating a Skill

Edit `SKILL.md` directly:
```bash
# Personal skill
code ~/.qwen/skills/my-skill/SKILL.md

# Project skill
code .qwen/skills/my-skill/SKILL.md
```

Changes take effect after restarting Qwen Code.

### Removing a Skill

```bash
# Personal
rm -rf ~/.qwen/skills/my-skill

# Project
rm -rf .qwen/skills/my-skill
git commit -m "Remove unused skill"
```

---

## Sharing Skills with Your Team

Project skills can be shared via git:

```bash
git add .qwen/skills/
git commit -m "Add team skill for PDF processing"
git push
```

Teammates automatically gain access after pulling the changes.

---

## Best Practices

### 1. Keep Skills Focused

One skill should address **one capability**:

| Focused ✅ | Too Broad ❌ |
|-----------|-------------|
| "PDF form filling" | "Document processing" |
| "Excel analysis" | (split into smaller skills) |
| "Git commit messages" | |

### 2. Write Clear Descriptions

Include specific triggers to help the model discover when to use skills:

```yaml
description: Analyze Excel spreadsheets, create pivot tables, and generate charts. Use when working with Excel files, spreadsheets, or .xlsx data.
```

### 3. Test with Your Team

Validate:
- Does the skill activate when expected?
- Are the instructions clear?
- Are there missing examples or edge cases?

### 4. Use Supporting Files

For complex skills, use supporting files:
- `reference.md` — Detailed documentation
- `examples.md` — Common use cases
- `scripts/` — Helper utilities
- `templates/` — Reusable templates

---

## Advanced: Skill with Scripts

```
api-documenter/
├── SKILL.md
├── templates/
│   └── api-template.md
└── scripts/
    └── generate-docs.py
```

**SKILL.md:**
```markdown
---
name: api-documenter
description: Generates comprehensive API documentation from source code. Use when asked to create API docs, document endpoints, or generate OpenAPI specs.
---

# API Documenter

## Instructions
1. Scan the source code for API endpoints (routes, controllers, handlers)
2. Extract request/response schemas
3. Generate documentation using the template
4. Run the generation script for complex projects

## Examples
- "Generate API documentation for this project"
- "Create OpenAPI spec from these endpoints"
- "Document all REST APIs"

## Script Usage
For large projects, run:
```bash
python scripts/generate-docs.py --output docs/api.md
```
```

---

## Benefits Summary

| Benefit | Description |
|---------|-------------|
| ✅ **Extend Capabilities** | Customize Qwen Code for your specific workflows |
| ✅ **Share Expertise** | Distribute team knowledge via git |
| ✅ **Reduce Prompting** | No need for repetitive instructions |
| ✅ **Compose Skills** | Combine multiple skills for complex tasks |
| ✅ **Auto-Discovery** | Model automatically finds relevant skills |

---

## Related Documentation

- [Sub-Agents](./sub-agents) — Create specialized AI assistants
- [Commands](./commands) — Slash commands, @ file injection, ! shell execution
- [MCP](./mcp) — Connect external tools and data sources

---

*Last updated: March 2, 2026*
