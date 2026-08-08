# 10 — Tool Architecture

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Critical |
| **Priority** | Highest |

---

## Purpose

This document defines the Tool Runtime of LifeOS.

The Tool Runtime allows AI agents to safely interact with the operating system, external services, and user data.

It provides:

- Tool registry
- Permission engine
- Execution engine
- Validation
- Confirmation flow
- Audit logging
- Future MCP compatibility

Every tool-mediated AI action must follow this document.

It sits under `08-AI-Architecture.md` and `09-Agent-Orchestration.md`. Agents request capabilities; this runtime decides whether and how those requests run.

---

## Philosophy

The AI should never directly modify anything.

Instead:

1. AI requests a tool
2. The Tool Runtime decides: Can it run? Should it ask the user? Did it succeed?

This separation makes the system:

- Secure
- Predictable
- Testable
- Replaceable

---

## High-Level Architecture

```text
User
 │
 ▼
Executive AI
 │
 ▼
Tool Runtime
 │
 ├── Permission Engine
 ├── Validation Engine
 ├── Execution Engine
 ├── Audit Logger
 ├── Tool Registry
 │
 ▼
Individual Tools
 │
 ├── Calendar
 ├── Tasks
 ├── Projects
 ├── Knowledge
 ├── Memory
 ├── Journal
 ├── Finance
 ├── Health
 ├── Search
 ├── OpenRouter
 ├── Integrations
 └── Future MCP
```

---

## Tool Lifecycle

Every tool execution follows the same pipeline:

```text
AI
 → Create Tool Request
 → Validate Input
 → Permission Check
 → Execute
 → Validate Output
 → Log Event
 → Return Result
```

---

## Tool Categories

### Internal Tools

Operate only on LifeOS.

**Examples:** Task · Project · Journal · Goal · Habit · Analytics · Memory · Knowledge

### External Tools

Interact with third-party services.

**Examples:** Google Calendar · Google Tasks · OpenRouter · GitHub · Email · Cloud storage

**Future:** Spotify · Discord · Slack · Maps

### Utility Tools

Support AI reasoning.

**Examples:** Search · Date · Timezone · Markdown · Parser · Summarizer · Vector search · Embedding · Tokenizer

---

## Tool Registry

Every tool must register itself.

Each registration includes:

- Tool name
- Description
- Input schema
- Output schema
- Permissions
- Timeout
- Retry policy
- Supported agent types
- Version

**Examples:**

- `Task.create`
- `Task.update`
- `Calendar.listEvents`
- `Knowledge.search`
- `Memory.retrieve`
- `OpenRouter.chat`

---

## Tool Interface

Every tool implements the same interface.

```ts
execute(input)
  → validate()
  → run()
  → return output
```

No exceptions.

---

## Input Validation

Every tool validates input with Zod.

```text
Invalid input → Reject immediately
```

Never trust AI-generated arguments.

---

## Output Validation

Every tool validates output.

```text
Malformed output → Retry → Error
```

Never return inconsistent data.

---

## Permission Engine

Permissions determine whether a tool can execute.

**Permission levels:**

- Read
- Write
- Delete
- Admin
- Sensitive

### Read Operations

Automatic.

**Examples:** Search notes · Read tasks · Get calendar · Retrieve memory

### Write Operations

Require confirmation.

**Examples:** Create task · Edit goal · Move calendar event · Archive project

### Sensitive Operations

Always require explicit confirmation.

**Examples:**

- Delete project
- Forget memory
- Reset dashboard
- Delete journal
- Disconnect integration

---

## Confirmation Flow

```text
AI
 → "Would you like me to create this task?"
 → User approves
 → Tool executes
 → Success
```

Never skip confirmation for write/sensitive operations.

---

## Execution Engine

**Responsibilities:**

- Queue requests
- Retry failures
- Handle timeouts
- Return structured errors
- Track latency

---

## Retry Policy

```text
Transient error  → Retry up to 3 times
Permanent error  → Return immediately
```

---

## Timeout Policy

Every tool defines a maximum execution time.

Never allow blocking operations.

---

## Audit Logging

Every execution records:

- Timestamp
- Tool
- Arguments (redacted where needed)
- Duration
- Result
- User confirmation
- Errors

**Purpose:** Transparency · Debugging · Analytics

---

## OpenRouter Tool

**Purpose:** Unified access to multiple AI models.

**Responsibilities:**

- Authentication
- Model selection
- Streaming
- Retry
- Fallback
- Cost tracking
- Token tracking
- Error mapping

OpenRouter should not contain business logic.

It is only an AI gateway.

---

## Calendar Tool

- Read events
- Create events
- Update events
- Delete events
- Conflict detection
- Availability
- Time blocking

---

## Task Tool

- CRUD
- Prioritization
- Scheduling
- Completion
- Dependency resolution

---

## Project Tool

- CRUD
- Milestones
- Progress
- Health
- Dependencies

---

## Knowledge Tool

- Search
- Create
- Update
- Link notes
- Backlinks
- Knowledge graph

---

## Memory Tool

- Retrieve
- Store
- Forget
- Summarize
- Classify
- Consent verification

---

## Search Tool

Supports:

- Keyword search
- Semantic search
- Hybrid search
- Filters
- Sorting
- Natural language

---

## Notification Tool

Supports:

- In-app
- Push (future)
- Email (future)
- Digest generation
- Priority rules

---

## Tool Discovery

The Executive AI does not hardcode tool names.

Instead, it queries the Tool Registry.

**Benefits:**

- Easy expansion
- Versioning
- Plugin support
- Testing

---

## Future MCP Support

LifeOS is MCP-compatible.

Future MCP servers register as tools.

No architectural changes required.

**Examples:**

- Filesystem MCP
- GitHub MCP
- Browser MCP
- Google Workspace MCP
- SQL MCP

---

## Security

Every tool must:

- Authenticate
- Authorize
- Validate
- Log
- Handle errors
- Respect rate limits

Never expose secrets.

---

## Testing Requirements

Every tool requires:

- Unit tests
- Schema validation
- Permission tests
- Error tests
- Timeout tests
- Performance tests

---

## Performance Targets

| Operation | Target |
|---|---|
| Tool discovery | < 5 ms |
| Validation | < 2 ms |
| Internal tools | < 50 ms |
| External tools | As fast as the provider allows |

---

## Design Principles

- A tool should do one thing well
- Never mix unrelated responsibilities
- Never expose database access to AI
- Never bypass the Tool Runtime

---

## Golden Rule

Agents think.

Tools act.

The Executive AI decides.

The Tool Runtime enforces.

This separation keeps LifeOS secure, predictable, and extensible.
