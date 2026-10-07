Claro. Para o GitHub, eu usaria um nome mais técnico e uma descrição curta, deixando toda a profundidade para o README.

**Nome do repositório**

`legacy-code`

**Descrição curta do GitHub**

> AI-native software engineering platform for autonomous coding, agent orchestration, workspaces, tools, MCP, Git, terminal and multi-provider LLM infrastructure.

**Topics sugeridos**

`ai` `software-engineering` `ai-agents` `coding-agent` `developer-tools` `mcp` `llm` `nvidia-ai` `git` `automation` `typescript` `astro` `react` `agentic-ai`

E este seria o README principal:

```markdown
# Legacy Code

> AI-native software engineering platform for building, analyzing, modifying, testing and operating software through natural language.

Legacy Code is an AI Software Engineering Platform designed to transform natural-language instructions into real engineering workflows.

Instead of functioning only as a conversational AI interface, Legacy Code is designed around an engineering runtime capable of understanding projects, operating on workspaces, executing tools, interacting with Git repositories, using MCP servers, running commands, executing tests and orchestrating specialized AI agents.

The interface is a chat.

The product is the engineering runtime behind it.

---

## Vision

Legacy Code aims to provide an AI-native development environment where developers can interact with software projects using natural language while maintaining the control, security, observability and engineering discipline required for production systems.

A typical workflow can look like:

```text
User
  │
  ▼
Natural Language
  │
  ▼
Legacy Code
  │
  ├── Project Context
  ├── Agent Runtime
  ├── AI Gateway
  ├── Tool Runtime
  ├── Workspace Runtime
  ├── Git Runtime
  ├── MCP Runtime
  ├── Skills Runtime
  └── Task Engine
          │
          ▼
      Real Project
          │
          ├── Files
          ├── Code
          ├── Tests
          ├── Git
          ├── Terminal
          └── Infrastructure
```

The objective is not to generate code blindly.

The objective is to build, modify, validate and operate software through an auditable engineering workflow.

---

# Core Capabilities

Legacy Code is being designed around the following capabilities.

## AI Engineering

- Natural-language software development
- Code generation
- Code modification
- Refactoring
- Debugging
- Architecture analysis
- Code review
- Technical documentation
- Automated testing
- Build verification
- Repository analysis
- Dependency analysis
- Security analysis

---

## Agent Runtime

Legacy Code uses an agent-oriented execution model.

The default engineering lifecycle is:

```text
UNDERSTAND
    ↓
ANALYZE
    ↓
PLAN
    ↓
APPROVE
    ↓
EXECUTE
    ↓
VERIFY
    ↓
REPORT
```

Agents are not expected to simply generate a response.

They can perform controlled engineering operations through the Tool Runtime.

---

## AI Gateway

All model communication is abstracted behind a provider-independent AI Gateway.

```text
Application
    │
    ▼
AI Gateway
    │
    ├── NVIDIA
    ├── OpenAI
    ├── Anthropic
    ├── Ollama
    └── Custom Providers
```

The initial implementation is designed around NVIDIA-hosted models.

The architecture intentionally avoids coupling the application domain to a single model provider.

### Provider abstraction

```text
AIProvider
├── generate()
├── stream()
├── embeddings()
├── capabilities()
└── usage()
```

Providers can be implemented through adapters.

---

# Tool Runtime

The Tool Runtime provides a controlled execution layer between agents and external capabilities.

An agent does not directly access infrastructure.

Instead:

```text
Agent
  │
  ▼
Tool Runtime
  │
  ▼
Permission Check
  │
  ▼
Tool
  │
  ▼
Execution
  │
  ▼
Tool Result
  │
  ▼
Agent
```

This architecture provides a central location for:

- authorization
- validation
- auditing
- timeout management
- execution policies
- risk classification
- error handling
- observability

---

# Core Tools

The platform is designed to support tools such as:

### Filesystem

- `read_file`
- `write_file`
- `edit_file`
- `delete_file`
- `list_files`
- `search_files`
- `search_code`

### Terminal

- `run_command`
- `run_tests`
- `run_build`

### Git

- `git_status`
- `git_diff`
- `git_log`
- `git_branch`
- `git_checkout`
- `git_commit`
- `git_pull`
- `git_push`

### Repository

- `clone_repository`
- `inspect_repository`
- `analyze_repository`

The Tool Registry is designed to allow new tools to be added without changing the Agent Runtime.

---

# Workspace Runtime

A Workspace represents an isolated development environment.

A workspace can contain:

```text
Workspace
├── Repository
├── Branch
├── Filesystem
├── Terminal
├── Context
├── Memory
├── Tools
├── MCPs
├── Skills
└── Permissions
```

The Workspace Runtime is responsible for controlling access to the project environment.

---

# Filesystem Runtime

Filesystem operations are abstracted behind a provider interface.

```text
FileSystemProvider
```

Expected operations include:

```text
read
write
create
delete
rename
move
copy
list
search
```

The filesystem layer is designed to support multiple execution environments, including local and remote workspaces.

---

# Terminal Runtime

The Terminal Runtime provides controlled command execution inside the active workspace.

Each execution can record:

```text
command
working_directory
stdout
stderr
exit_code
duration
status
user
agent
timestamp
```

Terminal execution must respect:

- workspace boundaries
- command policies
- permissions
- timeouts
- cancellation
- auditing

The goal is to prevent uncontrolled host-level execution.

---

# Git Runtime

Git is treated as an infrastructure capability rather than being directly embedded into agents.

The platform provides a Git abstraction capable of supporting:

- repository status
- diff
- history
- branches
- checkout
- commits
- pull
- push
- merge
- tags

The architecture is designed to support future integrations with Git hosting providers.

---

# MCP Runtime

Legacy Code is designed to support Model Context Protocol (MCP) servers.

MCP provides an extensibility layer for connecting external systems and capabilities to AI agents.

The MCP Runtime is responsible for:

- server registration
- configuration
- connection management
- tool discovery
- tool execution
- permissions
- lifecycle management
- health checks

Conceptually:

```text
Legacy Code
    │
    ▼
MCP Runtime
    │
    ├── MCP Server
    │     ├── Tools
    │     └── Resources
    │
    ├── MCP Server
    │     ├── Tools
    │     └── Resources
    │
    └── MCP Server
```

MCP integrations should not require changes to the Agent Core.

---

# Skills Runtime

Skills provide reusable engineering behavior.

Examples:

```text
Frontend Engineer
Backend Engineer
Database Engineer
DevOps Engineer
Security Engineer
QA Engineer
Architecture Reviewer
Code Reviewer
Technical Writer
```

A Skill can define:

```text
instructions
tools
permissions
model
context
validation
```

Skills are intended to be composable and reusable across projects.

---

# Project Context Engine

AI agents need context without receiving an entire repository in every request.

Legacy Code therefore provides a Context Engine responsible for collecting and retrieving relevant project information.

Potential context sources include:

- source code
- project structure
- README
- documentation
- package manifests
- configuration
- Git history
- architecture decisions
- project memory
- task history

The goal is contextual precision rather than indiscriminate context injection.

---

# Memory

Legacy Code separates different types of memory.

```text
Conversation Memory
Project Memory
Task Memory
Architecture Memory
```

Memory must remain isolated by project and execution context.

---

# Task Engine

Long-running engineering operations are represented as tasks.

Example:

```text
User:
"Analyze this repository and fix all critical issues."
```

The Task Engine can represent:

```text
QUEUED
   ↓
PLANNING
   ↓
RUNNING
   ↓
WAITING_APPROVAL
   ↓
VERIFYING
   ↓
COMPLETED
```

Failure states include:

```text
FAILED
CANCELLED
PAUSED
```

Tasks should support:

- pause
- resume
- cancel
- retry
- progress
- logs
- tool execution history
- verification results

---

# Approval System

Actions with meaningful side effects should be subject to explicit authorization.

Examples include:

- deleting files
- pushing Git changes
- merging branches
- modifying databases
- running migrations
- production deployments
- external mutations

The architecture supports policies such as:

```text
DENY
ASK
ALLOW
```

Permissions can be evaluated based on:

- user
- project
- workspace
- agent
- tool
- operation
- risk level

---

# Security

Security is a first-class concern.

The platform is designed around:

- authentication
- authorization
- RBAC
- workspace isolation
- tool permissions
- MCP permissions
- secret protection
- audit logs
- rate limiting
- command policies
- execution boundaries

API keys and credentials must never be exposed to the browser.

---

# Observability

Engineering automation requires visibility.

Legacy Code is designed to support:

- structured logging
- request IDs
- correlation IDs
- metrics
- distributed tracing
- AI request tracking
- tool execution tracking
- task execution tracking
- error tracking
- token usage
- latency monitoring

OpenTelemetry is the preferred observability architecture.

---

# Architecture

The platform follows modular architecture principles inspired by:

- Clean Architecture
- Domain-Driven Design
- SOLID
- Hexagonal Architecture
- Ports and Adapters
- Dependency Inversion
- API-first design
- Event-driven architecture

The logical architecture is:

```text
┌─────────────────────────────────────────────┐
│                  UI / Chat                  │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│                    API                      │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│               Application Layer             │
│                                             │
│ Chat │ Projects │ Tasks │ Agents │ Tools    │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│                 Domain Core                 │
│                                             │
│ Agents │ Workspaces │ Tasks │ Permissions   │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│               Infrastructure                │
│                                             │
│ AI │ Git │ MCP │ FS │ Terminal │ Database   │
└─────────────────────────────────────────────┘
```

---

# Frontend

The current frontend is designed using:

- Astro
- React
- TypeScript
- Tailwind CSS

Astro provides the application shell and routing architecture.

React is used for highly interactive application components such as:

- chat
- streaming responses
- code editor
- terminal
- file explorer
- diff viewer
- task execution
- agent controls
- MCP management

The UI follows a clean, light-first interface focused on developer productivity.

---

# Backend

The backend is responsible for:

- authentication
- project management
- workspace management
- AI orchestration
- agents
- tools
- MCP
- Git
- tasks
- permissions
- persistence
- auditing
- observability

The backend must remain independent from the UI.

---

# Data Layer

PostgreSQL is the preferred relational database.

Core entities include:

```text
users
sessions
projects
workspaces
repositories
conversations
messages
tasks
task_steps
agents
agent_sessions
tools
tool_calls
mcp_servers
mcp_tools
skills
providers
models
audit_logs
git_operations
project_memory
architecture_decisions
```

The schema should evolve through versioned migrations.

---

# API

The API exposes application capabilities through stable contracts.

Primary areas include:

```text
/auth
/projects
/workspaces
/chat
/messages
/tasks
/agents
/tools
/repositories
/git
/mcp
/skills
/models
/providers
/settings
```

The frontend must communicate with the backend through documented API contracts.

---

# Configuration

Secrets must be supplied through environment variables or an appropriate secret-management system.

Example:

```env
NVIDIA_API_KEY=
DATABASE_URL=
REDIS_URL=
GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
JWT_SECRET=
ENCRYPTION_KEY=
```

Never commit credentials.

Never expose provider API keys to browser code.

---

# Development

Install dependencies:

```bash
pnpm install
```

Start development:

```bash
pnpm dev
```

Run type checking:

```bash
pnpm typecheck
```

Run lint:

```bash
pnpm lint
```

Run tests:

```bash
pnpm test
```

Build:

```bash
pnpm build
```

The exact commands may vary according to the current workspace configuration.

---

# Engineering Principles

Legacy Code follows several non-negotiable principles.

### One responsibility

Every module should have a clear responsibility.

### One canonical implementation

Avoid duplicate implementations of the same subsystem.

### Dependency inversion

Domain logic must not depend directly on infrastructure providers.

### Provider independence

AI providers, Git providers, filesystem providers and other infrastructure should be replaceable.

### Explicit permissions

Agents must not automatically receive unrestricted access to infrastructure.

### Observable execution

Important operations must be auditable and observable.

### Production-oriented design

Mocks and placeholders should not be treated as completed functionality.

### Incremental evolution

Existing functionality should be analyzed and reused before introducing replacement systems.

---

# Repository Structure

The exact repository structure evolves with the implementation, but the target architecture follows clear boundaries.

Conceptually:

```text
legacy-code/
│
├── apps/
│   ├── web/
│   ├── api/
│   └── worker/
│
├── packages/
│   ├── domain/
│   ├── application/
│   ├── infrastructure/
│   ├── ai/
│   ├── agents/
│   ├── tools/
│   ├── workspace/
│   ├── filesystem/
│   ├── terminal/
│   ├── git/
│   ├── mcp/
│   ├── skills/
│   ├── tasks/
│   ├── security/
│   └── shared/
│
├── docs/
│
├── tests/
│
├── scripts/
│
├── docker/
│
└── README.md
```

This is a logical target, not a requirement to duplicate directories that already exist.

Existing implementations should be consolidated before new modules are introduced.

---

# Development Philosophy

Legacy Code is intentionally designed to avoid the common failure mode of AI-generated software:

```text
Beautiful UI
      +
Fake backend
      +
Mock data
      +
Disconnected buttons
      =
Non-production software
```

Instead:

```text
UI
 +
API
 +
Domain
 +
Infrastructure
 +
Real execution
 +
Validation
 +
Observability
 =
Engineering Platform
```

A feature is not considered complete merely because its interface exists.

A feature is complete when:

```text
Implementation
    +
Persistence
    +
Integration
    +
Validation
    +
Tests
    +
Error handling
```

are all present.

---

# Roadmap

## Phase 1 — Foundation

- repository audit
- architecture consolidation
- configuration cleanup
- dependency cleanup
- database foundation
- API foundation

## Phase 2 — AI Core

- AI Gateway
- NVIDIA provider
- model registry
- streaming
- usage tracking

## Phase 3 — Agent Core

- agent runtime
- planning
- execution
- verification
- permissions

## Phase 4 — Workspace

- workspace management
- filesystem
- terminal
- project detection

## Phase 5 — Engineering Tools

- Tool Registry
- Git Runtime
- repository analysis
- test execution
- build execution

## Phase 6 — Extensibility

- MCP Runtime
- Skills Runtime
- Plugins
- external connectors

## Phase 7 — Context

- project indexing
- context retrieval
- project memory
- architecture memory

## Phase 8 — Production

- security hardening
- audit
- observability
- performance
- automated testing
- CI/CD
- deployment

---

# Status

🚧 **Active Development**

Legacy Code is under active development.

Architecture and APIs may evolve while the core platform is being consolidated.

The project prioritizes engineering correctness and extensibility over premature feature completeness.

---

# Security

If you discover a security vulnerability, do not disclose it publicly through a GitHub issue.

Use the project's private security reporting mechanism when available.

Never submit:

- API keys
- credentials
- access tokens
- private source code
- personal data

to public issues or pull requests.

---

# Contributing

Contributions should follow the architectural boundaries established by the project.

Before implementing a new subsystem:

1. Search for an existing implementation.
2. Determine whether it can be reused.
3. Determine whether it should be refactored.
4. Avoid creating duplicate abstractions.
5. Add tests.
6. Update documentation.
7. Validate type checking and builds.

Pull requests should explain:

- problem
- architectural impact
- implementation
- tests
- security implications
- migration requirements

---

# License

License information will be defined as the project reaches its distribution stage.

---

# Legacy Code

**AI-native software engineering.**

Build software.

Analyze systems.

Operate repositories.

Execute engineering tasks.

With AI at the center of the development workflow.
```

# Legacy-Code
