# 09 — Agent Orchestration

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Critical |
| **Priority** | Highest |

---

## Purpose

This document defines how every AI component inside LifeOS collaborates.

It specifies:

- Executive AI
- Agent routing
- Tool calling
- Memory access
- Context assembly
- Multi-agent reasoning
- Result merging
- Failure recovery

Every multi-agent interaction must follow this document.

It sits under `08-AI-Architecture.md`. That document defines AI philosophy and agent roles; this document defines how they collaborate at runtime.

---

## Philosophy

Users interact with **one AI**.

Never expose multiple bots.

Never ask:

> "Which AI do you want?"

LifeOS decides internally.

---

## Architecture

```text
                         User
                           │
                           ▼
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
                     Executive AI
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
                           │
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
              Planning Engine
              Memory Engine
              Context Engine
              Reasoning Engine
              Tool Engine
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
                           │
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
              Planner Agent
              Calendar Agent
              Knowledge Agent
              Project Agent
              Journal Agent
              Finance Agent
              Health Agent
              Learning Agent
              Analytics Agent
              Relationship Agent
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Executive AI

**Responsibilities:**

- Receive requests
- Understand intent
- Collect context
- Choose agents
- Merge answers
- Explain reasoning
- Maintain personality

The Executive AI owns the conversation.

No specialist may directly reply.

---

## Workflow

```text
User asks
 → Intent Detection
 → Context Retrieval
 → Agent Selection
 → Parallel Execution
 → Merge Results
 → Validate
 → Respond
```

---

## Intent Detection

Every request is classified.

**Possible intents:**

- Planning
- Scheduling
- Learning
- Knowledge
- Research
- Reflection
- Health
- Finance
- Projects
- Goal review
- Quick question
- Search
- System
- Unknown

---

## Agent Selection

```text
Simple question  → One agent
Complex question → Multiple agents
```

**Example:**

> "I'm stressed and my startup deadline is tomorrow."

**Uses:**

- Planner
- Health
- Projects
- Calendar
- Analytics

---

## Parallel Execution

Whenever possible, agents work simultaneously.

**Example:** Planner · Calendar · Knowledge run together.

Never chain unless necessary.

---

## Context Engine

Every agent receives only relevant context.

**Example — Finance Agent gets:**

- Expenses
- Budget
- Subscriptions
- Savings

**Not:**

- Journal
- Learning
- Health

**Principle:** Least context required.

---

## Memory Engine

Memory has three layers:

| Layer | Scope |
|---|---|
| Layer 1 | Conversation |
| Layer 2 | Session |
| Layer 3 | Long-term |

The Executive AI decides which layer to use.

---

## Shared Memory

Agents never create private memories.

All long-term memory belongs to **LifeOS**.

This avoids conflicting knowledge.

---

## Agent Contracts

Every agent receives:

- Objective
- Relevant context
- Constraints
- Expected output schema
- Timeout

Nothing else.

---

## Output Format

Every agent returns structured JSON — never Markdown:

- Summary
- Reasoning
- Confidence
- Suggested actions
- Relevant entities
- Follow-up questions

---

## Result Merger

Executive AI combines multiple outputs.

- Removes duplicates
- Resolves conflicts
- Creates one coherent answer

The user never sees individual agent responses.

---

## Conflict Resolution

**Example:**

- Planner says: work today
- Health says: rest today

Executive AI evaluates:

- Deadline
- Stress
- Sleep
- Importance

Then produces a balanced recommendation.

---

## Tool Access

Agents never access databases directly.

Agents call tools.

**Examples:**

- Search tool
- Calendar tool
- Task tool
- Knowledge tool
- Memory tool
- Analytics tool
- Notification tool

This creates a secure boundary.

---

## Tool Execution

```text
Agent
 → Tool Request
 → Permission Check
 → Execute
 → Result
 → Agent
 → Executive AI
```

---

## Permissions

| Operation | Rule |
|---|---|
| Read | Automatic |
| Write | Require confirmation |

**Always ask for:**

- Delete project
- Create reminder
- Reschedule calendar

---

## Model Routing

Executive AI selects models.

| Work | Prefer |
|---|---|
| Planning | Claude Opus |
| Fast responses | GPT mini |
| Summaries | Gemini Flash |
| Coding | Claude · GPT |

**Future:** Automatic benchmarking.

---

## Failure Recovery

```text
Agent fails
 → Retry
 → Fallback model
 → Partial response
 → Graceful explanation
```

Never crash the conversation.

---

## Timeouts

Every agent has a maximum execution time.

Avoid waiting forever.

Late responses are ignored.

---

## Token Optimization

- Reuse retrieved context
- Never duplicate prompts
- Cache summaries
- Compress memory
- Retrieve only relevant entities

---

## Observability

Track:

- Latency
- Model
- Cost
- Tokens
- Failures
- Retries
- Tool usage
- Confidence

Without storing user prompts unnecessarily.

---

## Future Extensions

- MCP servers
- Browser automation
- Email
- GitHub
- Google Drive
- WhatsApp
- Wearables
- Smart home

Everything plugs into the **Tool Engine**, not directly into agents.

---

## Golden Rule

Agents are specialists.

The Executive AI is responsible.

The user should always feel they are working with **one intelligent operating system**, not ten separate chatbots.
