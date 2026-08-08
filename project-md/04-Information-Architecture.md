# 04 — Information Architecture

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Critical |

---

## Purpose

This document defines how every piece of information inside LifeOS is structured, connected, stored, and discovered.

LifeOS does **not** organize information by application.

It organizes information by **life**.

- Everything must have one logical place.
- Everything must be discoverable.
- Everything must be interconnected.

This document sits under `01-Vision.md`, `02-Core-Principles.md`, and `03-Product-Requirements.md`. UI and modules may evolve; this model should remain stable.

---

## Core Philosophy

People don't think in apps.

People think in context.

**Not this:**

- Calendar app
- Notes app
- Habit app
- Todo app

**This:**

> "I'm trying to finish my startup."

LifeOS should organize around that.

---

## Information Hierarchy

```text
Life
 └─ Life Areas
     └─ Goals
         └─ Projects
             └─ Tasks
                 └─ Subtasks
                     └─ Sessions
                         └─ Activity
```

---

## Primary Life Areas

Every piece of information belongs to at least one Life Area.

- Career
- Business
- Education
- Health
- Finance
- Relationships
- Personal Growth
- Knowledge
- Creativity
- Lifestyle
- Administration

---

## Information Pyramid

```text
User
 └─ Life Areas
     └─ Goals
         └─ Projects
             └─ Tasks
                 └─ Calendar Events
                     └─ Notes
                         └─ Journal
                             └─ Analytics
```

---

## Core Entities

The following entities exist throughout the system.

Each entity has its own module but can reference others.

### User

Represents the owner of the system.

**Contains:**

- Profile
- Preferences
- Timezone
- Theme
- AI settings
- Integrations
- Gamification
- Statistics

### Goal

Represents an outcome.

**Examples:** Graduate · Lose weight · Launch startup · Read 20 books

**Properties:**

- Title
- Description
- Priority
- Deadline
- Status
- Progress
- Life Area
- AI summary

**Relationships:**

- Projects
- Tasks
- Habits
- Journal
- Analytics

### Project

Collection of work.

**Examples:** LifeOS · XBionics · Semester 4

**Properties:**

- Status
- Timeline
- Milestones
- Risk
- Dependencies
- Related goals
- Related knowledge
- Related calendar
- Related journal

### Task

Small actionable work.

**Properties:**

- Title
- Description
- Priority
- Energy required
- Estimated time
- Deadline
- Context
- Status
- Project
- Goal
- Life Area
- AI breakdown
- Dependencies

### Subtask

Atomic work item.

Should usually be completable within **5–15 minutes**.

### Habit

Repeated behavior.

**Examples:** Workout · Read · Meditate · Drink water · Journal

**Properties:**

- Frequency
- Streak
- Completion
- Difficulty
- XP

### Calendar Event

Scheduled commitment.

**Examples:** Lecture · Meeting · Doctor · Birthday · Interview

**Properties:**

- Start
- End
- Location
- Participants
- Notes
- Linked project
- Linked goal

### Journal Entry

Reflection.

**Types:** Morning · Evening · Weekly · Monthly · Freeform

**Properties:**

- Mood
- Energy
- Reflection
- Lessons
- Wins
- Challenges
- AI summary

### Note

Knowledge in progress.

**Examples:** Research · Ideas · Bookmarks · Meeting notes · Lecture notes

**Properties:**

- Tags
- Relationships
- Backlinks
- Attachments
- AI summary

### Knowledge

Permanent information.

Unlike Notes, Knowledge is **refined**.

**Examples:** Programming concepts · Business ideas · Frameworks · Mental models

### Learning Resource

Anything that teaches.

**Types:** Books · Videos · Courses · Articles · Papers · Documentation

**Properties:**

- Progress
- Difficulty
- Time
- Tags
- Notes

### Finance Record

- Income
- Expense
- Investment
- Subscription
- Budget
- Goal

### Health Record

- Sleep
- Weight
- Exercise
- Mood
- Stress
- Medication
- Water

### AI Memory

Long-term context.

**Stores:**

- Goals
- Preferences
- Recurring routines
- Favorite workflows
- Working style
- Communication style

Never stores sensitive data automatically.

---

## Relationships

Everything connects.

```text
Goal
 └─ Projects
     └─ Tasks
         └─ Calendar
             └─ Journal
                 └─ Analytics
```

Every module enriches another.

Nothing exists alone.

---

## Navigation Hierarchy

```text
Home / Dashboard
 └─ Life Areas
     └─ Projects
         └─ Tasks
             └─ Calendar
                 └─ Knowledge
                     └─ Journal
                         └─ Analytics
                             └─ Settings
```

---

## Universal Search

Everything is searchable:

- Tasks
- Projects
- Goals
- Notes
- Journal
- Habits
- Events
- Knowledge
- AI conversations
- Settings

Search should understand natural language.

**Examples:**

- "What did I write about AI?"
- "What did I promise last week?"
- "Show unfinished startup work."

---

## Global Quick Capture

Accessible everywhere.

**Shortcut:** `Ctrl + K`  
**Or:** Quick Add button

Can instantly create:

- Task
- Note
- Idea
- Journal
- Reminder
- Project
- Goal
- AI conversation

No navigation required.

---

## AI Context Graph

The AI never sees isolated data.

Instead it sees:

```text
Goal
 └─ Project
     └─ Task
         └─ Calendar
             └─ Knowledge
                 └─ Journal
                     └─ Analytics
```

This enables contextual reasoning.

---

## Information Ownership

Every object has exactly one owner.

**Example:**

- Task belongs to Project
- Project belongs to Goal
- Goal belongs to Life Area

Avoid duplicated ownership.

---

## Data Flow

```text
Capture
 → Organize
 → Connect
 → Schedule
 → Execute
 → Reflect
 → Learn
 → Improve
 → Repeat
```

---

## Dashboard Data Sources

Dashboard never owns information.

It only aggregates.

**Sources:**

- Calendar
- Tasks
- Projects
- Habits
- AI
- Health
- Journal
- Finance
- Notifications

---

## AI Priority Order

When deciding today's work, AI considers:

1. Deadlines
2. Goal importance
3. Energy
4. Calendar
5. Habits
6. Previous progress
7. Estimated duration
8. Context switching cost
9. Burnout
10. Focus history

---

## Information Rules

Every object must have:

- ID
- Created date
- Updated date
- Status
- Owner
- Relationships
- Metadata
- Search index
- AI context

---

## Future Compatibility

Architecture must support the following without redesigning the data model:

- Voice
- Wearables
- Email
- Documents
- Browser extension
- Native mobile
- API
- Offline sync

---

## Architecture Principle

Pages may change.

Components may change.

Design may change.

**Information Architecture must remain stable.**

Everything else is built on top of this document.
