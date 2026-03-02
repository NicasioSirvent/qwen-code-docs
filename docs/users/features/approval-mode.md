# Approval Modes

## Overview

Qwen Code offers **four distinct permission modes** that control how AI interacts with your code and system. You can flexibly choose based on task complexity and risk level.

---

## Permission Modes Comparison

| Mode | File Editing | Shell Commands | Best For | Risk Level |
|------|-------------|----------------|----------|------------|
| **Plan** | ❌ Read-only analysis only | ❌ Not executed | Code exploration, planning complex changes, safe code review | Lowest |
| **Default** | ✅ Manual approval required | ✅ Manual approval required | New/unfamiliar codebases, critical systems, team collaboration, learning/teaching | Low |
| **Auto-Edit** | ✅ Auto-approved | ❌ Manual approval required | Daily development tasks, refactoring, code improvements, safe automation | Medium |
| **YOLO** | ✅ Auto-approved | ✅ Auto-approved | Trusted personal projects, automated scripts/CI/CD, batch processing | Highest |

---

## 1. Plan Mode

### Purpose
Instructs Qwen Code to create plans by analyzing the codebase with **read-only operations**.

### When to Use
- **Multi-step implementation**: When your feature requires edits to many files
- **Code exploration**: Research the codebase thoroughly before changing anything
- **Interactive development**: Iterate on direction with Qwen Code
- **Safe review**: Understanding code without making changes

### How to Use

**Switch during a session:**
```
Shift+Tab (or Tab on Windows) → cycle to Plan Mode
```
Indicated by `⏸ plan mode` at the bottom of the terminal.

**Start a new session:**
```bash
/approval-mode plan
```

**Run headless queries:**
```bash
qwen --prompt "What is machine learning?"
qwen -p "Analyze this codebase structure"
```

### Example
```
/approval-mode plan
I need to refactor our authentication system to use OAuth2. Create a detailed migration plan.
```

Qwen Code will:
1. Analyze current authentication implementation
2. Identify all files that need modification
3. Create a step-by-step migration plan
4. **Not make any changes** until you switch modes

### Configure as Default
```json
// .qwen/settings.json
{
  "permissions": {
    "defaultMode": "plan"
  }
}
```

---

## 2. Default Mode

### Purpose
Standard mode with **full manual control** over all potentially risky operations.

### When to Use
- **New to a codebase**: Exploring unfamiliar projects with extra caution
- **Critical systems**: Production code, infrastructure, sensitive data
- **Learning and teaching**: Understanding each step Qwen Code takes
- **Team collaboration**: Multiple people working on the same codebase
- **Complex operations**: Changes involving multiple files or complex logic

### How to Use

**Switch during a session:**
```
Shift+Tab (or Tab on Windows) → cycle to Default Mode
```
Indicated by the **absence** of any mode indicator at the terminal bottom.

**Start a new session:**
```bash
/approval-mode default
```

**Run headless queries:**
```bash
qwen --prompt "Analyze this code for potential bugs"
```

### Example
```
/approval-mode default
I need to add user profile pictures to our application. The pictures should be stored in an S3 bucket and the URLs saved in the database.
```

Qwen Code will ask for approval before:
1. Creating new files (controllers, models, migrations)
2. Modifying existing files (adding columns, updating APIs)
3. Running shell commands (database migrations, dependency installation)

### Configure as Default
```json
// .qwen/settings.json
{
  "permissions": {
    "defaultMode": "default"
  }
}
```

---

## 3. Auto-Edit Mode

### Purpose
**Automatically approves file edits** while requiring manual approval for shell commands.

### When to Use
- **Daily development**: Ideal for most coding tasks
- **Safe automation**: AI modifies code while preventing dangerous command execution
- **Team collaboration**: Shared projects to avoid unintended impacts
- **Refactoring**: Large-scale code improvements with test coverage

### How to Switch

**Via command:**
```bash
/approval-mode auto-edit
```

**Via keyboard shortcut:**
```
Shift+Tab (or Tab on Windows) → cycle from other modes
```

### Workflow Example

1. You ask Qwen Code to refactor a function
2. AI analyzes the code and proposes changes
3. **Automatically applies all file changes** without confirmation
4. If tests need to run, it **requests approval** to execute `npm test`

### Configure as Default
```json
// .qwen/settings.json
{
  "permissions": {
    "defaultMode": "auto-edit"
  }
}
```

---

## 4. YOLO Mode - Full Automation

### Purpose
Grants **highest permissions**, automatically approving all tool calls including file editing and shell commands.

### ⚠️ Security Warning

> **Use YOLO Mode with caution:** AI can execute **any command** with your terminal permissions. Ensure:
> 1. You trust the current codebase
> 2. You understand all actions AI will perform
> 3. Important files are backed up or committed to version control

### When to Use
- **Automated scripts**: Running predefined automated tasks
- **CI/CD pipelines**: Automated execution in controlled environments
- **Personal projects**: Rapid iteration in fully trusted environments
- **Batch processing**: Tasks requiring multi-step command chains

### How to Enable

**Temporarily (current session only):**
```bash
/approval-mode yolo
```

**Set as project default:**
```bash
/approval-mode yolo --project
```

**Set as user global default:**
```bash
/approval-mode yolo --user
```

**Via command-line:**
```bash
qwen --yolo
qwen --approval-mode yolo
```

### Configuration
```json
// .qwen/settings.json
{
  "permissions": {
    "defaultMode": "yolo",
    "confirmShellCommands": false,
    "confirmFileEdits": false
  }
}
```

### Automated Workflow Example

```bash
qwen --prompt "Run the test suite, fix all failing tests, then commit changes"
```

Without human intervention, AI will:
1. Run test commands (auto-approved)
2. Fix failed test cases (auto-edit files)
3. Execute git commit (auto-approved)

---

## Mode Switching & Configuration

### Keyboard Shortcut Switching

During a Qwen Code session, use **Shift+Tab** (or **Tab on Windows**) to cycle through modes:

```
Default Mode → Auto-Edit Mode → YOLO Mode → Plan Mode → Default Mode
```

The terminal status bar shows your current mode at all times:

| Mode Display | Current Mode |
|--------------|--------------|
| (no indicator) | Default Mode |
| `⚡ auto-edit` | Auto-Edit Mode |
| `🚀 yolo` | YOLO Mode |
| `⏸ plan mode` | Plan Mode |

### Persistent Configuration

**Project-level:** `./.qwen/settings.json`
**User-level:** `~/.qwen/settings.json`

```json
{
  "permissions": {
    "defaultMode": "auto-edit",  // "plan", "default", "auto-edit", or "yolo"
    "confirmShellCommands": true,
    "confirmFileEdits": true
  }
}
```

### Command-Line Options

```bash
# Set mode for this session
qwen --approval-mode plan

# YOLO mode shortcut
qwen --yolo

# Headless with specific mode
qwen -p "analyze this" --approval-mode default
```

---

## Security Implications

| Mode | Security Risk | Mitigation |
|------|--------------|------------|
| **Plan** | Minimal — read-only | None needed |
| **Default** | Low — manual review required | Review each change carefully |
| **Auto-Edit** | Medium — auto file changes | Ensure code is backed up; shell commands still require approval |
| **YOLO** | **High** — full automation | Only use in trusted environments; backup/commit before use |

### Best Security Practices

1. **Always commit before YOLO**: `git add . && git commit -m "WIP"`
2. **Use Plan mode for exploration**: Understand before modifying
3. **Default for production**: Manual approval for critical systems
4. **Auto-Edit for daily work**: Balance of safety and efficiency
5. **Review shell commands**: Even in Auto-Edit, review command approvals

---

## Best Practices & Recommendations

### Scenario-Based Mode Selection

| Scenario | Recommended Mode | Rationale |
|----------|-----------------|-----------|
| Understanding codebase | Plan | Safe exploration without changes |
| Planning complex changes | Plan | Create detailed plan first |
| Working on production code | Default | Manual review for critical changes |
| Team collaboration | Default or Auto-Edit | Balance safety with efficiency |
| Daily coding tasks | Auto-Edit | Efficient for routine work |
| Refactoring with tests | Auto-Edit | Auto-apply safe changes |
| CI/CD automation | YOLO | Full automation in controlled env |
| Personal trusted projects | YOLO | Maximum efficiency |

### Workflow Tips

1. **Start with Plan**: Explore and plan before making changes
2. **Switch to Auto-Edit**: Apply planned changes efficiently
3. **Use YOLO sparingly**: Only for trusted, repetitive tasks
4. **Default for review**: When learning or auditing code

### Quick Reference Guide

```
┌─────────────────────────────────────────────────────────────┐
│                    APPROVAL MODE FLOW                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   Plan Mode                                                 │
│   └─→ "What files need to change?"                         │
│                                                             │
│   Default Mode                                              │
│   └─→ "Review each change carefully"                       │
│                                                             │
│   Auto-Edit Mode                                            │
│   └─→ "Auto-apply file changes, ask for commands"          │
│                                                             │
│   YOLO Mode                                                 │
│   └─→ "Full automation - use with caution!"                │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Troubleshooting

### Mode Not Switching

1. **Check keyboard shortcut**: Use `Shift+Tab` (not just `Tab` on non-Windows)
2. **Verify command**: `/approval-mode <mode>` with correct spelling
3. **Restart session**: Some changes require new session

### Unexpected Approval Prompts

1. **Check current mode**: Look at terminal status bar
2. **Verify settings**: Check `.qwen/settings.json` for overrides
3. **Tool-specific settings**: Some tools may have individual approval settings

---

## Related Documentation

- [Commands](./commands) — `/approval-mode` command reference
- [Configuration](../configuration/settings) — Permission settings
- [Security](../configuration/settings#security) — Security configuration
- [Headless Mode](./headless) — Automation with approval modes

---

*Last updated: March 2, 2026*
