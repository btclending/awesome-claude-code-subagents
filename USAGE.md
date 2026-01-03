# How to Use Awesome Claude Code Subagents

This guide explains how to use the subagents in this repository with Claude Code.

## What Are Subagents?

Subagents are specialized AI agents that extend Claude Code's capabilities. Each subagent is an expert in a specific domain (like backend development, security auditing, or data engineering) and operates in its own isolated context window.

**Key benefits:**
- **Specialized expertise** - Domain-specific knowledge and best practices
- **Isolated context** - Each subagent works independently without cluttering your main conversation
- **Tool permissions** - Fine-grained control over what each subagent can do
- **Reusable** - Use the same subagents across all your projects

## Quick Start

### Method 1: Copy Files Directly

1. **Find the subagent you need** - Browse the `categories/` folder
2. **Copy the `.md` file** to your project's `.claude/agents/` directory
3. **Start using it** - Claude Code automatically detects and loads the subagent

```bash
# Example: Add the backend-developer subagent to your project
mkdir -p .claude/agents
cp categories/01-core-development/backend-developer.md .claude/agents/
```

### Method 2: Global Installation

For subagents you want available across all projects:

```bash
# Copy to your global agents directory
mkdir -p ~/.claude/agents
cp categories/04-quality-security/code-reviewer.md ~/.claude/agents/
```

### Method 3: Use the /agents Command

Claude Code has a built-in interface for managing subagents:

```bash
/agents
```

From here you can:
- View existing subagents
- Create new subagents (Claude can draft them for you)
- Edit subagent configurations
- Set tool permissions

## Using Subagents in Conversations

Once installed, you can invoke subagents in several ways:

### Automatic Invocation
Claude Code will automatically use the appropriate subagent when it matches the task:

```
> Review my latest commit for security issues
# Claude Code automatically uses security-auditor or code-reviewer
```

### Explicit Invocation
Request a specific subagent by name:

```
> Have the backend-developer subagent design the API for user authentication
```

```
> Ask the typescript-pro to help refactor this module
```

### Task Delegation
Claude Code can delegate complex tasks to specialized subagents:

```
> Build a REST API for managing products with PostgreSQL storage
# Claude Code may use: api-designer, backend-developer, postgres-pro
```

## Subagent File Structure

Each subagent follows a standard format:

```yaml
---
name: subagent-name
description: When this agent should be invoked
tools: Read, Write, Edit, Bash, Glob, Grep
---

[Detailed agent instructions and expertise areas]

[Checklists and guidelines specific to the domain]

## Communication Protocol
[How the agent communicates status and results]

## Development Workflow
[Structured phases for implementation]
```

### Understanding Tool Permissions

The `tools` field controls what the subagent can do:

| Permission Set | Tools | Use Case |
|----------------|-------|----------|
| **Read-only** | `Read, Grep, Glob` | Code review, auditing |
| **Research** | `Read, Grep, Glob, WebFetch, WebSearch` | Research, analysis |
| **Full development** | `Read, Write, Edit, Bash, Glob, Grep` | Building features |
| **Documentation** | `Read, Write, Edit, Glob, Grep, WebFetch, WebSearch` | Writing docs |

## Choosing the Right Subagent

### By Task Type

| Task | Recommended Subagent |
|------|---------------------|
| Build a REST API | `backend-developer`, `api-designer` |
| Review code quality | `code-reviewer` |
| Fix security issues | `security-auditor`, `penetration-tester` |
| Write tests | `qa-expert`, `test-automator` |
| Optimize database | `postgres-pro`, `database-optimizer` |
| Deploy to cloud | `cloud-architect`, `devops-engineer` |
| Build React UI | `react-specialist`, `frontend-developer` |
| Debug issues | `debugger`, `error-detective` |

### By Technology Stack

| Stack | Subagents |
|-------|-----------|
| **Node.js/TypeScript** | `typescript-pro`, `backend-developer`, `nextjs-developer` |
| **Python** | `python-pro`, `django-developer`, `data-scientist` |
| **Go** | `golang-pro`, `backend-developer` |
| **React** | `react-specialist`, `frontend-developer` |
| **Kubernetes** | `kubernetes-specialist`, `devops-engineer` |
| **PostgreSQL** | `postgres-pro`, `database-administrator` |

## Combining Multiple Subagents

Subagents work together on complex tasks. Example workflow:

1. **api-designer** - Designs the API schema and endpoints
2. **backend-developer** - Implements the server-side code
3. **code-reviewer** - Reviews the implementation
4. **test-automator** - Creates comprehensive tests
5. **devops-engineer** - Sets up CI/CD and deployment

## Customizing Subagents

You can modify any subagent to fit your needs:

1. Copy the subagent file to your `.claude/agents/` directory
2. Edit the file to add your specific requirements
3. Adjust tool permissions as needed
4. Add project-specific guidelines or patterns

Example customization:

```yaml
---
name: my-backend-developer
description: Backend developer for our Django + PostgreSQL stack
tools: Read, Write, Edit, Bash, Glob, Grep
---

You are a backend developer specializing in our Django 5.0 codebase.

Always follow our conventions:
- Use Django REST Framework for APIs
- Follow our naming conventions in /docs/conventions.md
- Run tests with: pytest --cov
- Use our custom base classes in /core/
```

## Categories Overview

| Category | Focus Area | Example Subagents |
|----------|------------|-------------------|
| **01-core-development** | Essential dev tasks | backend-developer, frontend-developer, mobile-developer |
| **02-language-specialists** | Language expertise | typescript-pro, python-pro, rust-engineer |
| **03-infrastructure** | DevOps & Cloud | kubernetes-specialist, terraform-engineer, cloud-architect |
| **04-quality-security** | Testing & Security | code-reviewer, security-auditor, qa-expert |
| **05-data-ai** | ML & Data | data-scientist, ml-engineer, postgres-pro |
| **06-developer-experience** | Tooling & DX | documentation-engineer, refactoring-specialist |
| **07-specialized-domains** | Domain experts | blockchain-developer, game-developer, fintech-engineer |
| **08-business-product** | Product & Business | product-manager, technical-writer |
| **09-meta-orchestration** | Multi-agent coordination | workflow-orchestrator, multi-agent-coordinator |
| **10-research-analysis** | Research & Analysis | research-analyst, competitive-analyst |

## Tips for Best Results

1. **Be specific** - Tell Claude Code exactly what you need
2. **Provide context** - Share relevant files or documentation
3. **Use the right subagent** - Match the task to the specialist
4. **Review outputs** - Subagents are powerful but should be reviewed
5. **Iterate** - Refine subagent configurations based on your experience

## Troubleshooting

### Subagent not found
- Check the file is in `.claude/agents/` or `~/.claude/agents/`
- Verify the file has a `.md` extension
- Ensure the YAML frontmatter is valid

### Wrong subagent being used
- Be more explicit in your request: "Use the security-auditor subagent to..."
- Check for naming conflicts between project and global subagents

### Subagent has too few/many permissions
- Edit the `tools` field in the subagent file
- Leave `tools` empty to inherit all available tools

## Contributing

Found a useful subagent configuration? Share it!

1. Fork this repository
2. Add your subagent to the appropriate category
3. Follow the standard template structure
4. Submit a pull request

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.
