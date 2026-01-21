# Qwen Code Documentation

## Overview

Qwen Code is an open-source AI coding assistant that lives in your terminal and helps developers understand, navigate, and build code faster. Built specifically for the Qwen3-Coder model, it provides powerful agentic capabilities through a command-line interface while also offering seamless IDE integration options.

Qwen Code transforms how you interact with your codebase by providing intelligent assistance that goes beyond simple code completion. It combines deep codebase understanding with practical action-taking capabilities to accelerate your development workflow.

## Get started in 30 seconds

Prerequisites:

- A [Qwen Code](https://chat.qwen.ai/auth?mode=register) account
- Requires [Node.js 20+](https://nodejs.org/zh-cn/download), you can use `node -v` to check the version. If it's not installed, use the following command to install it.

### Install Qwen Code:

**NPM**(recommended)

```bash
npm install -g @qwen-code/qwen-code@latest
```

**Homebrew**(macOS, Linux)

```bash
brew install qwen-code
```

### Start using Qwen Code:

```bash
cd your-project
qwen
```

Select **Qwen OAuth (Free)** authentication and follow the prompts to log in. Then let's start with understanding your codebase. Try one of these commands:

```
what does this project do?
```

![](https://cloud.video.taobao.com/vod/j7-QtQScn8UEAaEdiv619fSkk5p-t17orpDbSqKVL5A.mp4)

You'll be prompted to log in on first use. That's it! [Continue with Quickstart (5 mins) →](./docs/users/quickstart)

> [!tip]
>
> See [troubleshooting](./docs/users/support/troubleshooting) if you hit issues.

> [!note]
>
> **New VS Code Extension (Beta)**: Prefer a graphical interface? Our new **VS Code extension** provides an easy-to-use native IDE experience without requiring terminal familiarity. Simply install from the marketplace and start coding with Qwen Code directly in your sidebar. Download and install the [Qwen Code Companion](https://marketplace.visualstudio.com/items?itemName=qwenlm.qwen-code-vscode-ide-companion) now.

## What Qwen Code does for you

- **Build features from descriptions**: Tell Qwen Code what you want to build in plain language. It will make a plan, write the code, and ensure it works.
- **Debug and fix issues**: Describe a bug or paste an error message. Qwen Code will analyze your codebase, identify the problem, and implement a fix.
- **Navigate any codebase**: Ask anything about your team's codebase, and get a thoughtful answer back. Qwen Code maintains awareness of your entire project structure, can find up-to-date information from the web, and with [MCP](./docs/users/features/mcp) can pull from external datasources like Google Drive, Figma, and Slack.
- **Automate tedious tasks**: Fix fiddly lint issues, resolve merge conflicts, and write release notes. Do all this in a single command from your developer machines, or automatically in CI.

## Why developers love Qwen Code

- **Works in your terminal**: Not another chat window. Not another IDE. Qwen Code meets you where you already work, with the tools you already love.
- **Takes action**: Qwen Code can directly edit files, run commands, and create commits. Need more? [MCP](./docs/users/features/mcp) lets Qwen Code read your design docs in Google Drive, update your tickets in Jira, or use _your_ custom developer tooling.
- **Unix philosophy**: Qwen Code is composable and scriptable. `tail -f app.log | qwen -p "Slack me if you see any anomalies appear in this log stream"` _works_. Your CI can run `qwen -p "If there are new text strings, translate them into French and raise a PR for @lang-fr-team to review"`.

## Key Features

### Build Features from Descriptions
Transform plain language requirements into working code by describing what you want to build. Qwen Code creates implementation plans, writes the actual code, and ensures it works through automated testing and validation. This natural-language-to-code approach dramatically reduces the time between idea and implementation.

### Debug and Fix Issues
Resolve bugs quickly by describing the problem or pasting error messages. Qwen Code analyzes your entire codebase to identify root causes, suggests fixes, and can even implement the solution directly with your approval. The system understands context across files and dependencies, making it effective at solving complex debugging challenges.

### Navigate Any Codebase
Ask questions about your team's codebase and receive thoughtful, context-aware answers. Qwen Code maintains awareness of your entire project structure, can find up-to-date information from the web, and through Model Context Protocol (MCP) can pull from external data sources like Google Drive, databases, or custom APIs.

### Automate Tedious Tasks
Eliminate repetitive work through intelligent automation capabilities. Fix linting issues, resolve merge conflicts, write release notes, and perform other routine development tasks with a single command. These operations work on your local development machine or can be integrated into CI/CD pipelines for automated workflows.

## Architecture Overview

Qwen Code is built with a modular architecture that separates user-facing concerns from core AI orchestration, enabling flexible deployment and extensibility. The system consists of two primary packages working together through a well-defined interface.

The CLI package (packages/cli) handles all user interactions, including input processing, command handling, display rendering, and theme customization. It communicates with the Core package (packages/core), which manages API communication with the Qwen model, tool orchestration, and state management. The tool system provides extensible capabilities through built-in tools and MCP server integrations.

### Key Components

#### Terminal-First Design
Built for developers who live in the command line, Qwen Code integrates naturally with your existing workflow. It's not another chat window or separate IDE—it meets you where you already work with the tools you already love. The system follows Unix philosophy principles, making it composable and scriptable for seamless integration into existing pipelines.

#### Four Usage Modes
Qwen Code adapts to different working styles and automation needs through multiple usage patterns:

| Mode | Best For | Example |
|------|----------|---------|
| Interactive | Daily development work | `qwen` in your project folder |
| Headless | Scripts and CI/CD automation | `qwen -p "run tests"` |
| IDE Integration | Visual development experience | VS Code, Zed, JetBrains extensions |
| TypeScript SDK | Building custom AI tools | Programmatically embed in applications |

#### Subagents System
Break complex tasks into specialized subtasks handled by dedicated subagents. Each subagent focuses on specific capabilities like file editing, shell execution, or web searching, working together under the coordination of the main system. This enables more reliable handling of multi-step operations and better specialization for different types of work.

#### Built-in Tools
Access a rich set of built-in capabilities that extend Qwen Code's functionality without requiring additional configuration:

- **File Operations**: Read, write, and edit files with intelligent diff management
- **Shell Commands**: Execute system commands with configurable approval requirements
- **Search Tools**: Find files and search content using ripgrep-powered search
- **Web Capabilities**: Fetch web content and perform web searches
- **Smart Edit**: Context-aware editing that preserves code structure and formatting

#### Approval Modes
Control how Qwen Code interacts with your system through four permission modes designed for different risk levels and use cases:

| Mode | File Editing | Shell Commands | Best Use |
|------|--------------|----------------|----------|
| Plan | Read-only only | Not executed | Code exploration and planning |
| Default | Manual approval | Manual approval | New codebases and critical systems |
| Auto-Edit | Auto-approved | Manual approval | Daily development tasks |
| YOLO | Auto-approved | Auto-approved | Trusted automation and CI/CD |

Cycle through modes during sessions using Shift+Tab for flexible permission control based on your current task.

#### Agent Skills
Extend Qwen Code's capabilities through modular, discoverable skills. Skills are organized folders containing instructions (and optionally scripts/resources) that the model can autonomously invoke based on your request context. Unlike slash commands which require explicit invocation, skills are model-invoked, allowing for more natural and contextual assistance.

## Why Developers Choose Qwen Code

### Open Source and Co-Evolving
Both the framework and the Qwen3-Coder model are open-source, shipping and evolving together. This transparency allows you to understand how the system works, contribute improvements, and avoid vendor lock-in. The active development community ensures rapid iteration and continuous improvement.

### OpenAI-Compatible Authentication
Choose between two authentication methods based on your needs: use Qwen OAuth for 2,000 free requests per day, or configure an OpenAI-compatible API key for private deployments. This flexibility supports everything from personal experimentation to enterprise integration without mandatory vendor dependencies.

### Rich Agentic Workflow
Qwen Code provides a full agentic workflow experience similar to other advanced AI coding assistants, featuring sophisticated capabilities like Plan Mode for safe exploration, Subagents for specialized task handling, and MCP integration for connecting to external tools and data sources. These features work together to provide comprehensive assistance throughout the development lifecycle.

### IDE-Friendly Integration
While terminal-first by design, Qwen Code offers optional integrations for VS Code, Zed, and JetBrains IDEs. These integrations provide native graphical interfaces while maintaining access to the same powerful underlying capabilities, giving you the flexibility to work in whatever environment suits your preferences.

## Getting Started in 30 Seconds

### Prerequisites
- Node.js 20+ (check with `node -v`)
- A Qwen Code account

### Installation

#### NPM (Recommended)
```bash
npm install -g @qwen-code/qwen-code@latest
```

#### Homebrew (macOS, Linux)
```bash
brew install qwen-code
```

### First Session
Navigate to your project directory and start Qwen Code:

```bash
cd your-project
qwen
```

Select Qwen OAuth (Free) authentication and follow the browser prompts to log in. Once authenticated, you can start exploring your codebase with natural language queries like "what does this project do?" or "explain the main architecture."

Your OAuth credentials are cached locally after the first login, so you typically won't need to re-authenticate on subsequent sessions. Run `/auth` anytime to switch authentication methods or accounts.

## What's Next

After getting Qwen Code installed and running, explore more advanced features and integration options:

- Continue with the Quick Start guide for a comprehensive introduction to core workflows
- Learn about different Authentication Methods including OAuth and API keys
- Explore advanced capabilities in the Deep Dive section, including Subagents System, Built-in Tools Reference, and Model Context Protocol (MCP)
- Set up IDE Integration for VS Code, Zed, or JetBrains
- Build custom applications with the TypeScript SDK starting with SDK Quick Start