# Model Context Protocol (MCP)

## What is MCP?

**Model Context Protocol (MCP)** is a protocol that allows Qwen Code to connect to external tools and data sources. MCP servers give Qwen Code access to your tools, databases, and APIs.

### What You Can Do with MCP

With MCP servers connected, you can ask Qwen Code to:

| Capability | Examples |
|------------|----------|
| **Work with files and repos** | Read/search/write depending on enabled tools |
| **Query databases** | Schema inspection, queries, reporting |
| **Integrate internal services** | Wrap your APIs as MCP tools |
| **Automate workflows** | Repeatable tasks exposed as tools/prompts |
| **Connect external services** | Google Drive, Figma, Slack, Jira, GitHub |

---

## Quick Start

### Add Your First Server

1. **Add a server** (example: remote HTTP MCP server):
   ```bash
   qwen mcp add --transport http my-server http://localhost:3000/mcp
   ```

2. **Verify it shows up**:
   ```bash
   qwen mcp list
   ```

3. **Restart Qwen Code** in the same project, then ask the model to use tools from that server.

### View Configured Servers

```bash
# List all MCP servers
qwen mcp list

# Show server details
qwen mcp desc <server-name>
```

---

## Configuration

### Where Configuration is Stored (Scopes)

| Scope | Location | Description |
|-------|----------|-------------|
| **Project** (default) | `.qwen/settings.json` | In your project root — shared with team |
| **User** | `~/.qwen/settings.json` | Across all projects on your machine |

**Write to user scope:**
```bash
qwen mcp add --scope user --transport http my-server http://localhost:3000/mcp
```

### Choose a Transport

| Transport | When to Use | JSON Field(s) |
|-----------|-------------|---------------|
| **http** | Recommended for remote services; works well for cloud MCP servers | `httpUrl` (+ optional `headers`) |
| **sse** | Legacy/deprecated servers that only support Server-Sent Events | `url` (+ optional `headers`) |
| **stdio** | Local process (scripts, CLIs, Docker) on your machine | `command`, `args` (+ optional `cwd`, `env`) |

> **Note:** If a server supports both, prefer HTTP over SSE.

---

## Server Configuration Examples

### Stdio Server (Local Process)

Run a local Python MCP server:

**JSON** (`.qwen/settings.json`):
```json
{
  "mcpServers": {
    "pythonTools": {
      "command": "python",
      "args": ["-m", "my_mcp_server", "--port", "8080"],
      "cwd": "./mcp-servers/python",
      "env": {
        "DATABASE_URL": "$DB_CONNECTION_STRING",
        "API_KEY": "${EXTERNAL_API_KEY}"
      },
      "timeout": 15000
    }
  }
}
```

**CLI**:
```bash
qwen mcp add pythonTools \
  -e DATABASE_URL=$DB_CONNECTION_STRING \
  -e API_KEY=$EXTERNAL_API_KEY \
  --timeout 15000 \
  python -m my_mcp_server --port 8080
```

### HTTP Server (Remote Streamable HTTP)

Connect to a remote HTTP MCP server with authentication:

**JSON**:
```json
{
  "mcpServers": {
    "httpServerWithAuth": {
      "httpUrl": "http://localhost:3000/mcp",
      "headers": {
        "Authorization": "Bearer your-api-token"
      },
      "timeout": 5000
    }
  }
}
```

**CLI**:
```bash
qwen mcp add --transport http httpServerWithAuth \
  http://localhost:3000/mcp \
  --header "Authorization: Bearer your-api-token" \
  --timeout 5000
```

### SSE Server (Remote Server-Sent Events)

Connect to a legacy SSE-based MCP server:

**JSON**:
```json
{
  "mcpServers": {
    "sseServer": {
      "url": "http://localhost:8080/sse",
      "timeout": 30000
    }
  }
}
```

**CLI**:
```bash
qwen mcp add --transport sse sseServer \
  http://localhost:8080/sse \
  --timeout 30000
```

### Docker-based MCP Server

Run an MCP server in a Docker container:

**JSON**:
```json
{
  "mcpServers": {
    "dockerServer": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "my-mcp-image:latest"],
      "env": {
        "API_KEY": "${DOCKER_MCP_API_KEY}"
      }
    }
  }
}
```

---

## Safety and Control

### Trust (Skip Confirmations)

By default, Qwen Code asks for confirmation before using MCP tools. To bypass confirmations for trusted servers:

**JSON**:
```json
{
  "mcpServers": {
    "trustedServer": {
      "httpUrl": "http://localhost:3000/mcp",
      "trust": true
    }
  }
}
```

**CLI**:
```bash
qwen mcp add --trust trustedServer http://localhost:3000/mcp
```

> ⚠️ **Warning:** Only use `trust: true` for servers you fully control and trust.

### Tool Filtering (Allow/Deny Tools Per Server)

Restrict which tools an MCP server exposes:

**JSON**:
```json
{
  "mcpServers": {
    "filteredServer": {
      "command": "python",
      "args": ["-m", "my_mcp_server"],
      "includeTools": ["safe_tool", "file_reader", "data_processor"],
      "timeout": 30000
    }
  }
}
```

**CLI**:
```bash
qwen mcp add filteredServer \
  python -m my_mcp_server \
  --include-tools "safe_tool,file_reader,data_processor"
```

| Property | Description |
|----------|-------------|
| `includeTools` | Allowlist — only these tools are exposed |
| `excludeTools` | Denylist — these tools are hidden (takes precedence over includeTools) |

### Global Allow/Deny Lists

Define global rules for all MCP servers:

**JSON**:
```json
{
  "mcp": {
    "allowed": ["my-trusted-server", "internal-tools"],
    "excluded": ["experimental-server", "deprecated-server"]
  }
}
```

---

## Reference

### settings.json Structure

```json
{
  "mcpServers": {
    "serverName": {
      "command": "path/to/server",
      "args": ["--arg1", "value1"],
      "env": {
        "API_KEY": "$MY_API_TOKEN"
      },
      "cwd": "./server-directory",
      "timeout": 30000,
      "trust": false,
      "description": "Human-readable description",
      "includeTools": ["tool1", "tool2"],
      "excludeTools": ["dangerous_tool"]
    }
  }
}
```

### Server Configuration Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `command` | string | — | Path to executable for Stdio transport (required if using stdio) |
| `url` | string | — | SSE endpoint URL (required if using SSE) |
| `httpUrl` | string | — | HTTP streaming endpoint URL (required if using HTTP) |
| `args` | array | `[]` | Command-line arguments for Stdio transport |
| `headers` | object | `{}` | Custom HTTP headers for URL/HTTP transports |
| `env` | object | `{}` | Environment variables (supports `$VAR` or `${VAR}` syntax) |
| `cwd` | string | — | Working directory for Stdio transport |
| `timeout` | number | `600000` | Request timeout in milliseconds (10 min) |
| `trust` | boolean | `false` | Bypasses all tool call confirmations |
| `description` | string | — | Brief description for display |
| `includeTools` | array | — | Allowlist of tool names from this server |
| `excludeTools` | array | — | Denylist of tool names (takes precedence over includeTools) |

---

## CLI Reference: `qwen mcp`

### Adding a Server
```bash
qwen mcp add [options] <name> <commandOrUrl> [args...]
```

| Option | Description | Default |
|--------|-------------|---------|
| `-s, --scope` | Configuration scope (`user` or `project`) | `project` |
| `-t, --transport` | Transport type (`stdio`, `sse`, `http`) | `stdio` |
| `-e, --env` | Set environment variables (can be repeated) | — |
| `-H, --header` | Set HTTP headers for SSE/HTTP (can be repeated) | — |
| `--timeout` | Connection timeout in milliseconds | `600000` |
| `--trust` | Trust the server (skip confirmations) | `false` |
| `--description` | Set server description | — |
| `--include-tools` | Comma-separated tools to include | all |
| `--exclude-tools` | Comma-separated tools to exclude | none |

### Listing Servers
```bash
qwen mcp list
```

### Removing a Server
```bash
qwen mcp remove <server-name>
```

### Viewing Server Details
```bash
qwen mcp desc <server-name>
```

---

## Popular MCP Servers

### Filesystem Server
Access files outside the current project:
```bash
qwen mcp add filesystem npx -y @modelcontextprotocol/server-filesystem /path/to/allowed/files
```

### GitHub Server
Interact with GitHub repositories:
```bash
qwen mcp add --transport http github https://api.github.com \
  --header "Authorization: Bearer $GITHUB_TOKEN"
```

### Database Server
Query PostgreSQL databases:
```bash
qwen mcp add postgres npx -y @modelcontextprotocol/server-postgres \
  -e DATABASE_URL="postgresql://user:pass@localhost:5432/mydb"
```

### Slack Server
Send messages and read channels:
```bash
qwen mcp add slack npx -y @modelcontextprotocol/server-slack \
  -e SLACK_BOT_TOKEN="xoxb-..."
```

### Google Drive Server
Access Google Drive files:
```bash
qwen mcp add gdrive npx -y @modelcontextprotocol/server-gdrive \
  -e GOOGLE_APPLICATION_CREDENTIALS="~/.gcp/credentials.json"
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Server shows "Disconnected" | Verify URL/command is correct; increase `timeout` |
| Stdio server fails to start | Use absolute command path; check `cwd`/`env` |
| Environment variables don't resolve | Ensure they exist where Qwen Code runs (shell vs GUI environments differ) |
| Tools not appearing | Check `includeTools`/`excludeTools` settings; verify server exposes tools |
| Connection timeout | Increase `timeout` value; check network/firewall |
| Authentication fails | Verify headers contain correct tokens; check token expiration |

### Debug Mode

Enable debug logging to diagnose MCP issues:
```bash
qwen --debug
```

Check logs for MCP connection details and error messages.

---

## Best Practices

### 1. Use Project Scope for Team Servers
```bash
qwen mcp add --scope project internal-api http://internal.company.com/mcp
```
This shares the configuration with your team via `.qwen/settings.json`.

### 2. Use User Scope for Personal Servers
```bash
qwen mcp add --scope user personal-tools http://localhost:4000/mcp
```
Keep personal tools separate from project configuration.

### 3. Limit Tool Access
```json
{
  "mcpServers": {
    "readonly-db": {
      "command": "python",
      "args": ["-m", "db_server", "--readonly"],
      "includeTools": ["query", "schema"]
    }
  }
}
```

### 4. Use Environment Variables for Secrets
```json
{
  "mcpServers": {
    "secure-server": {
      "httpUrl": "https://api.company.com/mcp",
      "headers": {
        "Authorization": "Bearer $MCP_API_TOKEN"
      }
    }
  }
}
```

Store actual values in `.qwen/.env` (gitignored).

### 5. Set Appropriate Timeouts
- Local servers: `5000-15000` ms
- Remote servers: `30000-60000` ms
- Slow operations: `120000+` ms

---

## Related Documentation

- [Skills](./skills) — Create custom AI capabilities
- [Sub-Agents](./sub-agents) — Specialized AI assistants
- [Configuration](../configuration/settings) — All settings reference
- [Tools](../../developers/tools/introduction) — Built-in tools

---

*Last updated: March 2, 2026*
