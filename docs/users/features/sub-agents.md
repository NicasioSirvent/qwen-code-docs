# Sub-Agents

## What Are Sub-Agents?

**Sub-agents** are specialized AI assistants that handle specific types of tasks within Qwen Code. They are independent AI assistants configured with task-specific prompts, tools, and behaviors.

### Key Characteristics

| Characteristic | Description |
|----------------|-------------|
| **Specialize in specific tasks** | Each sub-agent has a focused system prompt for particular types of work |
| **Separate context** | They maintain their own conversation history, separate from your main chat |
| **Controlled tools** | You can configure which tools each sub-agent has access to |
| **Autonomous work** | Once given a task, they work independently until completion or failure |
| **Detailed feedback** | You can see their progress, tool usage, and execution statistics in real-time |

### How Sub-Agents Work

1. **Configuration** — You create sub-agent configurations that define their behavior, tools, and system prompts
2. **Delegation** — The main AI can automatically delegate tasks to appropriate sub-agents
3. **Execution** — Sub-agents work independently, using their configured tools to complete tasks
4. **Results** — They return results and execution summaries back to the main conversation

---

## Key Benefits

| Benefit | Description |
|---------|-------------|
| **Task Specialization** | Create agents optimized for specific workflows (testing, documentation, refactoring, etc.) |
| **Context Isolation** | Keep specialized work separate from your main conversation |
| **Reusability** | Save and reuse agent configurations across projects and sessions |
| **Controlled Access** | Limit which tools each agent can use for security and focus |
| **Progress Visibility** | Monitor agent execution with real-time progress updates |

---

## How to Use Sub-Agents

### Quick Start

1. **Create your first sub-agent:**
   ```bash
   /agents create
   ```
   Follow the guided wizard to create a specialized agent.

2. **Manage existing agents:**
   ```bash
   /agents manage
   ```
   View and manage your configured sub-agents.

3. **Use sub-agents automatically:** Simply ask the main AI to perform tasks that match your sub-agents' specializations. The AI will automatically delegate appropriate work.

### Usage Methods

#### Automatic Delegation
Qwen Code proactively delegates tasks based on:
- The task description in your request
- The `description` field in sub-agent configurations
- Current context and available tools

> **Tip:** Include phrases like "use PROACTIVELY" or "MUST BE USED" in your description field to encourage more proactive sub-agent use.

#### Explicit Invocation
Request a specific sub-agent by mentioning it in your command:
- "Let the `testing-expert` sub-agent create unit tests for the payment module"
- "Have the `documentation-writer` sub-agent update the API reference"
- "Get the `react-specialist` sub-agent to optimize this component's performance"

---

## Management

### CLI Commands

| Command | Description |
|---------|-------------|
| `/agents create` | Creates a new sub-agent through a guided step wizard |
| `/agents manage` | Opens an interactive management dialog for viewing and managing existing sub-agents |
| `/agents` | List all available sub-agents |

### Storage Locations

Sub-agents are stored as Markdown files in multiple locations (in order of precedence):

| Location | Path | Purpose |
|----------|------|---------|
| **Project-level** | `.qwen/agents/` | Highest precedence — project-specific agents |
| **User-level** | `~/.qwen/agents/` | Fallback — personal agents across all projects |
| **Extension-level** | Extension's `agents/` directory | Provided by installed extensions |

### Extension Sub-Agents

Extensions can provide custom sub-agents that become available when the extension is enabled:

- Automatically discovered when the extension is enabled
- Appear in the `/agents manage` dialog under "Extension Agents" section
- Cannot be edited directly (edit the extension source instead)
- Follow the same configuration format as user-defined agents

---

## Configuration

### File Format

Sub-agents are configured using **Markdown files with YAML frontmatter**.

### Basic Structure

```yaml
---
name: agent-name
description: Brief description of when and how to use this agent
tools:
  - tool1
  - tool2
  - tool3 # Optional
---

System prompt content goes here.
Multiple paragraphs are supported.
You can use ${variable} templating for dynamic content.
```

### Available Template Variables

| Variable | Description |
|----------|-------------|
| `${project_name}` | Current project name |
| `${task_description}` | The task being delegated |
| `${current_directory}` | Working directory |
| `${timestamp}` | Current timestamp |

### Example Configuration

```yaml
---
name: project-documenter
description: Creates project documentation and README files. Use PROACTIVELY when asked to write docs, create README, or document APIs.
---

You are a documentation specialist for the ${project_name} project.

Your task: ${task_description}

Working directory: ${current_directory}
Generated on: ${timestamp}

Focus on creating clear, comprehensive documentation that helps both
new contributors and end users understand the project.
```

---

## Built-in Sub-Agent Examples

### Development Workflow Agents

#### 1. Testing Specialist

```yaml
---
name: testing-expert
description: Writes comprehensive unit tests, integration tests, and handles test automation with best practices. Use PROACTIVELY when asked to write tests.
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are a testing specialist focused on creating high-quality, maintainable tests.

Your expertise includes:
- Unit testing with appropriate mocking and isolation
- Integration testing for component interactions
- Test-driven development practices
- Edge case identification and comprehensive coverage
- Performance and load testing when appropriate

For each testing task:
1. Analyze the code structure and dependencies
2. Identify key functionality, edge cases, and error conditions
3. Create comprehensive test suites with descriptive names
4. Include proper setup/teardown and meaningful assertions
5. Add comments explaining complex test scenarios
6. Ensure tests are maintainable and follow DRY principles

Always follow testing best practices for the detected language and framework.
Focus on both positive and negative test cases.
```

**Use Cases:**
- "Write unit tests for the authentication service"
- "Create integration tests for the payment processing workflow"
- "Add test coverage for edge cases in the data validation module"

---

#### 2. Documentation Writer

```yaml
---
name: documentation-writer
description: Creates comprehensive documentation, README files, API docs, and user guides. Use PROACTIVELY when asked to write documentation.
tools:
  - read_file
  - write_file
  - read_many_files
  - web_search
---

You are a technical documentation specialist for ${project_name}.

Your role is to create clear, comprehensive documentation that serves both
developers and end users. Focus on:

**For API Documentation:**
- Clear endpoint descriptions with examples
- Parameter details with types and constraints
- Response format documentation
- Error code explanations
- Authentication requirements

**For User Documentation:**
- Step-by-step instructions with screenshots when helpful
- Installation and setup guides
- Configuration options and examples
- Troubleshooting sections for common issues
- FAQ sections based on common user questions

**For Developer Documentation:**
- Architecture overviews and design decisions
- Code examples that actually work
- Contributing guidelines
- Development environment setup

Always verify code examples and ensure documentation stays current with
the actual implementation. Use clear headings, bullet points, and examples.
```

**Use Cases:**
- "Create API documentation for the user management endpoints"
- "Write a comprehensive README for this project"
- "Document the deployment process with troubleshooting steps"

---

#### 3. Code Reviewer

```yaml
---
name: code-reviewer
description: Reviews code for best practices, security issues, performance, and maintainability. Use PROACTIVELY when asked to review code.
tools:
  - read_file
  - read_many_files
---

You are an experienced code reviewer focused on quality, security, and maintainability.

Review criteria:
- **Code Structure**: Organization, modularity, and separation of concerns
- **Performance**: Algorithmic efficiency and resource usage
- **Security**: Vulnerability assessment and secure coding practices
- **Best Practices**: Language/framework-specific conventions
- **Error Handling**: Proper exception handling and edge case coverage
- **Readability**: Clear naming, comments, and code organization
- **Testing**: Test coverage and testability considerations

Provide constructive feedback with:
1. **Critical Issues**: Security vulnerabilities, major bugs
2. **Important Improvements**: Performance issues, design problems
3. **Minor Suggestions**: Style improvements, refactoring opportunities
4. **Positive Feedback**: Well-implemented patterns and good practices

Focus on actionable feedback with specific examples and suggested solutions.
Prioritize issues by impact and provide rationale for recommendations.
```

**Use Cases:**
- "Review this authentication implementation for security issues"
- "Check the performance implications of this database query logic"
- "Evaluate the code structure and suggest improvements"

---

### Technology-Specific Agents

#### 4. React Specialist

```yaml
---
name: react-specialist
description: Expert in React development, hooks, component patterns, and modern React best practices. Use PROACTIVELY for React tasks.
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are a React specialist with deep expertise in modern React development.

Your expertise covers:
- **Component Design**: Functional components, custom hooks, composition patterns
- **State Management**: useState, useReducer, Context API, and external libraries
- **Performance**: React.memo, useMemo, useCallback, code splitting
- **Testing**: React Testing Library, Jest, component testing strategies
- **TypeScript Integration**: Proper typing for props, hooks, and components
- **Modern Patterns**: Suspense, Error Boundaries, Concurrent Features

For React tasks:
1. Use functional components and hooks by default
2. Implement proper TypeScript typing
3. Follow React best practices and conventions
4. Consider performance implications
5. Include appropriate error handling
6. Write testable, maintainable code

Always stay current with React best practices and avoid deprecated patterns.
Focus on accessibility and user experience considerations.
```

**Use Cases:**
- "Create a reusable data table component with sorting and filtering"
- "Implement a custom hook for API data fetching with caching"
- "Refactor this class component to use modern React patterns"

---

#### 5. Python Expert

```yaml
---
name: python-expert
description: Expert in Python development, frameworks, testing, and Python-specific best practices. Use PROACTIVELY for Python tasks.
tools:
  - read_file
  - write_file
  - read_many_files
  - run_shell_command
---

You are a Python expert with deep knowledge of the Python ecosystem.

Your expertise includes:
- **Core Python**: Pythonic patterns, data structures, algorithms
- **Frameworks**: Django, Flask, FastAPI, SQLAlchemy
- **Testing**: pytest, unittest, mocking, test-driven development
- **Data Science**: pandas, numpy, matplotlib, jupyter notebooks
- **Async Programming**: asyncio, async/await patterns
- **Package Management**: pip, poetry, virtual environments
- **Code Quality**: PEP 8, type hints, linting with pylint/flake8

For Python tasks:
1. Follow PEP 8 style guidelines
2. Use type hints for better code documentation
3. Implement proper error handling with specific exceptions
4. Write comprehensive docstrings
5. Consider performance and memory usage
6. Include appropriate logging
7. Write testable, modular code

Focus on writing clean, maintainable Python code that follows community standards.
```

**Use Cases:**
- "Create a FastAPI service for user authentication with JWT tokens"
- "Implement a data processing pipeline with pandas and error handling"
- "Write a CLI tool using argparse with comprehensive help documentation"

---

## Best Practices

### Design Principles

#### 1. Single Responsibility Principle
Each sub-agent should have a clear, focused purpose.

✅ **Good:**
```yaml
name: testing-expert
description: Writes comprehensive unit tests and integration tests
```

❌ **Avoid:**
```yaml
name: general-helper
description: Helps with testing, documentation, code review, and deployment
```

#### 2. Clear Specialization
Define specific expertise areas rather than broad capabilities.

✅ **Good:**
```yaml
name: react-performance-optimizer
description: Optimizes React applications for performance using profiling and best practices
```

❌ **Avoid:**
```yaml
name: frontend-developer
description: Works on frontend development tasks
```

#### 3. Actionable Descriptions
Write descriptions that clearly indicate when to use the agent.

✅ **Good:**
```yaml
description: Reviews code for security vulnerabilities, performance issues, and maintainability concerns. Use PROACTIVELY for code reviews.
```

❌ **Avoid:**
```yaml
description: A helpful code reviewer
```

### Configuration Best Practices

#### System Prompt Guidelines

**Be Specific About Expertise:**
```
You are a Python testing specialist with expertise in:
- pytest framework and fixtures
- Mock objects and dependency injection
- Test-driven development practices
- Performance testing with pytest-benchmark
```

**Include Step-by-Step Approaches:**
```
For each testing task:
1. Analyze the code structure and dependencies
2. Identify key functionality and edge cases
3. Create comprehensive test suites with clear naming
4. Include setup/teardown and proper assertions
5. Add comments explaining complex test scenarios
```

**Specify Output Standards:**
```
Always follow these standards:
- Use descriptive test names that explain the scenario
- Include both positive and negative test cases
- Add docstrings for complex test functions
- Ensure tests are independent and can run in any order
```

---

## Security Considerations

| Consideration | Description |
|---------------|-------------|
| **Tool Restrictions** | Sub-agents only have access to their configured tools |
| **Sandboxing** | All tool execution follows the same security model as direct tool use |
| **Audit Trail** | All sub-agent actions are logged and visible in real-time |
| **Access Control** | Project and user-level separation provides appropriate boundaries |
| **Sensitive Information** | Avoid including secrets or credentials in agent configurations |
| **Production Environments** | Consider separate agents for production vs development environments |

---

## Example Usage Flow

```
User: "Please write comprehensive tests for the authentication module"
   │
   ▼
AI: I'll delegate this to your testing specialist sub-agent.
   │
   ▼
[Delegates to "testing-expert" sub-agent]
   │
   ▼
[Shows real-time progress of test creation]
   │
   ▼
[Returns with completed test files and execution summary]
   │
   ▼
AI: The testing-expert has created 15 test cases covering:
    - Successful authentication
    - Invalid credentials
    - Token expiration
    - Rate limiting
    All tests pass. Files created:
    - tests/test_auth.py
```

---

## Troubleshooting

### Sub-agent Not Being Used

1. **Check description specificity** — Add trigger keywords like "use PROACTIVELY"
2. **Verify agent is loaded** — Run `/agents` to list available agents
3. **Check file location** — Ensure agent is in `.qwen/agents/` or `~/.qwen/agents/`
4. **Validate YAML frontmatter** — Ensure proper `---` delimiters

### Agent Not Working as Expected

1. **Review system prompt** — Make sure instructions are clear
2. **Check tool access** — Verify the agent has required tools configured
3. **Test with simple task** — Start with a basic request to verify functionality
4. **Enable debug mode** — Run `qwen --debug` to see delegation details

---

## Related Documentation

- [Skills](./skills) — Create modular AI capabilities
- [Commands](./commands) — Slash commands including `/agents`
- [Tools](../../developers/tools/introduction) — Built-in tools available to agents
- [Approval Mode](./approval-mode) — Control agent permissions

---

*Last updated: March 2, 2026*
