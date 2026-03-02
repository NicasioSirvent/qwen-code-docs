# JetBrains IDEs

> JetBrains IDEs provide native support for AI coding assistants through the Agent Client Protocol (ACP). This integration allows you to use Qwen Code directly within your JetBrains IDE.

![Qwen Code in JetBrains AI Chat](https://img.alicdn.com/imgextra/i3/O1CN01ZxYel21y433Ci6eg0_!!6000000006524-2-tps-2774-1494.png)

## Features

| Feature | Description |
|---------|-------------|
| **Native Agent Experience** | Integrated AI assistant panel within your JetBrains IDE |
| **Agent Client Protocol** | Full support for ACP enabling advanced IDE interactions |
| **Symbol Management** | #-mention symbols to add them to the conversation context |
| **Conversation History** | Access to past conversations within the IDE |

## Supported IDEs

- IntelliJ IDEA (Ultimate and Community)
- WebStorm
- PyCharm (Professional and Community)
- GoLand
- PhpStorm
- RubyMine
- CLion
- Rider
- AppCode
- DataGrip

## Requirements

- JetBrains IDE 2024.1 or higher (with ACP support)
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

### Step 2: Open Your JetBrains IDE

Open any JetBrains IDE with ACP support.

### Step 3: Configure ACP Agent

1. Navigate to the **AI Chat** tool window
2. Click the **3-dot menu** in the upper-right corner
3. Select **Configure ACP Agent**
4. Configure Qwen Code with the following settings:

```json
{
  "agent_servers": {
    "qwen": {
      "command": "/path/to/qwen",
      "args": ["--acp"],
      "env": {}
    }
  }
}
```

> [!note]
> Replace `/path/to/qwen` with the actual path to the qwen executable. You can find it by running `which qwen` (macOS/Linux) or `where qwen` (Windows).

### Step 4: Start Using

The Qwen Code agent should now be available in the AI Assistant panel.

## Usage

### Start a Conversation

1. Open the AI Assistant panel in your JetBrains IDE
2. Select "Qwen Code" from the agent dropdown
3. Start chatting with your code context

### Reference Code

Use `#` to mention symbols in your conversation:
```
#MyClass explain this class
```

### Approval Modes

Qwen Code in JetBrains IDEs respects the same approval modes as the CLI:
- **Plan**: Read-only analysis
- **Default**: Manual approval for all changes
- **Auto-Edit**: Auto-approve file edits
- **YOLO**: Full automation

## Platform-Specific Notes

### macOS

The qwen command is typically located at:
```
/usr/local/bin/qwen
```

### Windows

The qwen command is typically located at:
```
C:\Users\<username>\AppData\Roaming\npm\qwen.cmd
```

### Linux

The qwen command is typically located at:
```
/usr/bin/qwen
```

## Troubleshooting

### Agent Not Appearing

- Run `qwen --version` in terminal to verify installation
- Ensure your JetBrains IDE version supports ACP (2024.1+)
- Check that the command path is correct in the configuration
- Restart your JetBrains IDE

### Qwen Code Not Responding

- Check your internet connection
- Verify CLI works by running `qwen` in terminal
- Check authentication: run `qwen /auth` in terminal
- [File an issue on GitHub](https://github.com/QwenLM/qwen-code/issues) if the problem persists

### Configuration Issues

- Ensure the command path is absolute (not relative)
- On Windows, use `.cmd` extension: `qwen.cmd`
- Check that `--acp` flag is included in args
- Verify environment variables are properly formatted

### ACP Not Supported

- Update your JetBrains IDE to version 2024.1 or higher
- Check that the AI Chat plugin is enabled
- Verify ACP is enabled in IDE settings

## Related Documentation

- [Quick Start](./users/quickstart) — Getting started guide
- [Commands](./users/features/commands) — Available commands
- [ACP Integration](./developers/architecture) — Architecture overview

---

*Last updated: March 2, 2026*
