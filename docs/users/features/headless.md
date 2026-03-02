# Headless Mode

## Overview

**Headless Mode** enables non-interactive, scriptable usage of Qwen Code. It's designed for automation, CI/CD pipelines, and batch processing where terminal interaction is not required.

---

## Quick Start

### Basic Usage

Run a single prompt and exit:
```bash
qwen --prompt "What does this project do?"
```

Shorthand:
```bash
qwen -p "Explain the main architecture"
```

### With Output Format

Get structured JSON output:
```bash
qwen -p "List all API endpoints" --output-format json
```

---

## Command-Line Options

### Core Options

| Option | Alias | Description | Example |
|--------|-------|-------------|---------|
| `--prompt` | `-p` | Run a single prompt and exit | `qwen -p "analyze this"` |
| `--prompt-interactive` | `-i` | Start interactive session with initial prompt | `qwen -i "fix bugs"` |
| `--output-format` | `-o` | Output format | `text`, `json`, `stream-json` |
| `--input-format` | — | Input format | `text`, `stream-json` |
| `--model` | `-m` | Specify model for session | `qwen -m qwen3-coder-plus` |
| `--approval-mode` | — | Set approval mode | `plan`, `default`, `auto-edit`, `yolo` |
| `--yolo` | — | Auto-approve all tool calls | `qwen --yolo -p "fix tests"` |

### Advanced Options

| Option | Description |
|--------|-------------|
| `--sandbox` | Enable sandbox mode for command execution |
| `--sandbox-image` | Set sandbox container image URI |
| `--debug` | Enable verbose debug logging |
| `--all-files` | Include all files recursively in context |
| `--include-directories` | Include additional directories in context |
| `--extensions` | Specify extensions to load |
| `--telemetry` | Enable telemetry collection |

---

## Output Formats

### Text Format (Default)

Human-readable text output:
```bash
qwen -p "What testing framework does this project use?"
```

Output:
```
This project uses Jest as its testing framework. I can see this from:

1. package.json lists "jest": "^29.0.0" as a devDependency
2. jest.config.js configuration file in the root
3. Test files follow the *.test.ts naming convention
```

### JSON Format

Structured JSON output for programmatic processing:
```bash
qwen -p "List all dependencies" -o json
```

Output:
```json
{
  "type": "final_response",
  "content": "This project has the following dependencies:\n\n**Production:**\n- express: ^4.18.0\n- lodash: ^4.17.21\n\n**Development:**\n- jest: ^29.0.0\n- typescript: ^5.0.0",
  "model": "qwen3-coder-plus",
  "turns": 1
}
```

### Stream JSON Format

Real-time streaming output for live processing:
```bash
qwen -p "Generate a report" -o stream-json --include-partial-messages
```

Useful for:
- Building custom UIs
- Real-time logging
- Progress tracking

---

## Use Cases

### 1. CI/CD Automation

**GitHub Actions Example:**
```yaml
name: Code Review
on: [pull_request]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Install Qwen Code
        run: npm install -g @qwen-code/qwen-code
      
      - name: Run Code Review
        env:
          QWEN_API_KEY: ${{ secrets.QWEN_API_KEY }}
        run: |
          qwen -p "Review this PR for security issues and best practices" \
            --approval-mode yolo \
            -o json > review-output.json
      
      - name: Upload Review Results
        uses: actions/upload-artifact@v4
        with:
          name: code-review
          path: review-output.json
```

### 2. Automated Testing

Run tests and auto-fix failures:
```bash
#!/bin/bash

# Run tests and fix failures
qwen --yolo -p "
  Run the test suite. If any tests fail, analyze the failures 
  and fix the issues. Continue until all tests pass.
" --output-format json > test-results.json
```

### 3. Batch Processing

Process multiple files or projects:
```bash
#!/bin/bash

for project in projects/*/; do
  echo "Processing $project..."
  cd "$project"
  
  qwen -p "Generate documentation for this project" \
    --approval-mode plan \
    -o json > docs-output.json
  
  cd ..
done
```

### 4. Log Analysis

Pipe logs to Qwen Code for analysis:
```bash
# Analyze application logs
tail -f app.log | qwen -p "
  Monitor this log stream. Alert me if you see any errors, 
  exceptions, or unusual patterns.
"
```

### 5. Code Generation Pipeline

```bash
#!/bin/bash

# Generate code from specifications
qwen -p "
  Read specs/api-spec.yaml and generate:
  1. TypeScript interfaces
  2. API route handlers
  3. Unit test stubs
  
  Save all files in the appropriate directories.
" --approval-mode auto-edit
```

---

## Integration Examples

### Shell Script Integration

```bash
#!/bin/bash

# Daily code health check
echo "Running daily code health check..."

# Check for code smells
qwen -p "Analyze this codebase for code smells and technical debt" \
  --approval-mode plan \
  -o json > health-report.json

# Extract summary
jq '.content' health-report.json

# Notify team (example with curl)
curl -X POST "$SLACK_WEBHOOK" \
  -H "Content-Type: application/json" \
  -d "{\"text\": \"Daily health check: $(cat health-report.json)\"}"
```

### Makefile Integration

```makefile
.PHONY: review docs test

review:
	qwen -p "Review all changed files for best practices" \
		--approval-mode plan \
		-o json > review.json

docs:
	qwen -p "Generate API documentation from source code" \
		--approval-mode auto-edit

test:
	qwen -p "Run tests and fix any failures" \
		--yolo \
		-o json > test-results.json
```

### Node.js Script Integration

```javascript
const { execSync } = require('child_process');
const fs = require('fs');

function runQwenCode(prompt, options = {}) {
  const args = [
    '-p', `"${prompt}"`,
    '--output-format', 'json',
    options.approvalMode ? `--approval-mode ${options.approvalMode}` : '',
    options.yolo ? '--yolo' : ''
  ].filter(Boolean).join(' ');
  
  const output = execSync(`qwen ${args}`, {
    encoding: 'utf-8',
    cwd: options.cwd || process.cwd()
  });
  
  return JSON.parse(output);
}

// Usage
const result = runQwenCode('Generate unit tests for src/auth.ts', {
  approvalMode: 'auto-edit',
  cwd: '/path/to/project'
});

console.log(result.content);
```

---

## Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `QWEN_API_KEY` | API key for authentication | `export QWEN_API_KEY="sk-..."` |
| `QWEN_CODE` | Set to `1` when running in Qwen Code context | Auto-set for `!` commands |
| `DEBUG` | Enable debug logging | `export DEBUG=true` |
| `NO_COLOR` | Disable colored output | `export NO_COLOR=1` |

---

## Exit Codes

| Code | Description |
|------|-------------|
| `0` | Success |
| `1` | General error |
| `2` | Invalid arguments |
| `3` | Authentication failed |
| `4` | Network error |
| `5` | Tool execution failed |

---

## Best Practices

### 1. Use Appropriate Approval Modes

| Scenario | Recommended Mode |
|----------|-----------------|
| Analysis only | `plan` |
| CI/CD (trusted) | `yolo` |
| Code generation | `auto-edit` |
| Review workflows | `default` |

### 2. Handle Output Programmatically

```bash
# Parse JSON output
qwen -p "List all TODO comments" -o json | jq '.content'

# Check for errors
if qwen -p "fix bugs" --yolo; then
  echo "Success!"
else
  echo "Failed with exit code: $?"
fi
```

### 3. Set Timeouts for Long Operations

```bash
# Timeout after 10 minutes
timeout 600 qwen -p "Refactor the entire codebase" --yolo
```

### 4. Use Sandboxing for Untrusted Code

```bash
# Run in Docker sandbox
qwen -p "Execute this untrusted code" --sandbox --sandbox-image qwen-code-sandbox
```

### 5. Log Everything for Debugging

```bash
# Enable debug logging
qwen -p "Complex operation" --debug 2>&1 | tee operation.log
```

---

## Troubleshooting

### Command Hangs

1. **Check approval mode**: Interactive approval may be waiting
2. **Use --yolo**: For full automation
3. **Set timeout**: `timeout 300 qwen ...`

### Output Not JSON

1. **Verify flag**: Use `--output-format json`
2. **Check for errors**: Error messages may be printed to stderr

### Authentication Issues

1. **Set API key**: `export QWEN_API_KEY="..."`
2. **Check credentials**: Run `qwen /auth` interactively first

### Memory Issues

For large projects:
```bash
# Increase Node.js memory
export NODE_OPTIONS="--max-old-space-size=4096"
qwen -p "Analyze entire codebase"
```

---

## Related Documentation

- [Approval Mode](./approval-mode) — Control permissions in headless mode
- [Configuration](../configuration/settings) — All settings reference
- [Commands](./commands) — Available slash commands
- [MCP](./mcp) — External tool integration

---

*Last updated: March 2, 2026*
