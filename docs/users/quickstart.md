# Quickstart

> 👏 Welcome to Qwen Code!

This quickstart guide will have you using AI-powered coding assistance in just a few minutes.

## Before You Begin

Make sure you have:

- A **terminal** or command prompt open
- A code project to work with
- Node.js 20+ (check with `node -v`)

## Step 1: Install Qwen Code

### NPM (Recommended)

```bash
npm install -g @qwen-code/qwen-code@latest
```

### Homebrew (macOS, Linux)

```bash
brew install qwen-code
```

## Step 2: Start Your First Session

Navigate to your project and start Qwen Code:

```bash
cd your-project
qwen
```

On first use, you'll be prompted to log in. Select **Qwen OAuth (Free)** and follow the browser prompts to authenticate. Your credentials are cached locally for future sessions.

> [!note]
> When you first authenticate, a workspace called ".qwen" is automatically created for centralized cost tracking and management.

> [!tip]
> To switch accounts or re-authenticate, use `/auth` within Qwen Code.

## Step 3: Chat with Qwen Code

### Ask Your First Question

Qwen Code will analyze your files and provide a summary. Try these:

```
what does this project do?
```

```
explain the folder structure
```

```
what can Qwen Code do?
```

> [!note]
> Qwen Code reads your files as needed — you don't have to manually add context.

### Make Your First Code Change

Try a simple task:

```
add a hello world function to the main file
```

Qwen Code will:
1. Find the appropriate file
2. Show you the proposed changes
3. Ask for your approval
4. Make the edit

> [!note]
> Qwen Code always asks for permission before modifying files. Use [Approval Modes](./features/approval-mode) to customize this behavior.

### Use Git with Qwen Code

```
what files have I changed?
```

```
commit my changes with a descriptive message
```

```
create a new branch called feature/new-feature
```

```
help me resolve merge conflicts
```

---

## Common Workflows

### Fix a Bug

Describe the issue:

```
there's a bug where users can submit empty forms - fix it
```

Or share an error:

```
I'm seeing an error when I run npm test
```

### Refactor Code

```
refactor the authentication module to use async/await
```

### Write Tests

```
write unit tests for the calculator functions
```

### Update Documentation

```
update the README with installation instructions
```

### Code Review

```
review my changes and suggest improvements
```

> [!tip]
> **Remember**: Qwen Code is your AI pair programmer. Talk to it like you would a helpful colleague.

---

## Use Specialized Sub-Agents

Sub-agents are specialized AI assistants for specific tasks.

### View Available Sub-Agents

```
/agents
```

### Use Sub-Agents

Qwen Code automatically delegates appropriate tasks:

```
review my recent code changes for security issues
```

```
run all tests and fix any failures
```

Explicitly request a specific sub-agent:

```
use the code-reviewer sub-agent to check the auth module
```

### Create Custom Sub-Agents

```
/agents create
```

Follow the prompts to define:
- A unique identifier (e.g., `code-reviewer`, `api-designer`)
- When to use this agent
- Which tools it can access
- A system prompt describing the agent's role

> [!tip]
> Learn more about [Sub-Agents](./features/sub-agents) and [Approval Modes](./features/approval-mode).

---

## Essential Commands

| Command | Description | Example |
|---------|-------------|---------|
| `qwen` | Start Qwen Code | `qwen` |
| `/help` | Show available commands | `/help` |
| `/clear` | Clear screen | `/clear` or `Ctrl+L` |
| `/compress` | Compress chat history | `/compress` |
| `/agents` | Manage sub-agents | `/agents` |
| `/skills` | List and use skills | `/skills` |
| `/mcp` | Manage MCP servers | `/mcp` |
| `/approval-mode` | Change permission mode | `/approval-mode auto-edit` |
| `/theme` | Change theme | `/theme` |
| `/quit` | Exit Qwen Code | `/quit` |

See the [Commands Reference](./features/commands) for a complete list.

---

## Pro Tips for Beginners

### Be Specific

❌ "fix the bug"  
✅ "fix the login bug where users see a blank screen after entering wrong credentials"

### Use Step-by-Step Instructions

```
1. create a new database table for user profiles
2. create an API endpoint to get and update profiles
3. build a webpage to view and edit profiles
```

### Let Qwen Code Explore First

```
analyze the database schema
```

```
build a dashboard showing products most frequently returned by UK customers
```

### Use Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `?` | Show all shortcuts |
| `Tab` | Command completion |
| `↑` | Command history |
| `/` | Show slash commands |
| `Shift+Tab` | Cycle approval modes |

---

## Getting Help

- **In Qwen Code**: Type `/help` or ask "how do I..."
- **Documentation**: Browse other guides in this documentation
- **Community**: Join [GitHub Discussions](https://github.com/QwenLM/qwen-code/discussions) for tips and support

---

## What's Next?

- [Common Workflows](./common-workflow) — Detailed workflow examples
- [Skills](./features/skills) — Create custom AI capabilities
- [Sub-Agents](./features/sub-agents) — Specialized AI assistants
- [MCP](./features/mcp) — Connect external tools and data sources
- [Configuration](./configuration/settings) — Customize Qwen Code

---

*Last updated: March 2, 2026*
