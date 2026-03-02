# Common Workflows

Learn common workflows with Qwen Code. Each task includes clear instructions, example commands, and best practices.

---

## Understand New Codebases

### Get a Quick Codebase Overview

When joining a new project, understand its structure quickly:

```bash
cd /path/to/project
qwen
```

Ask for a high-level overview:

```
give me an overview of this codebase
```

Dive deeper:

```
explain the main architecture patterns used here
```

```
what are the key data models?
```

```
how is authentication handled?
```

> [!tip]
> - Start with broad questions, then narrow down
> - Ask about coding conventions and patterns
> - Request a glossary of project-specific terms

### Find Relevant Code

Locate code related to specific features:

```
find the files that handle user authentication
```

```
how do these authentication files work together?
```

```
trace the login process from front-end to database
```

> [!tip]
> - Be specific about what you're looking for
> - Use domain language from the project

---

## Fix Bugs Efficiently

Share the error with Qwen Code:

```
I'm seeing an error when I run npm test
```

Ask for fix recommendations:

```
suggest a few ways to fix the ts-ignore in user.ts
```

Apply the fix:

```
update user.ts to add the null check you suggested
```

> [!tip]
> - Tell Qwen Code the command to reproduce the issue
> - Mention any steps to reproduce the error
> - Let Qwen Code know if the error is intermittent or consistent

---

## Refactor Code

Update old code to use modern patterns:

```
find deprecated API usage in our codebase
```

```
suggest how to refactor utils.js to use modern JavaScript features
```

```
refactor utils.js to use ES 2024 features while maintaining the same behavior
```

Verify the refactoring:

```
run tests for the refactored code
```

> [!tip]
> - Ask Qwen Code to explain the benefits of the modern approach
> - Request changes maintain backward compatibility when needed
> - Do refactoring in small, testable increments

---

## Use Specialized Sub-Agents

Sub-agents are specialized AI assistants for specific tasks.

### View Available Sub-Agents

```
/agents
```

### Use Sub-Agents Automatically

Qwen Code automatically delegates appropriate tasks:

```
review my recent code changes for security issues
```

```
run all tests and fix any failures
```

### Explicitly Request Specific Sub-Agents

```
use the code-reviewer sub-agent to check the auth module
```

```
have the debugger sub-agent investigate why users can't log in
```

### Create Custom Sub-Agents

```
/agents create
```

Define:
- A unique identifier (e.g., `code-reviewer`, `api-designer`)
- When Qwen Code should use this agent
- Which tools it can access
- A system prompt describing the agent's role

> [!tip]
> - Create project-specific sub-agents in `.qwen/agents/` for team sharing
> - Use descriptive `description` fields to enable automatic delegation
> - Limit tool access to what each sub-agent actually needs
> - Learn more about [Sub-Agents](./features/sub-agents)

---

## Work with Tests

### Identify Untested Code

```
find functions in the notification service that are not covered by tests
```

### Generate Test Scaffolding

```
add tests for the notification service
```

### Add Meaningful Test Cases

```
add test cases for edge conditions in the notification service
```

### Run and Verify Tests

```
run the new tests and fix any failures
```

Qwen Code generates tests that follow your project's existing patterns. When asking for tests:
- Be specific about what behavior to verify
- Qwen Code examines existing test files to match style and frameworks
- Ask Qwen Code to identify edge cases you might have missed

---

## Create Pull Requests

### Summarize Your Changes

```
summarize the changes I've made to the authentication module
```

### Generate a Pull Request

```
create a pr
```

### Review and Refine

```
enhance the PR description with more context about the security improvements
```

### Add Testing Details

```
add information about how these changes were tested
```

> [!tip]
> - Ask Qwen Code directly to make a PR for you
> - Review Qwen Code's generated PR before submitting
> - Ask Qwen Code to highlight potential risks or considerations

---

## Handle Documentation

### Identify Undocumented Code

```
find functions without proper JSDoc comments in the auth module
```

### Generate Documentation

```
add JSDoc comments to the undocumented functions in auth.js
```

### Review and Enhance

```
improve the generated documentation with more context and examples
```

### Verify Documentation

```
check if the documentation follows our project standards
```

> [!tip]
> - Specify the documentation style you want (JSDoc, docstrings, etc.)
> - Ask for examples in the documentation
> - Request documentation for public APIs, interfaces, and complex logic

---

## Reference Files and Directories

Use `@` to include files or directories without waiting for Qwen Code to read them.

### Reference a Single File

```
Explain the logic in @src/utils/auth.js
```

### Reference a Directory

```
What's the structure of @src/components?
```

### Reference MCP Resources

```
Show me the data from @github: repos/owner/repo/issues
```

> [!tip]
> - File paths can be relative or absolute
> - @ file references add `QWEN.md` in the file's directory to context
> - Directory references show file listings, not contents
> - You can reference multiple files in a single message
> - Learn more about [Commands](./features/commands)

---

## Resume Previous Conversations

Qwen Code provides two options for resuming previous conversations:

### Continue the Most Recent Conversation

```bash
qwen --continue
```

This immediately resumes your most recent conversation without any prompts.

### Show Conversation Picker

```bash
qwen --resume
```

This displays an interactive conversation selector showing:
- Session summary (or initial prompt)
- Metadata: time elapsed, message count, and git branch

### Continue in Non-Interactive Mode

```bash
qwen --continue -p "Continue with my task"
```

> [!tip]
> - Conversation history is stored locally on your machine
> - Use `--continue` for quick access to your most recent conversation
> - Use `--resume` when you need to select a specific past conversation
> - When resuming, you'll see the entire conversation history before continuing

---

## Run Parallel Qwen Code Sessions with Git Worktrees

Git worktrees allow you to check out multiple branches from the same repository into separate directories, enabling parallel Qwen Code sessions.

### Create a New Worktree

```bash
# Create a new worktree with a new branch
git worktree add ../project-feature-a -b feature-a

# Or create a worktree with an existing branch
git worktree add ../project-bugfix bugfix-123
```

### Run Qwen Code in Each Worktree

```bash
cd ../project-feature-a
qwen
```

### Manage Your Worktrees

```bash
# List all worktrees
git worktree list

# Remove a worktree when done
git worktree remove ../project-feature-a
```

> [!tip]
> - Each worktree has its own independent file state
> - Changes made in one worktree won't affect others
> - All worktrees share the same Git history and remote connections
> - Use descriptive directory names to identify each worktree's task

---

## Use Qwen Code as a Unix-Style Utility

### Add Qwen Code to Your Verification Process

Use Qwen Code as a linter or code reviewer:

```json
// package.json
{
  "scripts": {
    "lint:qwen": "qwen -p 'you are a linter. look at the changes vs. main and report any issues. report the filename and line number on one line, and a description on the second line.'"
  }
}
```

### Pipe Data Through Qwen Code

```bash
cat build-error.txt | qwen -p 'concisely explain the root cause of this build error' > output.txt
```

### Control Output Format

**Text format (default):**
```bash
cat data.txt | qwen -p 'summarize this data' --output-format text > summary.txt
```

**JSON format:**
```bash
cat code.py | qwen -p 'analyze this code for bugs' --output-format json > analysis.json
```

**Streaming JSON format:**
```bash
cat log.txt | qwen -p 'parse this log file for errors' --output-format stream-json
```

> [!tip]
> - Use pipes to integrate Qwen Code into existing shell scripts
> - Combine with other Unix tools for powerful workflows
> - Use `--output-format json` when you need structured output
> - Learn more about [Headless Mode](./features/headless)

---

## Ask Qwen Code About Its Capabilities

Qwen Code has built-in access to its documentation and can answer questions about its own features.

### Example Questions

```
can Qwen Code create pull requests?
```

```
how does Qwen Code handle permissions?
```

```
what slash commands are available?
```

```
how do I use MCP with Qwen Code?
```

```
what are the limitations of Qwen Code?
```

> [!note]
> Qwen Code provides documentation-based answers to these questions. For executable examples, refer to the specific workflow sections above.

> [!tip]
> - Qwen Code always has access to the latest documentation
> - Ask specific questions to get detailed answers
> - Qwen Code can explain complex features like MCP integration and advanced workflows

---

## Related Documentation

- [Quick Start](./quickstart) — Getting started in 30 seconds
- [Commands](./features/commands) — Slash, @, and ! commands
- [Sub-Agents](./features/sub-agents) — Specialized AI assistants
- [Skills](./features/skills) — Create custom AI capabilities
- [Headless Mode](./features/headless) — Automation and CI/CD

---

*Last updated: March 2, 2026*
