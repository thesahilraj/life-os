# 12 — Database Architecture

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Critical |
| **Priority** | Highest |

---

## Purpose

This document defines the complete data architecture of LifeOS.

It specifies:

- Database philosophy
- MySQL design
- Prisma strategy
- Entity relationships
- Indexing
- Search
- AI memory
- Event storage
- Audit system
- Performance
- Migration strategy

This document is the blueprint for every table, relation, and query.

It sits under Domain Model, Engineering Architecture, and Event-Driven Architecture. Domain entities define *what*; events define *history*; this document defines *how data is stored*.

---

## Database Philosophy

The database exists to answer three questions:

1. What exists?
2. What happened?
3. What does AI need to know?

| Concern | Storage |
|---|---|
| Current state | Entities |
| History | Events |
| Long-term understanding | AI memory |

---

## Storage Architecture

```text
                    LifeOS
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
     MySQL         Event Log      AI Memory
        │              │              │
        ▼              ▼              ▼
    Prisma ORM     Activity Feed   Context Engine
        │
        ▼
   Search Index
        │
        ▼ (future)
   Embeddings → Semantic Search
```

---

## Primary Database

| Setting | Value |
|---|---|
| Engine | MySQL 8+ |
| Character set | `utf8mb4` |
| Collation | `utf8mb4_unicode_ci` |
| Timezone | UTC |
| Storage engine | InnoDB |

---

## ORM

**Prisma**

**Rules:**

- Strict schema
- Named relations
- No raw SQL unless justified
- Migrations committed to Git
- Generated client only

---

## ID Strategy

Every table uses **UUID v7**.

Never auto-increment IDs.

**Benefits:**

- Globally unique
- Better distributed indexing
- Future sync support

---

## Timestamp Strategy

Every table includes:

- `createdAt`
- `updatedAt`
- `deletedAt` (nullable)

**Optional:**

- `completedAt`
- `archivedAt`
- `reviewedAt`

Always UTC.

---

## Ownership

Every business table includes `userId`.

LifeOS is single-user today, but ownership remains explicit.

This enables future expansion.

---

## Soft Delete

| State | Behavior |
|---|---|
| Default | `deletedAt = NULL` |
| Deletion | Set `deletedAt` |

Never physically delete user data automatically.

---

## Core Tables

- `User`
- `LifeArea`
- `Goal`
- `Project`
- `Task`
- `Subtask`
- `Habit`
- `CalendarEvent`
- `JournalEntry`
- `Note`
- `KnowledgeItem`
- `LearningItem`
- `FinanceRecord`
- `HealthRecord`
- `Notification`
- `AIMemory`
- `AIConversation`
- `DomainEvent`
- `AnalyticsSnapshot`
- `Settings`

---

## Relationship Rules

```text
One User
 └── Many Life Areas
     └── Many Goals
         └── Many Projects
             └── Many Tasks
                 └── Many Subtasks
```

Additional rules:

- Goals may have many Habits
- Projects may have many Notes
- Tasks may have many Journal references
- Calendar Events may reference Tasks
- Knowledge may reference almost everything

---

## Junction Tables

- `GoalProject`
- `GoalHabit`
- `TaskKnowledge`
- `ProjectKnowledge`
- `JournalTask`
- `JournalGoal`
- `KnowledgeTag`
- `LearningKnowledge`

Avoid storing arrays in relational columns.

---

## Normalization

**Target:** Third Normal Form (3NF)

Duplicate data only when performance requires it.

Document every denormalization.

---

## Index Strategy

Every table indexes:

- Primary key
- User ID
- `createdAt`
- `updatedAt`
- Status
- Foreign keys

**Additional indexes as needed:**

- Deadline
- Priority
- Event type
- Search fields

---

## Full-Text Search

**Supported entities:**

- Tasks
- Projects
- Goals
- Notes
- Knowledge
- Journal

**Implementation:** MySQL Full-Text initially.

**Future:**

```text
Hybrid Search → Embeddings → Semantic Ranking
```

---

## AI Memory Tables

### AIMemory

**Fields:**

- ID
- User
- Type
- Content
- Importance
- Confidence
- Source
- `createdAt`
- `updatedAt`
- Consent status
- Status

**Relationships:**

- Referenced entity
- Referenced entity ID
- Embedding ID (future)

---

## Conversation Tables

- `Conversation`
- `ConversationMessage`

**Tracked fields:**

- Model
- Provider
- Prompt tokens
- Completion tokens
- Latency
- Cost
- Context version
- Referenced entities

**Purpose:** Transparency · Debugging · Future analytics

---

## Domain Events Table

Stores immutable events.

**Fields:**

- ID
- Event type
- Entity
- Entity ID
- User ID
- Metadata
- Correlation ID
- Version
- Timestamp

**Indexed by:**

- Timestamp
- Event type
- Entity ID
- Correlation ID

---

## Analytics Tables

- `DailySnapshot`
- `WeeklySnapshot`
- `MonthlySnapshot`
- Productivity score
- Habit score
- Goal score
- Focus score
- Energy score

These are **derived**.

Never manually edited.

---

## Search Tables

**Future:**

- `SearchDocument`
- `Embedding`
- `KeywordIndex`
- `Backlinks`

Used by AI.

---

## Audit Strategy

Every update records:

- Who
- When
- What changed
- Previous value (optional)
- Reason

---

## Attachments

**Future:**

- Attachment
- File
- Image
- PDF
- Voice
- Video

Store metadata only.

Files live in object storage.

---

## Transactions

Use transactions whenever multiple related writes occur.

**Example:**

```text
Create Project
 → Create Default Milestones
 → Emit Event
 → Commit
```

---

## Query Strategy

- Always paginate
- Never return unlimited rows
- Prefer cursor pagination
- Avoid `OFFSET` for large datasets

---

## N+1 Prevention

- Use Prisma `include` / `select` carefully
- Load only required fields
- Avoid nested loading without limits

---

## Caching

| Level | Technology |
|---|---|
| Level 1 | React Query |
| Level 2 | Server cache |
| Future | Redis |

Never cache private writes.

---

## Migration Strategy

Every migration is:

- Reviewed
- Versioned
- Rollback tested
- Committed

Never edit old migrations.

---

## Backup Strategy

- Daily backups
- Point-in-time recovery
- Encrypted storage
- Periodic restore testing

---

## Future Multi-Device Sync

Database design already supports:

- Conflict detection
- Version numbers
- Sync timestamps
- Offline reconciliation

---

## AI Optimization

Database should make it easy to answer:

- "What changed today?"
- "What is overdue?"
- "What goal is stalled?"
- "What habit is declining?"
- "What project needs attention?"

Without expensive joins.

---

## Security

- Parameterized queries
- Prisma only
- Least-privilege database user
- Encrypted secrets
- No credentials in code
- Regular backups

---

## Performance Targets

| Query type | Target |
|---|---|
| Simple query | < 10 ms |
| Dashboard query | < 100 ms |
| Global search | < 100 ms |
| Task list | < 50 ms |
| AI context retrieval | < 200 ms |

---

## Database Conventions

| Layer | Convention |
|---|---|
| Prisma models | PascalCase |
| MySQL tables | snake_case |
| Prisma columns | camelCase |
| MySQL columns | snake_case |
| Enums | Centralized — no magic strings |

---

## Golden Rule

The database should optimize for clarity, consistency, and future evolution — not cleverness.

If an engineer can understand the schema in one sitting, the architecture is successful.
