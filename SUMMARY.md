# Qwen Code Documentation Replication Summary

## Overview

This repository contains comprehensive documentation for **Qwen Code** — an open-source AI coding agent that lives in your terminal. The documentation has been updated with the latest features including Skills, Sub-Agents, enhanced Approval Modes, MCP integration, and extensive use cases beyond software development.

**Last Updated:** March 2, 2026  
**Qwen Code Version:** v0.6.0+

---

## Files Created and Updated

### Root Directory
| File | Description |
|------|-------------|
| `README.md` | Main overview with features, installation, and quick start |
| `TOC.md` | Table of contents for all documentation |
| `SUMMARY.md` | This summary document |
| `beyond-code-assistance.md` | Additional use cases beyond code assistance |

### User Documentation (`docs/users/`)

#### Getting Started
| File | Description |
|------|-------------|
| `quickstart.md` | Quick start guide with installation and first session |
| `common-workflow.md` | Common workflows with practical examples |

#### Features (`docs/users/features/`)
| File | Description | Status |
|------|-------------|--------|
| `skills.md` | **NEW** — Agent Skills for modular capabilities | ✅ Updated |
| `sub-agents.md` | **NEW** — Specialized AI assistants | ✅ Updated |
| `commands.md` | **NEW** — Slash, @, and ! commands | ✅ Updated |
| `approval-mode.md` | Four permission modes (Plan, Default, Auto-Edit, YOLO) | ✅ Updated |
| `mcp.md` | Model Context Protocol for external tools | ✅ Updated |
| `headless.md` | Non-interactive automation and CI/CD | ✅ Updated |
| `vision-models.md` | Vision and multimodal capabilities | ✅ Updated |

#### Configuration (`docs/users/configuration/`)
| File | Description | Status |
|------|-------------|--------|
| `auth.md` | OAuth and API key authentication | 📁 Existing |
| `settings.md` | **NEW** — Complete settings reference | ✅ Created |

#### IDE Integration
| File | Description |
|------|-------------|
| `integration-vscode.md` | VS Code extension |
| `integration-zed.md` | Zed integration |
| `integration-jetbrains.md` | JetBrains IDEs integration |

#### Use Cases (`docs/use-cases/`) — **NEW SECTION**
| File | Description |
|------|-------------|
| `README.md` | **NEW** — Overview of use cases beyond software development |
| `office/README.md` | **NEW** — Email, documents, spreadsheets, scheduling with skills & agents |
| `hr/README.md` | **NEW** — Job descriptions, resume screening, onboarding with sub-agents |
| `finance/README.md` | **NEW** — Invoices, budgets, forecasts with MCP integrations |
| `marketing/README.md` | **NEW** — Content creation, social media, SEO with skills |
| `legal/README.md` | **NEW** — Contract review, compliance audits, legal research |
| `sales/README.md` | **NEW** — Proposals, health scoring, churn analysis |
| `personal/README.md` | **NEW** — Personal finance, travel planning, study guides |

### Developer Documentation (`docs/developers/`)

| File | Description | Status |
|------|-------------|--------|
| `architecture.md` | System architecture with Skills, Sub-Agents, Tools | ✅ Updated |
| `tools/introduction.md` | Built-in tools reference | 📁 Existing |
| `roadmap.md` | Development roadmap and planned features | 📁 Existing |

---

## Key Updates in This Version

### 1. Agent Skills (Experimental)
- Model-invoked modular capabilities
- Personal, Project, and Extension skills
- SKILL.md format with YAML frontmatter
- Skill discovery and loading system
- **20+ example skills** for business and personal use

### 2. Sub-Agents System
- Specialized AI assistants for specific tasks
- Built-in agents: Testing, Documentation, Code Review, React, Python
- **15+ business sub-agents**: HR, Finance, Marketing, Legal, Sales, Personal
- Custom sub-agent creation with `/agents create`
- Sub-agents using skills together

### 3. Enhanced Approval Modes
- **Plan Mode**: Read-only analysis
- **Default Mode**: Manual approval for all changes
- **Auto-Edit Mode**: Auto-approve file edits
- **YOLO Mode**: Full automation
- Keyboard shortcut switching (Shift+Tab)

### 4. Commands System
- **Slash Commands** (`/`): Session control, settings, help
- **At Commands** (`@`): File and directory injection
- **Exclamation Commands** (`!`): Shell execution
- Custom commands via Markdown files

### 5. MCP Integration
- HTTP, SSE, and Stdio transports
- Server configuration and management
- **Business tool integrations**: Salesforce, HubSpot, Google Workspace, Slack, QuickBooks, Stripe
- Tool filtering and trust settings

### 6. Headless Mode
- Non-interactive execution with `--prompt`
- JSON and stream-json output formats
- CI/CD integration examples
- Environment variable configuration

### 7. Configuration System
- Complete settings reference
- Configuration layers and precedence
- Environment variables support
- Context files (QWEN.md)

### 8. Use Cases Documentation
- **Office & Administrative**: Email drafting, meeting minutes, document formatting, scheduling
- **HR & Recruiting**: Job descriptions, resume screening, performance reviews, onboarding
- **Finance & Accounting**: Invoice processing, budget analysis, financial forecasting
- **Marketing & Content**: Content calendars, social media posts, SEO optimization
- **Legal & Compliance**: Contract review, clause extraction, compliance audits
- **Sales & Customer Success**: Proposal writing, health scoring, QBR preparation
- **Personal & Home**: Budget management, travel planning, study guides, home projects

---

## New Features Summary

| Feature | Version | Description |
|---------|---------|-------------|
| Skills | v0.6.0 | Extensible custom AI capabilities |
| Sub-Agents | v0.0.11+ | Dedicated agent system for task delegation |
| Multi-Model Support | v0.1.0+ | Switch between Qwen, Anthropic, OpenAI |
| Anthropic Provider | v0.7.0 | Claude model support |
| Multimodal Input | v0.6.0 | Image, PDF, audio, video support |
| LSP Support | v0.7.0 | Experimental language server protocol |
| Extension System | v0.8.0 | Custom extensions with skills, agents, commands |
| VS Code Extension | v0.5.0 | Native IDE integration |
| GitHub Actions | v0.5.0 | CI/CD automation |

---

## Documentation Structure

```
qwen-code-docs/
├── README.md                 # Main overview
├── TOC.md                    # Table of contents
├── SUMMARY.md                # This file
├── beyond-code-assistance.md # Additional use cases
└── docs/
    ├── users/
    │   ├── quickstart.md
    │   ├── common-workflow.md
    │   ├── configuration/
    │   │   ├── auth.md
    │   │   └── settings.md
    │   ├── features/
    │   │   ├── skills.md
    │   │   ├── sub-agents.md
    │   │   ├── commands.md
    │   │   ├── approval-mode.md
    │   │   ├── mcp.md
    │   │   ├── headless.md
    │   │   └── vision-models.md
    │   ├── integration-*.md
    │   └── use-cases/        # NEW
    │       ├── README.md
    │       ├── office/
    │       ├── hr/
    │       ├── finance/
    │       ├── marketing/
    │       ├── legal/
    │       ├── sales/
    │       └── personal/
    └── developers/
        ├── architecture.md
        ├── tools/
        │   └── introduction.md
        └── roadmap.md
```

---

## Quick Reference

### Installation
```bash
npm install -g @qwen-code/qwen-code@latest
```

### First Session
```bash
cd your-project
qwen
```

### Common Commands
```
/help          - Show available commands
/skills        - List and use skills
/agents        - Manage sub-agents
/mcp           - Manage MCP servers
/approval-mode - Change permission mode
/compress      - Compress conversation history
```

### Headless Usage
```bash
qwen -p "analyze this codebase"
qwen -p "run tests and fix failures" --yolo
```

### Create a Skill
```bash
mkdir -p ~/.qwen/skills/my-skill
# Create SKILL.md with instructions
```

### Create a Sub-Agent
```bash
/agents create
# Follow the wizard to define your agent
```

---

## Related Resources

- **GitHub Repository**: https://github.com/QwenLM/qwen-code
- **Official Documentation**: https://qwenlm.github.io/qwen-code-docs/
- **NPM Package**: https://www.npmjs.com/package/@qwen-code/qwen-code
- **VS Code Extension**: https://marketplace.visualstudio.com/items?itemName=qwenlm.qwen-code-vscode-ide-companion

---

*Documentation maintained by the Qwen Code community. Contributions welcome!*
