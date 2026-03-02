# Qwen Code Architecture Overview

This document provides a high-level overview of Qwen Code's modular architecture, including the new Skills system, Sub-Agents, and extended tool capabilities.

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         CLI Package (packages/cli)                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐ │
│  │   Input     │  │   Display   │  │   Theme     │  │  Configuration  │ │
│  │  Processing │  │  Rendering  │  │   Engine    │  │   Manager       │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────────┘ │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐ │
│  │   Slash     │  │  Session    │  │  Extension  │  │   Keyboard      │ │
│  │  Commands   │  │  Manager    │  │   Loader    │  │   Shortcuts     │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────────┘ │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                        Core Package (packages/core)                     │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐ │
│  │   Model     │  │   Tool      │  │   State     │  │  Generation     │ │
│  │   Client    │  │  Orchestrator│  │  Manager    │  │   Config        │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────────┘ │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐ │
│  │   Skills    │  │  Sub-Agent  │  │   Memory    │  │   Approval      │ │
│  │   Loader    │  │   Manager   │  │   Manager   │  │   Controller    │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────────┘ │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
          ┌─────────────────────────┼─────────────────────────┐
          ▼                         ▼                         ▼
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────────────┐
│  Built-in Tools  │    │   MCP Servers    │    │    Sub-Agents System     │
│  ┌────────────┐  │    │  ┌────────────┐  │    │  ┌────────────────────┐  │
│  │File System │  │    │  │  External  │  │    │  │ Testing Specialist │  │
│  │   Tools    │  │    │  │   APIs     │  │    │  │ Documentation      │  │
│  ├────────────┤  │    │  ├────────────┤  │    │  │ Writer             │  │
│  │   Shell    │  │    │  │ Databases  │  │    │  │ Code Reviewer      │  │
│  │   Tools    │  │    │  │  Services  │  │    │  │ Tech Specialists   │  │
│  ├────────────┤  │    │  └────────────┘  │    │  └────────────────────┘  │
│  │   Search   │  │    └──────────────────┘    └──────────────────────────┘
│  │   Tools    │  │
│  ├────────────┤  │
│  │    Web     │  │
│  │   Tools    │  │
│  ├────────────┤  │
│  │   Task     │  │
│  │   (Delegation)││
│  └────────────┘  │
└──────────────────┘
```

---

## Core Components

### 1. CLI Package (`packages/cli`)

**Purpose:** User-facing interface that handles input, output, and overall user experience.

#### Key Modules

| Module | Responsibility |
|--------|----------------|
| **Input Processing** | Handles text entry, slash commands (`/help`), at commands (`@file`), exclamation commands (`!cmd`) |
| **Display Rendering** | Formats responses with syntax highlighting, code blocks, and proper terminal formatting |
| **Theme Engine** | Manages visual themes and UI customization |
| **Configuration Manager** | Loads and merges settings from multiple sources |
| **Session Manager** | Maintains conversation history, enables session resumption |
| **Extension Loader** | Discovers and loads installed extensions |
| **Keyboard Shortcuts** | Handles `Ctrl+C`, `Ctrl+L`, `Shift+Tab`, and other shortcuts |

#### Input Types

| Prefix | Type | Handler |
|--------|------|---------|
| `/` | Slash Commands | Command registry → action execution |
| `@` | File Injection | File system → content injection |
| `!` | Shell Commands | Shell executor → output capture |
| (none) | Natural Language | Forward to Core for model processing |

---

### 2. Core Package (`packages/core`)

**Purpose:** Backend orchestration that manages model API communication, tool execution, and state.

#### Key Modules

| Module | Responsibility |
|--------|----------------|
| **Model Client** | API communication with Qwen, Anthropic, OpenAI-compatible providers |
| **Tool Orchestrator** | Registers, discovers, and executes tools based on model requests |
| **State Manager** | Maintains conversation state, token counts, session metadata |
| **Generation Config** | Model parameters, temperature, context window, caching |
| **Skills Loader** | Discovers and loads skills from `~/.qwen/skills/`, `.qwen/skills/`, extensions |
| **Sub-Agent Manager** | Manages sub-agent configurations and delegation |
| **Memory Manager** | Handles persistent context across sessions |
| **Approval Controller** | Enforces permission modes (Plan, Default, Auto-Edit, YOLO) |

---

### 3. Skills System

**Purpose:** Modular capabilities that extend Qwen Code's effectiveness through model-invoked expertise.

#### Skill Discovery

```
Skill Locations (in order of precedence):
1. Extension Skills    → <extension>/skills/
2. Project Skills      → .qwen/skills/
3. Personal Skills     → ~/.qwen/skills/
```

#### Skill Structure

```
my-skill/
├── SKILL.md           # Required: YAML frontmatter + instructions
├── reference.md       # Optional: Detailed documentation
├── examples.md        # Optional: Usage examples
├── scripts/           # Optional: Helper utilities
│   └── helper.py
└── templates/         # Optional: Reusable templates
    └── template.txt
```

#### Skill Loading Flow

```
1. User starts Qwen Code
2. Skills Loader scans discovery locations
3. Parse SKILL.md frontmatter (name, description)
4. Register skill with model context
5. Model autonomously invokes skills when relevant
```

---

### 4. Sub-Agents System

**Purpose:** Specialized AI assistants that handle specific task types with dedicated prompts and tools.

#### Sub-Agent Discovery

```
Agent Locations (in order of precedence):
1. Extension Agents    → <extension>/agents/
2. Project Agents      → .qwen/agents/
3. Personal Agents     → ~/.qwen/agents/
```

#### Agent Structure

```yaml
---
name: agent-name
description: When and how to use this agent
tools:
  - read_file
  - write_file
---

System prompt with ${variable} templating support.
```

#### Delegation Flow

```
1. User request received
2. Main model analyzes task
3. Matches task to sub-agent descriptions
4. Delegates to appropriate sub-agent via Task tool
5. Sub-agent executes with isolated context
6. Results returned to main conversation
```

---

### 5. Built-in Tools

Tools are individual modules that enable model interaction with the local environment.

#### Tool Categories

| Category | Tools |
|----------|-------|
| **File Operations** | `read_file`, `write_file`, `edit_file`, `read_many_files` |
| **Shell Commands** | `run_shell_command` (with approval control) |
| **Search** | `search_files`, `search_content` (ripgrep-powered) |
| **Web** | `web_fetch`, `web_search` (Tavily API) |
| **Task Management** | `todo_write`, `task` (sub-agent delegation) |
| **Memory** | `memory_add`, `memory_retrieve` |
| **Exit Plan** | `exit_plan_mode` |

#### Tool Execution Flow

```
1. Model requests tool execution
2. Approval Controller checks permission mode
3. If approval required → prompt user
4. If approved (or not required) → execute tool
5. Return result to model
6. Model generates response based on result
```

---

### 6. MCP Integration

**Purpose:** Connect to external tools and data sources via Model Context Protocol.

#### MCP Architecture

```
┌─────────────────┐
│  Qwen Code      │
│  Core Package   │
└────────┬────────┘
         │ MCP Client
         ▼
┌─────────────────┐
│  MCP Servers    │
│  ┌───────────┐  │
│  │ Filesystem│  │
│  ├───────────┤  │
│  │ Database  │  │
│  ├───────────┤  │
│  │  GitHub   │  │
│  ├───────────┤  │
│  │   Slack   │  │
│  └───────────┘  │
└─────────────────┘
```

#### Transport Types

| Transport | Use Case |
|-----------|----------|
| **stdio** | Local processes, scripts, Docker |
| **http** | Remote HTTP streaming (recommended) |
| **sse** | Legacy Server-Sent Events |

---

## Interaction Flow

### Standard Request Flow

```
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│   User   │     │   CLI    │     │   Core   │     │   Model  │
│          │     │ Package  │     │ Package  │     │   API    │
└────┬─────┘     └────┬─────┘     └────┬─────┘     └────┬─────┘
     │                │                │                │
     │ 1. Input       │                │                │
     │───────────────>│                │                │
     │                │                │                │
     │                │ 2. Forward     │                │
     │                │ Request        │                │
     │                │───────────────>│                │
     │                │                │                │
     │                │                │ 3. Build Prompt│
     │                │                │ (context +     │
     │                │                │  tools +       │
     │                │                │  history)      │
     │                │                │                │
     │                │                │ 4. API Call    │
     │                │                │───────────────>│
     │                │                │                │
     │                │                │ 5. Response    │
     │                │                │<───────────────│
     │                │                │                │
     │                │                │ [Tool Request?]│
     │                │                │       │        │
     │                │                │       │ Yes    │
     │                │                │       ▼        │
     │                │                │ 6. Execute Tool│
     │                │                │ (with approval)│
     │                │                │       │        │
     │                │                │ 7. Result      │
     │                │                │───────────────>│
     │                │                │                │
     │                │                │ 8. Final       │
     │                │                │ Response       │
     │                │                │<───────────────│
     │                │                │                │
     │                │ 9. Response    │                │
     │                │<───────────────│                │
     │                │                │                │
     │ 10. Display    │                │                │
     │<───────────────│                │                │
     │                │                │                │
```

### Sub-Agent Delegation Flow

```
User Request
     │
     ▼
Main Model analyzes task
     │
     ▼
Matches to sub-agent description
     │
     ▼
Task Tool delegates to sub-agent
     │
     ├───► Sub-Agent receives task
     │     │
     │     ▼
     │     Executes with isolated context
     │     │
     │     ▼
     │     Uses configured tools
     │     │
     │     ▼
     │     Returns results
     │
     ▼
Main Model integrates results
     │
     ▼
Response to user
```

---

## Configuration System

### Configuration Layers (Precedence Order)

| Level | Source | Override Behavior |
|-------|--------|-------------------|
| 1 | Default values | Base layer |
| 2 | System defaults | `/etc/qwen-code/system-defaults.json` |
| 3 | User settings | `~/.qwen/settings.json` |
| 4 | Project settings | `.qwen/settings.json` |
| 5 | System settings | `/etc/qwen-code/settings.json` |
| 6 | Environment variables | Session-specific |
| 7 | Command-line arguments | Highest precedence |

### Configuration Categories

| Category | Settings |
|----------|----------|
| **General** | `vimMode`, `preferredEditor`, `enableAutoUpdate`, `gitCoAuthor` |
| **Output** | `format` (text, json, stream-json) |
| **UI** | `theme`, `hideWindowTitle`, `showLineNumbers`, `customWittyPhrases` |
| **Model** | `name`, `maxSessionTurns`, `generationConfig`, `chatCompression` |
| **Context** | `fileName`, `includeDirectories`, `fileFiltering` |
| **Tools** | `sandbox`, `approvalMode`, `allowed`, `exclude`, `useRipgrep` |
| **MCP** | `serverCommand`, `allowed`, `excluded`, `mcpServers` |
| **Security** | `folderTrust`, `auth.selectedType`, `auth.enforcedType` |
| **Telemetry** | `enabled`, `target`, `otlpEndpoint`, `logPrompts` |

---

## Key Design Principles

| Principle | Description |
|-----------|-------------|
| **Modularity** | CLI and Core separation enables independent development and multiple frontends |
| **Extensibility** | Skills, Sub-Agents, Tools, and MCP allow unlimited capability expansion |
| **User Experience** | Terminal-first design with rich interactivity, themes, and intuitive commands |
| **Security** | Approval modes, sandboxing, and tool restrictions protect user systems |
| **Flexibility** | Multiple configuration methods adapt to different workflows |
| **Open Source** | Apache 2.0 licensed; community contributions welcome |

---

## Extension System

Extensions can provide:

| Extension Component | Description |
|---------------------|-------------|
| **Custom Skills** | Add domain-specific capabilities |
| **Custom Sub-Agents** | Provide specialized AI assistants |
| **Custom Commands** | Add new slash commands |
| **Custom Tools** | Extend tool capabilities |
| **Theme Packs** | Provide visual themes |

### Extension Structure

```
my-extension/
├── qwen-extension.json    # Extension manifest
├── skills/                # Custom skills
├── agents/                # Custom sub-agents
├── commands/              # Custom slash commands
└── themes/                # Custom themes
```

---

## Related Documentation

- [Skills](../users/features/skills) — Create custom AI capabilities
- [Sub-Agents](../users/features/sub-agents) — Specialized AI assistants
- [Tools Reference](./tools/introduction) — Built-in tools documentation
- [Configuration](../users/configuration/settings) — All settings reference
- [Roadmap](./roadmap) — Development plan and future features

---

*Last updated: March 2, 2026*
