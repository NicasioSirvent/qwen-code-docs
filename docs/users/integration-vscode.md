# Visual Studio Code

> The VS Code extension (Beta) lets you see Qwen's changes in real-time through a native graphical interface integrated directly into your IDE.

<br/>

<video src="https://cloud.video.taobao.com/vod/IKKwfM-kqNI3OJjM_U8uMCSMAoeEcJhs6VNCQmZxUfk.mp4" controls width="800">
  Your browser does not support the video tag.
</video>

## Features

| Feature | Description |
|---------|-------------|
| **Native IDE Experience** | Dedicated Qwen Code sidebar panel accessed via the Qwen icon |
| **Auto-Accept Edits** | Automatically apply Qwen's changes as they're made |
| **File Management** | @-mention files or attach files and images using the system file picker |
| **Conversation History** | Access to past conversations |
| **Multiple Sessions** | Run multiple Qwen Code sessions simultaneously |

## Requirements

- VS Code 1.85.0 or higher
- Node.js 20+ (for CLI)

## Installation

1. Install Qwen Code CLI:
   ```bash
   npm install -g @qwen-code/qwen-code@latest
   ```

2. Download and install the extension from the [Visual Studio Code Extension Marketplace](https://marketplace.visualstudio.com/items?itemName=qwenlm.qwen-code-vscode-ide-companion).

3. Open VS Code and click the Qwen icon in the sidebar to start a session.

## Usage

### Start a Session

1. Click the Qwen icon in the VS Code sidebar
2. Authenticate if prompted (uses same credentials as CLI)
3. Start chatting with Qwen Code

### Auto-Accept Mode

Enable auto-accept mode to automatically apply Qwen's changes:
1. Click the approval mode indicator in the Qwen panel
2. Select "Auto-Edit" for automatic file changes
3. Shell commands will still require approval

### File References

- Click the attachment icon to select files
- Type `@` to mention files in your conversation
- Drag and drop files into the chat panel

## Troubleshooting

### Extension Not Installing

- Ensure you have VS Code 1.85.0 or higher
- Check that VS Code has permission to install extensions
- Try installing directly from the Marketplace website

### Qwen Code Not Responding

- Check your internet connection
- Verify CLI is installed: `qwen --version`
- Start a new conversation to see if the issue persists
- [File an issue on GitHub](https://github.com/QwenLM/qwen-code/issues) if the problem continues

### Authentication Issues

- Use `/auth` in the CLI to verify your credentials
- The extension shares credentials with the CLI

## Related Documentation

- [Quick Start](./users/quickstart) — Getting started guide
- [Commands](./users/features/commands) — Available commands
- [Approval Mode](./users/features/approval-mode) — Control permissions

---

*Last updated: March 2, 2026*
