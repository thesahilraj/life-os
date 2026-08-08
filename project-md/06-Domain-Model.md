# 06 — Domain Model

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Critical |

---

## Purpose

Define every business entity, its responsibilities, ownership, relationships, lifecycle, and invariants.

This document is the source of truth for:

- Prisma schema
- MySQL database
- API contracts
- AI context engine
- Search
- Analytics

It sits under Vision, Core Principles, Product Requirements, Information Architecture, and User Flows. Implementation must conform to this model.

---

## Philosophy

LifeOS is not page-driven.

It is **entity-driven**.

Everything revolves around entities.

The UI is simply a visualization.

---

## Entity Hierarchy

```text
User
 ├── Life Areas
 ├── Goals
 ├── Projects
 ├── Tasks
 ├── Calendar
 ├── Habits
 ├── Journal
 ├── Knowledge
 ├── Health
 ├── Finance
 └── AI Memory
```

---

## Root Entity

### User

The user owns everything.

**Responsibilities:**

- Identity
- Preferences
- Settings
- Theme
- Integrations
- AI configuration
- Statistics

**Relationships:**

```text
One User
 └── Many Goals
 └── Many Projects
 └── Many Tasks
 └── Many Notes
 └── Many Journal Entries
 └── Many Habits
 └── Many Memories
```

---

## Life Area

Represents one major area of life.

**Examples:** Career · Business · Health · Finance · Learning · Relationships · Personal · Creativity

**Properties:**

- ID
- Name
- Description
- Icon
- Color
- Order

**Contains:**

- Goals
- Projects
- Tasks
- Habits
- Knowledge
- Analytics

---

## Goal

Represents a desired outcome.

**Examples:** Graduate · Launch LifeOS · Lose weight · Read 20 books

**Lifecycle:**

```text
Draft → Active → Completed → Archived
```

**Properties:**

- ID
- Title
- Description
- Priority
- Deadline
- Progress
- Status
- Created at
- Updated at

**Relationships:**

```text
One Goal
 └── Many Projects
 └── Many Tasks
 └── Many Habits
 └── Many Journal Entries
 └── Many Notes
```

---

## Project

A structured body of work.

**Examples:** LifeOS · Semester 5 · Startup website · Hackathon

**Properties:**

- ID
- Goal
- Status
- Timeline
- Risk
- Priority
- Progress
- Estimated hours

**Relationships:**

```text
One Project
 └── Many Tasks
 └── Many Notes
 └── Many Calendar Events
 └── Many Files
```

---

## Task

The smallest schedulable unit of work.

**Properties:**

- ID
- Title
- Description
- Priority
- Energy required
- Estimated duration
- Actual duration
- Status
- Deadline
- Context

**Relationships:**

```text
Task
 └── Subtasks
 └── Calendar Event
 └── Goal
 └── Project
 └── Knowledge
 └── Journal
```

---

## Subtask

Atomic work.

**Rule:** A subtask should ideally be completable within **5–15 minutes**.

**Properties:**

- Status
- XP
- Completion time
- Parent task

---

## Calendar Event

Scheduled commitment.

**Types:** Meeting · Reminder · Lecture · Appointment · Deadline · Birthday

**Properties:**

- Start
- End
- Timezone
- Location
- Participants
- Related project
- Related task
- Related goal

---

## Habit

Recurring behavior.

**Examples:** Workout · Read · Meditate · Drink water

**Properties:**

- Frequency
- Difficulty
- Current streak
- Best streak
- Completion %
- XP

**Relationships:**

- Goal
- Journal
- Analytics

---

## Journal Entry

Reflection.

**Types:** Morning · Evening · Weekly · Monthly · Freeform

**Properties:**

- Mood
- Energy
- Reflection
- Gratitude
- Challenges
- Wins
- AI summary

**Relationships:**

- Goals
- Projects
- Tasks

---

## Note

Temporary knowledge.

**Types:** Idea · Meeting notes · Research · Bookmark · Checklist · Reference

**Properties:**

- Title
- Content
- Tags
- Attachments

**Relationships:**

- Projects
- Goals
- Knowledge

---

## Knowledge Item

Permanent information.

Unlike Notes, Knowledge should be **refined**.

**Examples:** Programming concepts · Business frameworks · Mental models · Research

**Can reference:**

- Notes
- Projects
- Learning
- Goals

---

## Learning Item

Something being studied.

**Types:** Book · Video · Article · Course · Paper · Documentation

**Properties:**

- Progress
- Estimated time
- Difficulty
- Rating
- Completion

**Relationships:**

- Knowledge
- Journal
- Goals

---

## Finance Record

Financial tracking.

**Types:** Income · Expense · Subscription · Investment · Budget · Savings

**Properties:**

- Amount
- Currency
- Category
- Payment method
- Recurring

**Relationships:**

- Financial goals
- Analytics

---

## Health Record

Track well-being.

**Types:** Sleep · Exercise · Water · Mood · Stress · Medication · Weight · Heart rate

**Relationships:**

- Habits
- Journal
- Analytics

---

## AI Memory

Long-term contextual memory.

**Stores:**

- Goals
- Preferences
- Communication style
- Favorite workflows
- Recurring patterns

**Avoid storing:**

- Passwords
- Sensitive credentials
- Private information without explicit approval

---

## AI Conversation

Conversation history.

**Stores:**

- Question
- Response
- Referenced entities
- Confidence
- Follow-ups
- Summary

---

## Notification

User attention.

**Priority levels:** Critical · High · Medium · Low

**Types:** Reminder · Deadline · AI suggestion · Calendar · Habit · System

---

## Analytics Snapshot

Historical metrics.

**Contains:**

- Productivity
- Focus
- Mood
- Learning
- Finance
- Health
- Habit completion
- Goal progress

---

## Search Index

Every searchable entity creates a search document.

**Includes:**

- Title
- Description
- Tags
- Relationships
- Embedding
- Last accessed

---

## Entity Relationships

```text
Goal
 └── Project
     └── Task
         └── Subtask

Calendar
 └── Task
     └── Journal
         └── Analytics

Knowledge
 └── Learning
     └── Projects
```

Everything is connected.

Nothing exists in isolation.

---

## Domain Rules

- A Task may belong to one Project.
- A Project may belong to one Goal.
- A Goal belongs to one Life Area.
- A Journal Entry may reference many Tasks.
- A Habit may support many Goals.
- Knowledge may reference any entity.
- Calendar Events may link to Tasks.

---

## Soft Delete

Never permanently delete by default.

Use:

- `deletedAt`
- Restore
- Archive
- Audit trail

---

## Status Standards

Allowed statuses only:

- Draft
- Active
- Paused
- Completed
- Cancelled
- Archived

No custom statuses.

---

## IDs

Every entity uses **UUID v7**.

Never integer IDs.

---

## Timestamps

All UTC:

- `createdAt`
- `updatedAt`
- `deletedAt`
- `completedAt`

---

## Audit Fields

Future-ready:

- Created by
- Updated by
- Version
- Change history

---

## Domain Events

Events that power analytics, achievements, AI insights, notifications, and future automations:

- Task Completed
- Goal Created
- Project Archived
- Habit Completed
- Journal Written
- Calendar Synced
- Finance Added
- Knowledge Created

---

## Domain Philosophy

Features come and go.

Pages change.

UI evolves.

**The Domain Model should remain stable for years.**

If the Domain Model is correct, everything else becomes significantly easier.
