# Qwen Code Documentation

## Overview

Qwen Code is an open-source AI coding agent that lives in your terminal, helping developers understand, navigate, and build code faster. Built specifically for the Qwen3-Coder model family, it provides powerful agentic capabilities through a command-line interface while also offering seamless IDE integration options.

Qwen Code transforms how you interact with your codebase by providing intelligent assistance that goes beyond simple code completion. It combines deep codebase understanding with practical action-taking capabilities to accelerate your development workflow.

## Get Started in 30 Seconds

### Prerequisites

- A [Qwen Code](https://chat.qwen.ai/auth?mode=register) account
- Node.js 20+ (check with `node -v`)

### Installation

**NPM** (recommended)
```bash
npm install -g @qwen-code/qwen-code@latest
```

**Homebrew** (macOS, Linux)
```bash
brew install qwen-code
```

### Start Using Qwen Code

```bash
cd your-project
qwen
```

Select **Qwen OAuth (Free)** authentication and follow the prompts to log in. Then start exploring your codebase:

```
what does this project do?
explain the main architecture
```

You'll be prompted to log in on first use. That's it! [Continue with Quickstart (5 mins) →](./docs/users/quickstart)

> [!tip]
> See [troubleshooting](./docs/users/support/troubleshooting) if you hit issues.

> [!note]
> **VS Code Extension (Beta)**: Prefer a graphical interface? Our **VS Code extension** provides an easy-to-use native IDE experience. Install [Qwen Code Companion](https://marketplace.visualstudio.com/items?itemName=qwenlm.qwen-code-vscode-ide-companion) from the marketplace.

---

## What Qwen Code Does

| Capability | Description |
|------------|-------------|
| **Build Features** | Tell Qwen Code what you want to build in plain language. It creates a plan, writes the code, and ensures it works. |
| **Debug & Fix** | Describe a bug or paste an error message. Qwen Code analyzes your codebase, identifies the problem, and implements a fix. |
| **Navigate Codebases** | Ask anything about your team's codebase. Qwen Code maintains awareness of your entire project structure. |
| **Automate Tasks** | Fix lint issues, resolve merge conflicts, write release notes. Works locally or in CI/CD pipelines. |

---

## Why Developers Love Qwen Code

- **Terminal-First Design**: Not another chat window. Qwen Code meets you where you already work.
- **Takes Action**: Can edit files, run commands, and create commits. With [MCP](./docs/users/features/mcp), connect to Google Drive, Jira, Slack, and more.
- **Unix Philosophy**: Composable and scriptable. Pipe logs: `tail -f app.log | qwen -p "Slack me if you see anomalies"`.
- **Open Source**: Both the framework and Qwen3-Coder models are open-source (Apache 2.0).
- **Flexible Authentication**: Qwen OAuth (2,000 free requests/day) or OpenAI-compatible API keys.

---

## Key Features

### 1. Agent Skills (Experimental)

**Skills** are modular capabilities that extend Qwen Code's effectiveness. Each skill packages expertise into a discoverable format.

| Skills vs. Slash Commands |
|---------------------------|
| **Skills**: Model-invoked — the AI autonomously decides when to use them |
| **Slash Commands**: User-invoked — you explicitly type `/command` |

**Skill Locations:**
- Personal: `~/.qwen/skills/`
- Project: `.qwen/skills/`
- Extensions: Provided by installed extensions

**Example Skill Structure:**
```
my-skill/
├── SKILL.md (required)
├── reference.md (optional)
├── scripts/helper.py (optional)
└── templates/template.txt (optional)
```

[Learn more →](./docs/users/features/skills)

### 2. Sub-Agents

**Sub-agents** are specialized AI assistants that handle specific types of tasks. They maintain separate context and can be configured with specific tools.

**Built-in Sub-agents:**
- Testing Specialist — writes comprehensive unit/integration tests
- Documentation Writer — creates README, API docs, user guides
- Code Reviewer — reviews for security, performance, best practices
- React Specialist — modern React development with hooks
- Python Expert — Python frameworks, testing, data science

**Create Custom Sub-agents:**
```bash
/agents create
```

[Learn more →](./docs/users/features/sub-agents)

### 3. Approval Modes

Control how Qwen Code interacts with your system through four permission modes:

| Mode | File Editing | Shell Commands | Best For |
|------|--------------|----------------|----------|
| **Plan** | Read-only | Not executed | Code exploration, planning |
| **Default** | Manual approval | Manual approval | New codebases, critical systems |
| **Auto-Edit** | Auto-approved | Manual approval | Daily development tasks |
| **YOLO** | Auto-approved | Auto-approved | Trusted automation, CI/CD |

**Switch modes:** `Shift+Tab` during session or `/approval-mode <mode>`

[Learn more →](./docs/users/features/approval-mode)

### 4. Model Context Protocol (MCP)

Connect Qwen Code to external tools, databases, and APIs through MCP servers.

**Add an MCP Server:**
```bash
qwen mcp add --transport http my-server http://localhost:3000/mcp
qwen mcp list
```

**Configuration Scopes:**
- Project: `.qwen/settings.json`
- User: `~/.qwen/settings.json`

[Learn more →](./docs/users/features/mcp)

### 5. Built-in Tools

| Tool Category | Tools |
|---------------|-------|
| **File Operations** | Read, write, edit files with intelligent diff management |
| **Shell Commands** | Execute system commands with configurable approval |
| **Search** | File search, content search (ripgrep-powered) |
| **Web** | Web fetch, web search (Tavily API) |
| **Task Management** | TodoWrite, Task tool for sub-agent delegation |
| **Memory** | Persistent context across sessions |

[Learn more →](./docs/developers/tools/introduction)

### 6. Commands System

Qwen Code supports three command types:

| Prefix | Type | Examples |
|--------|------|----------|
| `/` | Slash Commands | `/help`, `/clear`, `/compress`, `/mcp`, `/skills`, `/agents` |
| `@` | File Injection | `@src/main.py explain this`, `@docs/ summarize` |
| `!` | Shell Execution | `!git status`, `!npm test` |

[Learn more →](./docs/users/features/commands)

---

## Usage Modes

| Mode | Best For | Example |
|------|----------|---------|
| **Interactive** | Daily development | `qwen` in your project folder |
| **Headless** | Scripts and CI/CD | `qwen -p "run tests"` |
| **IDE Integration** | Visual development | VS Code, Zed, JetBrains extensions |
| **TypeScript SDK** | Custom AI tools | Programmatically embed in applications |

---

## Configuration

### Settings Files

| Location | Scope |
|----------|-------|
| `~/.qwen/settings.json` | User-level (all projects) |
| `.qwen/settings.json` | Project-level (current project) |

### Environment Variables

```bash
# API Configuration
export QWEN_API_KEY="your-api-key"

# Sandbox Mode
export GEMINI_SANDBOX="docker"

# Debug Mode
export DEBUG="true"
```

### Command-Line Arguments

```bash
qwen --model qwen3-coder-plus
qwen --prompt "analyze this codebase"
qwen --approval-mode auto-edit
qwen --sandbox
qwen --debug
```

[Full Configuration Reference →](./docs/users/configuration/settings)

---

## IDE Integrations

| IDE | Extension |
|-----|-----------|
| **VS Code** | [Qwen Code Companion](https://marketplace.visualstudio.com/items?itemName=qwenlm.qwen-code-vscode-ide-companion) |
| **Zed** | Built-in integration |
| **JetBrains** | IntelliJ IDEA, PyCharm, WebStorm, GoLand |

[View Integration Docs →](./docs/users/integration-vscode)

---

## Architecture Overview

Qwen Code uses a modular architecture:

```
┌─────────────────────────────────────────────────────────────┐
│                      CLI Package                            │
│  (packages/cli) - User interactions, input/output, themes   │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      Core Package                           │
│  (packages/core) - API communication, tool orchestration    │
└─────────────────────────────────────────────────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
       ┌──────────┐   ┌──────────┐   ┌──────────────┐
       │ Built-in │   │   MCP    │   │  Sub-agents  │
       │  Tools   │   │  Servers │   │   System     │
       └──────────┘   └──────────┘   └──────────────┘
```

[Architecture Details →](./docs/developers/architecture)

---

## Roadmap

### Completed (Phase 1-2)
- ✅ Terminal UI, OAuth, Settings, Themes
- ✅ Skills (Experimental), Sub-Agents, Headless Mode
- ✅ MCP, Multi-Model Support, Plan Mode
- ✅ VS Code Extension, GitHub Actions
- ✅ Anthropic Provider, Multimodal Input (images, PDFs, video)
- ✅ LSP Support (Experimental), Concurrent Runner

### In Progress / Planned
- 🔄 Cross-platform Compatibility (Windows/Linux/macOS)
- 🔄 Hooks System for Extensions
- 📅 Better UI, Onboarding Flow, Permission System
- 📅 Cost Tracking, Management Dashboard

[Roadmap Details →](./docs/developers/roadmap)

---

## What's Next

After getting started, explore:

### User Documentation
- [Quick Start Guide](./docs/users/quickstart) — Comprehensive introduction
- [Common Workflows](./docs/users/common-workflow) — Best practices
- [Skills](./docs/users/features/skills) — Create custom AI skills
- [Sub-Agents](./docs/users/features/sub-agents) — Specialized AI assistants
- [Approval Modes](./docs/users/features/approval-mode) — Control permissions
- [MCP](./docs/users/features/mcp) — Connect external tools
- [Commands](./docs/users/features/commands) — Slash, @, ! commands
- [Headless Mode](./docs/users/features/headless) — Automation & CI/CD
- [Configuration](./docs/users/configuration/settings) — All settings reference

### Use Cases (Beyond Code)
- [Overview](./docs/use-cases/README.md) — Qwen Code for non-development tasks
- [Office & Admin](./docs/use-cases/office/README.md) — Email, documents, scheduling
- [HR & Recruiting](./docs/use-cases/hr/README.md) — Job descriptions, resume screening
- [Finance & Accounting](./docs/use-cases/finance/README.md) — Invoices, budgets, forecasts
- [Marketing & Content](./docs/use-cases/marketing/README.md) — Content creation, social media
- [Legal & Compliance](./docs/use-cases/legal/README.md) — Contract review, compliance audits
- [Sales & Customer Success](./docs/use-cases/sales/README.md) — Proposals, health scoring
- [Personal & Home](./docs/use-cases/personal/README.md) — Finance, travel, education

### Developer Documentation
- [Architecture](./docs/developers/architecture) — System design
- [Tools Reference](./docs/developers/tools/introduction) — Built-in tools
- [Roadmap](./docs/developers/roadmap) — Development plan

### Additional Resources
- [Beyond Code Assistance](./beyond-code-assistance.md) — Research, education, business automation

---

**Last Updated:** March 2, 2026  
**Version:** Qwen Code v0.6.0+
