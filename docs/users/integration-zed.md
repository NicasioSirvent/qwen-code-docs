# Zed Editor

> Zed Editor provides native support for AI coding assistants through the Agent Client Protocol (ACP). This integration allows you to use Qwen Code directly within Zed's interface.

![Zed Editor Overview](https://img.alicdn.com/imgextra/i1/O1CN01aAhU311GwEoNh27FP_!!6000000000686-2-tps-3024-1898.png)

## Features

| Feature | Description |
|---------|-------------|
| **Native Agent Experience** | Integrated AI assistant panel within Zed's interface |
| **Agent Client Protocol** | Full support for ACP enabling advanced IDE interactions |
| **File Management** | @-mention files to add them to the conversation context |
| **Conversation History** | Access to past conversations within Zed |

## Requirements

- Zed Editor (latest version recommended)
- Qwen Code CLI installed (`npm install -g @qwen-code/qwen-code@latest`)

## Installation

### Step 1: Install Qwen Code CLI

```bash
npm install -g @qwen-code/qwen-code@latest
```

Verify installation:
```bash
qwen --version
```

### Step 2: Download and Install Zed Editor

Download from [Zed.dev](https://zed.dev/)

### Step 3: Configure Qwen Code in Zed

1. Open Zed Editor
2. Click the **settings button** in the top right corner
3. Select **"Add agent"**
4. Choose **"Create a custom agent"**
5. Add the following configuration:

```json
{
  "Qwen Code": {
    "type": "custom",
    "command": "qwen",
    "args": ["--acp"],
    "env": {}
  }
}
```

![Qwen Code Integration](https://img.alicdn.com/imgextra/i1/O1CN013s61L91dSE1J7MTgO_!!6000000003734-2-tps-2592-1234.png)

### Step 4: Start Using

The Qwen Code agent should now be available in the AI Assistant panel.

## Usage

### Start a Conversation

1. Open the AI Assistant panel in Zed
2. Select "Qwen Code" from the agent dropdown
3. Start chatting with your code context

### Reference Files

Use `@` to mention files in your conversation:
```
@src/main.rs explain this function
```

### Approval Modes

Qwen Code in Zed respects the same approval modes as the CLI:
- **Plan**: Read-only analysis
- **Default**: Manual approval for all changes
- **Auto-Edit**: Auto-approve file edits
- **YOLO**: Full automation

## Troubleshooting

### Agent Not Appearing

- Run `qwen --version` in terminal to verify installation
- Check that the JSON configuration is valid (use a JSON validator)
- Restart Zed Editor
- Ensure Zed has terminal permissions

### Qwen Code Not Responding

- Check your internet connection
- Verify CLI works by running `qwen` in terminal
- Check authentication: run `qwen /auth` in terminal
- [File an issue on GitHub](https://github.com/QwenLM/qwen-code/issues) if the problem persists

### Configuration Issues

- Ensure the command path is correct (may need full path: `/usr/local/bin/qwen`)
- Check that `--acp` flag is included in args
- Verify environment variables are properly formatted

## Related Documentation

- [Quick Start](./users/quickstart) — Getting started guide
- [Commands](./users/features/commands) — Available commands
- [ACP Integration](./developers/architecture) — Architecture overview

---

*Last updated: March 2, 2026*
