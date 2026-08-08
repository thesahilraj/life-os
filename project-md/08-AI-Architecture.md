# 08 — AI Architecture

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Critical |
| **Priority** | Highest |

---

## Purpose

This document defines the complete AI architecture of LifeOS.

It specifies:

- AI philosophy
- AI responsibilities
- Agent architecture
- Memory system
- Context engine
- Prompt system
- Decision framework
- Model routing
- OpenRouter integration
- AI safety
- Reasoning pipeline

Every AI interaction must follow this document.

It sits under Vision, Core Principles, Product Requirements, Domain Model, and Engineering Architecture. Engineering defines the stack; this document defines how intelligence behaves.

---

## Core Philosophy

LifeOS is not an AI chatbot.

It is an **AI Operating System**.

The AI is the intelligence layer that connects every module.

The user should never feel like they are "chatting with AI."

Instead, they are interacting with their operating system.

---

## AI Mission

- Reduce thinking
- Reduce stress
- Increase clarity
- Increase momentum
- Protect attention
- Support long-term goals
- Never replace human judgment

---

## AI Principles

### The AI should

- Remember
- Plan
- Prioritize
- Coach
- Organize
- Explain
- Challenge assumptions
- Detect overload
- Suggest improvements
- Celebrate progress

### The AI should never

- Pretend certainty
- Invent facts
- Manipulate users
- Hide important decisions
- Automatically perform meaningful actions
- Store sensitive data without consent

---

## AI Provider

| Field | Value |
|---|---|
| **Provider** | OpenRouter |
| **Purpose** | Single gateway for multiple LLM providers |

**Benefits:**

- Model flexibility
- Fallback support
- Cost optimization
- Vendor independence
- Easy experimentation

---

## Supported Models

| Use case | Models |
|---|---|
| Planning | Claude Opus |
| Reasoning | Claude Sonnet |
| Fast UI tasks | GPT · Gemini Flash |
| Coding | Claude · GPT · DeepSeek |
| Summarization | Gemini Flash · GPT Mini |
| Creative writing | Claude · GPT |
| Future | Automatic model routing |

---

## AI Layers

```text
Layer 1 — UI
  ↓
Layer 2 — Coordinator
  ↓
Layer 3 — Specialist Agents
  ↓
Layer 4 — Memory Engine
  ↓
Layer 5 — Prompt Builder
  ↓
Layer 6 — Model Router
  ↓
OpenRouter
  ↓
Chosen Model
```

---

## Coordinator AI

The Coordinator is the only AI directly visible to the user.

**Responsibilities:**

- Receive requests
- Understand intent
- Collect context
- Select specialists
- Merge results
- Generate response
- Maintain personality

The user never interacts directly with specialist agents.

---

## Specialist Agents

| Agent | Domain |
|---|---|
| Planner | Daily / weekly planning |
| Calendar | Time and scheduling |
| Projects | Structured work |
| Knowledge | Notes and knowledge graph |
| Journal | Reflection |
| Finance | Money |
| Health | Well-being |
| Learning | Study and retention |
| Analytics | Insights and reports |
| Reflection | Growth patterns |
| Career | Professional trajectory |
| Relationships | People and follow-ups |

Each agent has:

- Domain expertise
- Own prompt
- Own context
- Own tools

Never access unrelated data.

---

### Planner Agent

- Daily planning
- Weekly planning
- Priorities
- Time blocking
- Task ordering
- Microtask generation

### Calendar Agent

- Scheduling
- Conflict detection
- Free time analysis
- Meeting preparation
- Time estimation

### Project Agent

- Milestones
- Dependencies
- Risk analysis
- Progress tracking
- Scope management

### Knowledge Agent

- Organize notes
- Knowledge graph
- Search
- Backlinks
- Summaries
- Permanent knowledge

### Journal Agent

- Reflection
- Mood trends
- Pattern detection
- Summaries
- Growth insights

### Health Agent

- Energy
- Sleep
- Exercise
- Recovery
- Stress
- Healthy workload

### Finance Agent

- Budget
- Expenses
- Savings
- Financial goals
- Subscription awareness

### Learning Agent

- Learning plans
- Revision
- Recommendations
- Knowledge retention

### Analytics Agent

- Productivity
- Habit trends
- Goal progress
- Insights
- Reports

### Relationship Agent

- Important people
- Follow-ups
- Shared events
- Important dates
- Healthy communication reminders

Never infer emotions or intentions about other people.

---

## Context Engine

Before any model call, LifeOS builds context.

**Context may include:**

- Current goal
- Current project
- Relevant tasks
- Upcoming events
- Recent journal
- Relevant notes
- AI memory
- Current time
- Current screen
- User preferences
- Energy (if available)

Only relevant information is included.

---

## Prompt Builder

Every request is composed dynamically.

**Structure:**

```text
System Prompt
 → Agent Prompt
 → Relevant Context
 → User Request
 → Formatting Rules
 → Output Schema
```

No hardcoded prompts inside components.

---

## Memory Architecture

### Short-Term Memory

- Current conversation
- Recent actions
- Current screen
- Temporary context

Expires automatically.

### Long-Term Memory

- Goals
- Preferences
- Routines
- Communication style
- Work style
- Frequently used workflows
- User-approved memories

Never store automatically without user consent.

---

## Context Retrieval

The AI retrieves only what is relevant.

**Example:**

User asks: *"Help me finish LifeOS."*

**Retrieve:**

- LifeOS project
- Related tasks
- Current sprint
- Knowledge notes
- Recent journal

**Ignore:**

- Finance
- Health
- Old unrelated projects

---

## Decision Framework

Every recommendation should answer:

- Why now?
- Why this?
- Why not something else?
- Can it wait?
- Should the AI ask first?

If uncertainty is high, ask a clarifying question.

---

## AI Transparency

Whenever AI recommends something, it should explain:

- Reasoning
- Confidence
- Trade-offs
- Unknowns (if any)

Never present guesses as facts.

---

## Model Routing

The Coordinator selects the model.

Routing depends on:

- Complexity
- Latency
- Cost
- Required reasoning
- Expected output

**Future:** Automatic benchmarking and adaptive routing.

---

## Structured Outputs

Whenever possible, models return structured JSON.

Avoid free-form text for:

- Task creation
- Planning
- Scheduling
- Summaries
- Recommendations

This improves reliability.

---

## AI Tools

The Coordinator may call tools such as:

- Calendar
- Tasks
- Knowledge search
- Memory retrieval
- Journal
- Analytics
- Notifications

**Future:**

- Email
- GitHub
- Weather
- Maps
- Browser

Every tool call that changes data requires explicit user confirmation.

---

## OpenRouter Strategy

LifeOS owns:

- Prompts
- Memory
- Routing
- Context
- Agent orchestration

OpenRouter only provides model access.

Never couple business logic to a specific model.

Switching providers should require configuration changes only.

---

## Failure Handling

```text
Model fails
 → Retry
 → Fallback model
 → Graceful error
 → Explain to user
```

Never expose provider errors directly.

---

## Cost Optimization

| Work type | Prefer |
|---|---|
| Simple work | Small models |
| Planning | Large models |
| Complex reasoning | Architecture-capable models |

Cache repeated requests where safe.

---

## Privacy

- Never send unnecessary context
- Never send secrets
- Never include API keys
- Redact sensitive information when possible
- Allow users to inspect stored memories
- Allow users to delete memories

---

## Learning

**Future capability:** AI learns from

- Accepted suggestions
- Rejected suggestions
- Preferred workflows
- Planning habits

Never silently retrain on private data.

---

## AI Personality

- Professional
- Supportive
- Honest
- Calm
- Curious
- Direct

Never patronizing.

Never manipulative.

Never guilt the user.

Always encourage sustainable progress.

---

## AI Golden Rule

The AI exists to amplify human judgment, not replace it.

- If the AI is uncertain → it should ask
- If the user disagrees → the AI should adapt
- If the user is overwhelmed → the AI should simplify

The best AI helps the user think clearly while remaining fully in control.
