# Configuration & Settings

Qwen Code offers multiple configuration methods to customize behavior for your workflow.

---

## Configuration Overview

### Configuration Methods

| Method | Use Case | Precedence |
|--------|----------|------------|
| **Settings Files** | Persistent configuration | Low |
| **Environment Variables** | Session-specific or sensitive values | Medium |
| **Command-Line Arguments** | Per-session overrides | High |
| **Context Files** | Instructional context (QWEN.md) | N/A |

---

## Configuration Layers & Precedence

Configuration is applied in the following order (lower numbers are overridden by higher numbers):

| Level | Source | Description |
|-------|--------|-------------|
| 1 | Default values | Hardcoded defaults within the application |
| 2 | System defaults file | System-wide defaults |
| 3 | User settings file | `~/.qwen/settings.json` — Global settings |
| 4 | Project settings file | `.qwen/settings.json` — Project-specific |
| 5 | System settings file | System-wide settings for all users |
| 6 | Environment variables | Session-specific overrides |
| 7 | Command-line arguments | Per-session overrides |

---

## Settings Files

### File Locations

| Type | Location | Scope |
|------|----------|-------|
| **System defaults** | Linux: `/etc/qwen-code/system-defaults.json`<br>Windows: `C:\ProgramData\qwen-code\system-defaults.json`<br>macOS: `/Library/Application Support/QwenCode/system-defaults.json` | Base layer |
| **User settings** | `~/.qwen/settings.json` | All sessions for current user |
| **Project settings** | `.qwen/settings.json` | Only when running from that project |
| **System settings** | Linux: `/etc/qwen-code/settings.json`<br>Windows: `C:\ProgramData\qwen-code\settings.json`<br>macOS: `/Library/Application Support/QwenCode/settings.json` | All users on system |

### Environment Variable Paths

Override default paths with environment variables:
```bash
export QWEN_CODE_SYSTEM_DEFAULTS_PATH="/custom/path/system-defaults.json"
export QWEN_CODE_SYSTEM_SETTINGS_PATH="/custom/path/settings.json"
```

### Environment Variables in Settings

String values in `settings.json` can reference environment variables:
```json
{
  "apiKey": "$MY_API_TOKEN",
  "databaseUrl": "${DATABASE_URL}"
}
```

Both `$VAR_NAME` and `${VAR_NAME}` syntax are supported.

---

## All Available Settings

### General Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `general.preferredEditor` | string | Preferred editor to open files | `undefined` |
| `general.vimMode` | boolean | Enable Vim keybindings | `false` |
| `general.enableAutoUpdate` | boolean | Enable automatic update checks | `true` |
| `general.gitCoAuthor` | boolean | Add Co-authored-by to git commits | `true` |
| `general.checkpointing.enabled` | boolean | Enable session checkpointing | `false` |
| `general.defaultFileEncoding` | string | Default encoding for new files | `"utf-8"` |

### Output Settings

| Setting | Type | Description | Default | Values |
|---------|------|-------------|---------|--------|
| `output.format` | string | Format of CLI output | `"text"` | `text`, `json`, `stream-json` |

### UI Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `ui.theme` | string | Color theme for UI | `undefined` |
| `ui.customThemes` | object | Custom theme definitions | `{}` |
| `ui.hideWindowTitle` | boolean | Hide window title bar | `false` |
| `ui.hideTips` | boolean | Hide helpful tips | `false` |
| `ui.hideBanner` | boolean | Hide application banner | `false` |
| `ui.hideFooter` | boolean | Hide footer | `false` |
| `ui.showMemoryUsage` | boolean | Display memory usage | `false` |
| `ui.showLineNumbers` | boolean | Show line numbers in code blocks | `true` |
| `ui.showCitations` | boolean | Show citations for generated text | `true` |
| `ui.enableWelcomeBack` | boolean | Show welcome back dialog | `true` |
| `ui.accessibility.enableLoadingPhrases` | boolean | Enable loading phrases | `true` |
| `ui.accessibility.screenReader` | boolean | Enable screen reader mode | `false` |
| `ui.customWittyPhrases` | array | Custom loading phrases | `[]` |

### IDE Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `ide.enabled` | boolean | Enable IDE integration mode | `false` |
| `ide.hasSeenNudge` | boolean | Whether user has seen IDE nudge | `false` |

### Privacy Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `privacy.usageStatisticsEnabled` | boolean | Enable usage statistics collection | `true` |

### Model Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `model.name` | string | The model to use | `undefined` |
| `model.maxSessionTurns` | number | Max user/model/tool turns (-1 = unlimited) | `-1` |
| `model.summarizeToolOutput` | object | Summarization with token budget | `undefined` |
| `model.generationConfig` | object | Advanced generation overrides | `undefined` |
| `model.chatCompression.contextPercentageThreshold` | number | Threshold for history compression (0-1) | `0.7` |
| `model.skipNextSpeakerCheck` | boolean | Skip next speaker check | `false` |
| `model.skipLoopDetection` | boolean | Disable loop detection | `false` |
| `model.skipStartupContext` | boolean | Skip startup workspace context | `false` |
| `model.enableOpenAILogging` | boolean | Enable OpenAI API call logging | `false` |
| `model.openAILoggingDir` | string | Custom directory for OpenAI logs | `undefined` |

#### Generation Config Example

```json
{
  "model": {
    "generationConfig": {
      "timeout": 60000,
      "contextWindowSize": 128000,
      "enableCacheControl": true,
      "extra_body": {
        "enable_thinking": true
      },
      "samplingParams": {
        "temperature": 0.2,
        "top_p": 0.8,
        "max_tokens": 1024
      }
    }
  }
}
```

### Context Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `context.fileName` | string/array | Name of context file(s) | `undefined` |
| `context.importFormat` | string | Format for importing memory | `undefined` |
| `context.includeDirectories` | array | Additional directories to include | `[]` |
| `context.loadFromIncludeDirectories` | boolean | Load QWEN.md from included dirs | `false` |
| `context.fileFiltering.respectGitIgnore` | boolean | Respect .gitignore files | `true` |
| `context.fileFiltering.respectQwenIgnore` | boolean | Respect .qwenignore files | `true` |
| `context.fileFiltering.enableRecursiveFileSearch` | boolean | Enable recursive file search | `true` |
| `context.fileFiltering.enableFuzzySearch` | boolean | Enable fuzzy search | `true` |

### Tools Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `tools.sandbox` | boolean/string | Sandbox execution environment | `undefined` |
| `tools.shell.enableInteractiveShell` | boolean | Use node-pty for interactive shell | `false` |
| `tools.core` | array | Allowlist of built-in tools | `undefined` |
| `tools.exclude` | array | Tool names to exclude | `undefined` |
| `tools.allowed` | array | Tools that bypass confirmation | `undefined` |
| `tools.approvalMode` | string | Default approval mode | `default` |
| `tools.discoveryCommand` | string | Command for tool discovery | `undefined` |
| `tools.callCommand` | string | Custom shell command for tools | `undefined` |
| `tools.useRipgrep` | boolean | Use ripgrep for content search | `true` |
| `tools.useBuiltinRipgrep` | boolean | Use bundled ripgrep binary | `true` |
| `tools.enableToolOutputTruncation` | boolean | Enable output truncation | `true` |
| `tools.truncateToolOutputThreshold` | number | Truncate output > N characters | `25000` |
| `tools.truncateToolOutputLines` | number | Maximum lines when truncating | `1000` |

#### Approval Mode Values

| Value | Description |
|-------|-------------|
| `plan` | Read-only analysis, no execution |
| `default` | Manual approval for all changes |
| `auto-edit` | Auto-approve file edits, manual for commands |
| `yolo` | Auto-approve all tool calls |

### MCP Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `mcp.serverCommand` | string | Command to start MCP server | `undefined` |
| `mcp.allowed` | array | Allowlist of MCP servers | `undefined` |
| `mcp.excluded` | array | Denylist of MCP servers | `undefined` |

### Security Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `security.folderTrust.enabled` | boolean | Track folder trust status | `false` |
| `security.auth.selectedType` | string | Currently selected auth type | `undefined` |
| `security.auth.enforcedType` | string | Required auth type (enterprise) | `undefined` |
| `security.auth.useExternal` | boolean | Use external auth flow | `undefined` |

### Advanced Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `advanced.autoConfigureMemory` | boolean | Auto-configure Node.js memory | `false` |
| `advanced.dnsResolutionOrder` | string | DNS resolution order | `undefined` |
| `advanced.excludedEnvVars` | array | Env vars to exclude from context | `["DEBUG","DEBUG_MODE"]` |
| `advanced.bugCommand` | object | Configuration for /bug command | `undefined` |
| `advanced.tavilyApiKey` | string | API key for Tavily web search | `undefined` |

### MCP Servers Configuration

Configure MCP server connections:

| Property | Type | Description | Required |
|----------|------|-------------|----------|
| `command` | string | Command to execute (stdio) | Yes* |
| `args` | array | Arguments for command | No |
| `env` | object | Environment variables | No |
| `cwd` | string | Working directory | No |
| `url` | string | SSE endpoint URL | Yes* |
| `httpUrl` | string | HTTP streaming URL | Yes* |
| `headers` | object | HTTP headers | No |
| `timeout` | number | Timeout in milliseconds | No |
| `trust` | boolean | Bypass tool confirmations | No |
| `description` | string | Brief description | No |
| `includeTools` | array | Allowlist of tools | No |
| `excludeTools` | array | Denylist of tools | No |

*At least one of `command`, `url`, or `httpUrl` must be provided.

### Telemetry Settings

| Setting | Type | Description | Default |
|---------|------|-------------|---------|
| `telemetry.enabled` | boolean | Whether telemetry is enabled | — |
| `telemetry.target` | string | Destination (`local`, `gcp`) | — |
| `telemetry.otlpEndpoint` | string | OTLP exporter endpoint | — |
| `telemetry.otlpProtocol` | string | OTLP protocol (`grpc`, `http`) | — |
| `telemetry.logPrompts` | boolean | Include prompts in logs | — |
| `telemetry.outfile` | string | File for local target | — |
| `telemetry.useCollector` | boolean | Use external OTLP collector | — |

---

## Environment Variables

| Variable | Description | Notes |
|----------|-------------|-------|
| `QWEN_API_KEY` | API key for authentication | Overrides settings file |
| `GEMINI_TELEMETRY_ENABLED` | Enable telemetry | `true`/`1` enables |
| `GEMINI_TELEMETRY_TARGET` | Set telemetry target | `local`, `gcp` |
| `GEMINI_TELEMETRY_OTLP_ENDPOINT` | Set OTLP endpoint | URL |
| `GEMINI_TELEMETRY_OTLP_PROTOCOL` | Set OTLP protocol | `grpc`, `http` |
| `GEMINI_TELEMETRY_LOG_PROMPTS` | Enable prompt logging | `true`/`1` enables |
| `GEMINI_TELEMETRY_OUTFILE` | Set telemetry output file | Path |
| `GEMINI_SANDBOX` | Enable sandbox mode | `true`, `false`, `docker`, `podman` |
| `SEATBELT_PROFILE` | macOS sandbox profile | `permissive-open`, `strict`, custom |
| `DEBUG` / `DEBUG_MODE` | Enable debug logging | Auto-excluded from context |
| `NO_COLOR` | Disable color output | Any value disables |
| `CLI_TITLE` | Customize CLI title | String |
| `CODE_ASSIST_ENDPOINT` | Code assist server endpoint | Development/testing |
| `TAVILY_API_KEY` | Tavily API key | For web_search tool |

---

## Command-Line Arguments

| Argument | Alias | Description | Values |
|----------|-------|-------------|--------|
| `--model` | `-m` | Specify model for session | Model name |
| `--prompt` | `-p` | Pass prompt (non-interactive) | Prompt text |
| `--prompt-interactive` | `-i` | Interactive with initial prompt | Prompt text |
| `--output-format` | `-o` | Output format | `text`, `json`, `stream-json` |
| `--sandbox` | `-s` | Enable sandbox mode | — |
| `--sandbox-image` | — | Set sandbox image URI | URI |
| `--debug` | `-d` | Enable debug mode | — |
| `--all-files` | `-a` | Include all files recursively | — |
| `--help` | `-h` | Display help | — |
| `--show-memory-usage` | — | Display memory usage | — |
| `--yolo` | — | Auto-approve all tool calls | — |
| `--approval-mode` | — | Set approval mode | `plan`, `default`, `auto-edit`, `yolo` |
| `--allowed-tools` | — | Tools bypassing confirmation | Comma-separated |
| `--telemetry` | — | Enable telemetry | — |
| `--checkpointing` | — | Enable checkpointing | — |
| `--extensions` | `-e` | Specify extensions | Extension names |
| `--list-extensions` | `-l` | List available extensions | — |
| `--proxy` | — | Set proxy URL | Proxy URL |
| `--include-directories` | — | Include additional directories | Paths |
| `--screen-reader` | — | Enable screen reader mode | — |
| `--version` | — | Display version | — |
| `--openai-logging` | — | Enable OpenAI API logging | — |
| `--openai-logging-dir` | — | Set OpenAI logs directory | Path |
| `--tavily-api-key` | — | Set Tavily API key | API key |

---

## Context Files (QWEN.md)

### Purpose

Context files provide project-specific instructions, coding style guides, and relevant background information to the AI.

### Hierarchical Loading Order

1. **Global Context**: `~/.qwen/<context-filename>` — Default for all projects
2. **Project Root & Ancestors**: Current directory and parent directories up to `.git` or home

### Commands

| Command | Description |
|---------|-------------|
| `/memory refresh` | Force re-scan and reload of all context files |
| `/memory show` | Display combined instructional context |

### Example Context File

```markdown
# Project: My Awesome TypeScript Library

## General Instructions
- When generating TypeScript code, follow existing coding style
- Ensure all new functions have JSDoc comments
- Prefer functional programming paradigms
- Compatible with TypeScript 5.0+ and Node.js 20+

## Coding Style
- Use 2 spaces for indentation
- Interface names prefixed with `I` (e.g., `IUserService`)
- Private members prefixed with `_`
- Always use strict equality (`===` and `!==`)

## Specific Component: src/api/client.ts
- Handles all outbound API requests
- Include robust error handling and logging
- Use existing `fetchWithRetry` utility for GET requests

## Dependencies
- Avoid new external dependencies unless necessary
- State reason if new dependency is required
```

---

## Example Configuration

### Complete settings.json

```json
{
  "general": {
    "vimMode": true,
    "preferredEditor": "code"
  },
  "ui": {
    "theme": "GitHub",
    "hideTips": false,
    "customWittyPhrases": [
      "You forget a thousand things every day",
      "Connecting to AGI"
    ]
  },
  "tools": {
    "approvalMode": "auto-edit",
    "sandbox": "docker",
    "exclude": ["write_file"]
  },
  "mcpServers": {
    "mainServer": {
      "httpUrl": "http://localhost:3000/mcp",
      "headers": {
        "Authorization": "Bearer ${MCP_TOKEN}"
      }
    }
  },
  "model": {
    "name": "qwen3-coder-plus",
    "maxSessionTurns": 10,
    "generationConfig": {
      "temperature": 0.2,
      "max_tokens": 2048
    }
  },
  "context": {
    "fileName": ["QWEN.md", "CONTEXT.md"],
    "includeDirectories": ["./src", "./docs"]
  },
  "privacy": {
    "usageStatisticsEnabled": true
  }
}
```

---

## Best Practices

### 1. Configuration Organization

| Scope | Use For |
|-------|---------|
| **Project settings** | Project-specific configurations |
| **User settings** | Personal preferences across projects |
| **Environment variables** | Sensitive data (API keys, tokens) |
| **Command-line arguments** | One-off session overrides |

### 2. Security

- Enable **sandbox mode** for untrusted code execution
- Use appropriate **approval modes**:
  - `plan` — Analysis only
  - `default` — Manual approval (recommended)
  - `auto-edit` — Auto-approve file edits
  - `yolo` — Full automation (use with caution)
- Store API keys in `.qwen/.env` (never commit to version control)

### 3. Performance Optimization

For large projects:
```json
{
  "context": {
    "fileFiltering": {
      "enableFuzzySearch": false,
      "enableRecursiveFileSearch": false
    }
  }
}
```

Create `.qwenignore` to exclude directories:
```
node_modules/
dist/
build/
*.log
```

### 4. Context Management

- Create comprehensive `QWEN.md` at project root
- Use global `~/.qwen/QWEN.md` for personal preferences
- Run `/memory refresh` after updating context files
- Use `/memory show` to verify loaded context

### 5. Telemetry & Privacy

Opt out of usage statistics:
```json
{
  "privacy": {
    "usageStatisticsEnabled": false
  }
}
```

Use `NO_COLOR` for CI/CD:
```bash
export NO_COLOR=1
```

---

## Troubleshooting

### Settings Not Applied

1. **Check precedence**: Command-line > env vars > project > user > defaults
2. **Verify JSON syntax**: Use a JSON validator
3. **Restart session**: Some changes require new session

### Environment Variables Not Resolving

1. **Check variable exists**: `echo $MY_VAR`
2. **Verify syntax**: Use `$VAR` or `${VAR}` in settings
3. **Shell context**: Ensure variable is set in shell running Qwen Code

### Memory Issues

For large projects:
```bash
export NODE_OPTIONS="--max-old-space-size=4096"
qwen
```

Or in settings:
```json
{
  "advanced": {
    "autoConfigureMemory": true
  }
}
```

---

## Related Documentation

- [Authentication](./auth) — OAuth and API key setup
- [Approval Mode](../users/features/approval-mode) — Permission control
- [MCP](../users/features/mcp) — External tool integration
- [Architecture](../developers/architecture) — System design overview

---

*Last updated: March 2, 2026*
