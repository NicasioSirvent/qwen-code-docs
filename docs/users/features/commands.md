# Commands

Qwen Code supports three command types triggered by specific prefixes. Each type serves a different purpose in your workflow.

## Command Types Overview

| Prefix | Type | Function | Use Case |
|--------|------|----------|----------|
| `/` | **Slash Commands** | Meta-level control | Managing sessions, settings, help |
| `@` | **At Commands** | Inject file content | AI analysis of files/directories |
| `!` | **Exclamation Commands** | Shell execution | System commands like `git status`, `ls` |

---

## 1. Slash Commands (/)

Slash commands provide meta-level control over Qwen Code's behavior, sessions, and configuration.

### Session and Project Management

| Command | Description | Usage |
|---------|-------------|-------|
| `/init` | Analyze current directory and create initial context file | `/init` |
| `/summary` | Generate project summary based on conversation history | `/summary` |
| `/compress` | Replace chat history with summary to save tokens | `/compress` |
| `/resume` | Resume a previous conversation session | `/resume` |
| `/restore` | Restore files to state before tool execution | `/restore` or `/restore <ID>` |

### Interface and Workspace Control

| Command | Description | Usage |
|---------|-------------|-------|
| `/clear` | Clear terminal screen content | `/clear` (shortcut: `Ctrl+L`) |
| `/theme` | Change Qwen Code visual theme | `/theme` |
| `/vim` | Turn input area Vim editing mode on/off | `/vim` |
| `/directory` | Manage multi-directory support workspace | `/dir add ./src,./tests` |
| `/editor` | Open dialog to select supported editor | `/editor` |

### Language Settings

| Command | Description | Usage |
|---------|-------------|-------|
| `/language` | View or change language settings | `/language` |
| `/language ui [language]` | Set UI interface language | `/language ui zh-CN` |
| `/language output [language]` | Set LLM output language | `/language output Chinese` |

**Available UI languages:** zh-CN (Simplified Chinese), en-US (English), ru-RU (Russian), de-DE (German)

### Tool and Model Management

| Command | Description | Usage |
|---------|-------------|-------|
| `/mcp` | List configured MCP servers and tools | `/mcp`, `/mcp desc` |
| `/tools` | Display currently available tool list | `/tools`, `/tools desc` |
| `/skills` | List and run available skills | `/skills`, `/skills <name>` |
| `/agents` | List, create, and manage sub-agents | `/agents`, `/agents create`, `/agents manage` |
| `/approval-mode` | Change approval mode for tool usage | `/approval-mode <mode> --project` |
| `/model` | Switch model used in current session | `/model` |
| `/extensions` | List all active extensions in current session | `/extensions` |
| `/memory` | Manage AI's instruction context | `/memory add Important Info` |

#### Approval Modes

| Mode | Description | Use Case |
|------|-------------|----------|
| `plan` | Analysis only, no execution | Secure review |
| `default` | Require approval for edits | Daily use |
| `auto-edit` | Automatically approve edits | Trusted environment |
| `yolo` | Automatically approve all | Quick prototyping |

### Information, Settings, and Help

| Command | Description | Usage |
|---------|-------------|-------|
| `/help` | Display help information for available commands | `/help` or `/?` |
| `/about` | Display version information | `/about` |
| `/stats` | Display detailed statistics for current session | `/stats` |
| `/settings` | Open settings editor | `/settings` |
| `/auth` | Change authentication method | `/auth` |
| `/bug` | Submit issue about Qwen Code | `/bug` |
| `/copy` | Copy last output content to clipboard | `/copy` |
| `/quit` | Exit Qwen Code immediately | `/quit` or `/exit` |

---

## 2. At Commands (@) — File Injection

At commands inject file or directory content into the conversation for AI analysis.

### Command Formats

| Format | Description | Examples |
|--------|-------------|----------|
| `@<file path>` | Inject content of specified file | `@src/main.py Please explain this code` |
| `@<directory path>` | Recursively read all text files in directory | `@docs/ Summarize content of this directory` |
| `@` (standalone) | Used when discussing @ symbol itself | `@ What is this symbol used for in programming?` |

### Usage Examples

```
@src/auth/login.ts Review this code for security issues
@README.md Update this documentation with new features
@tests/ Add more test cases to these files
@package.json What dependencies are outdated?
```

### Path Handling

**Spaces in paths** need to be escaped with backslash:
```
@My\ Documents/file.txt Explain this document
@src/my\ folder/utils.ts Review these utilities
```

### Best Practices

1. **Be specific with file paths**: `@src/components/Button.tsx` instead of `@src/`
2. **Use for context**: Reference files you want the AI to consider
3. **Combine with requests**: Always include what you want done with the injected content

---

## 3. Exclamation Commands (!) — Shell Execution

Exclamation commands execute shell commands directly in your terminal.

### Command Formats

| Format | Description | Examples |
|--------|-------------|----------|
| `!<shell command>` | Execute command in sub-shell | `!ls -la`, `!git status` |
| `!` (standalone) | Switch to Shell mode (any input executed directly) | `!` → Input command → `!` (exit) |

### Usage Examples

```
!git status
!npm install
!docker ps
!python scripts/process.py
```

### Shell Mode

Enter shell mode for multiple consecutive commands:

```
!
> ls -la
> git status
> npm test
> !  (exit shell mode)
```

### Environment Variables

Commands executed via `!` set `QWEN_CODE=1` environment variable, allowing scripts to detect Qwen Code context.

### Security Notes

- Shell commands follow your terminal user's permissions
- In Default and Plan modes, commands may require approval
- YOLO mode auto-approves all commands (use with caution)

---

## Keyboard Shortcuts

| Shortcut | Function | Note |
|----------|----------|-------|
| `Ctrl/Cmd+L` | Clear screen | Equivalent to `/clear` |
| `Ctrl/Cmd+T` | Toggle tool description | MCP tool management |
| `Ctrl/Cmd+C` (×2) | Exit confirmation | Secure exit mechanism |
| `Ctrl/Cmd+Z` | Undo input | Text editing |
| `Ctrl/Cmd+Shift+Z` | Redo input | Text editing |
| `Shift+Tab` | Cycle approval modes | Default → Auto-Edit → YOLO → Plan |

---

## Custom Commands

Create your own slash commands using Markdown files.

### Location & Naming

| Location | Generated Command | Priority | Use Case |
|----------|-------------------|----------|----------|
| `~/.qwen/commands/` | `/test` | Low | Personal commands (all projects) |
| `<project>/.qwen/commands/` | `/git:commit` | High | Project-specific commands |

**Priority Rule:** Project commands override user commands when names conflict.

### Command Naming Rules

| File Location | Generated Command | Example Call |
|---------------|-------------------|--------------|
| `~/.qwen/commands/test.md` | `/test` | `/test Parameter` |
| `<project>/.qwen/commands/git/commit.md` | `/git:commit` | `/git:commit Message` |

**Rule:** Path separators (`/` or `\`) are converted to colons (`:`)

### Markdown File Format

```markdown
---
description: Optional description (displayed in /help)
---

Your prompt content here.
Use {{args}} for parameter injection.
```

### Parameter Processing Mechanisms

| Method | Syntax | Purpose |
|--------|--------|---------|
| Context-aware Injection | `{{args}}` | Precise parameter control with automatic shell escaping |
| Default Parameter Processing | (none) | Simple commands, parameters appended as-is |
| Shell Command Execution | `!{command}` | Dynamic content with execution confirmation |
| File Content Injection | `@{file path}` | Static reference file injection |

### Example: Git Commit Message Command

**File:** `.qwen/commands/git/commit.md`

```markdown
---
description: Generate commit message based on staged changes
---

Please generate a commit message based on the following diff:

```diff
!{git diff --staged}
```

The commit message should:
1. Start with a concise summary line (50 chars max)
2. Include detailed explanation if needed
3. Reference any related issues
```

### Example: Code Review Command

**File:** `.qwen/commands/review.md`

```markdown
---
description: Code review based on best practices
---

Review {{args}} using these standards:

@{docs/code-standards.md}

Focus on:
1. Security vulnerabilities
2. Performance issues
3. Code style consistency
4. Test coverage
```

### Custom Command Best Practices

| Practice | Recommended Approach | Avoid |
|----------|---------------------|-------|
| **Command Naming** | Use namespaces for organization | Overly generic names |
| **Parameter Processing** | Clearly use `{{args}}` | Relying on default appending |
| **Error Handling** | Utilize shell error output | Ignoring execution failure |
| **File Organization** | Organize by function in directories | All commands in root directory |
| **Description Field** | Always provide clear description | Relying on auto-generated description |

### Security Features

| Mechanism | Protection | User Operation |
|-----------|------------|----------------|
| Shell Escaping | Prevent command injection | Automatic |
| Execution Confirmation | Avoid accidental execution | Dialog confirmation |
| Error Reporting | Help diagnose issues | View error information |

---

## Command Reference Quick Lookup

### Most Used Commands

```
/help          - Show all available commands
/clear         - Clear the screen (Ctrl+L)
/compress      - Compress conversation history
/agents        - Manage sub-agents
/skills        - List and use skills
/mcp           - Manage MCP servers
/approval-mode - Change permission mode
/stats         - Show session statistics
/quit          - Exit Qwen Code
```

### File Operations

```
@<file>        - Inject file content
@<directory>   - Inject directory content
/restore       - Restore files to previous state
```

### Shell Operations

```
!<command>     - Run shell command
!              - Enter shell mode
```

### Agent & Skills

```
/agents create - Create new sub-agent
/agents manage - Manage existing agents
/skills        - List available skills
/skills <name> - Use specific skill
```

---

## Troubleshooting

### Command Not Recognized

1. **Check spelling**: Ensure command is spelled correctly
2. **Verify location**: Custom commands must be in `.qwen/commands/` or `~/.qwen/commands/`
3. **Check YAML frontmatter**: Ensure `---` delimiters are correct

### File Injection Not Working

1. **Check path**: Verify file path is correct
2. **Escape spaces**: Use backslash for paths with spaces
3. **File permissions**: Ensure file is readable

### Shell Commands Failing

1. **Check approval mode**: Some modes require command approval
2. **Verify command**: Test command directly in terminal
3. **Environment**: Some commands may need specific environment setup

---

## Related Documentation

- [Skills](./skills) — Create custom AI capabilities
- [Sub-Agents](./sub-agents) — Specialized AI assistants
- [Approval Mode](./approval-mode) — Control permissions
- [Configuration](../configuration/settings) — All settings reference

---

*Last updated: March 2, 2026*
