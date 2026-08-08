# 11 — Event-Driven Architecture

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Critical |
| **Priority** | Highest |

---

## Purpose

This document defines the event system of LifeOS.

Every meaningful action inside LifeOS creates an immutable event.

Events are **not** the source of truth.

**MySQL remains the source of truth.**

Events describe what happened.

This document sits under Domain Model and Engineering Architecture. Domain entities define current state; events define history and derived side effects.

---

## Philosophy

Data stores the current state.

Events store history.

**Example:**

Task status = Completed

This tells us current state — but not:

- When?
- Why?
- How long?
- Was it rescheduled?
- Was AI involved?

Events answer those questions.

---

## Architecture

```text
            User
             │
             ▼
      Domain Entity
             │
             ▼
       Domain Event
             │
     ┌───────┼───────┐
     ▼       ▼       ▼
 Analytics   AI   Notifications
     ▼       ▼       ▼
Gamification Timeline Weekly Review
```

---

## Event Lifecycle

```text
Action
 → Validate
 → Database Update
 → Emit Event
 → Event Bus
 → Subscribers
 → Side Effects
```

Database always succeeds first.

Events never modify business data.

---

## Event Format

Every event contains:

- Event ID
- Event type
- Entity
- Entity ID
- Timestamp
- User ID
- Source
- Metadata
- Version
- Correlation ID

**Example:**

| Field | Value |
|---|---|
| Event type | `TaskCompleted` |
| Entity | Task |
| Entity ID | UUID |
| Timestamp | 2026-08-08 |
| Source | System |
| Metadata | `{}` |
| Version | v1 |
| Correlation ID | `abc123` |

---

## Event Categories

- Task events
- Project events
- Goal events
- Calendar events
- Habit events
- Journal events
- Knowledge events
- Finance events
- Health events
- AI events
- System events

---

### Task Events

- `TaskCreated`
- `TaskUpdated`
- `TaskCompleted`
- `TaskDeleted`
- `TaskArchived`
- `TaskRescheduled`
- `TaskStarted`
- `TaskPaused`
- `TaskEstimated`
- `TaskSplit`

### Project Events

- `ProjectCreated`
- `ProjectCompleted`
- `ProjectArchived`
- `MilestoneReached`
- `RiskDetected`
- `ProjectDelayed`
- `ProjectUpdated`

### Goal Events

- `GoalCreated`
- `GoalCompleted`
- `GoalPaused`
- `GoalArchived`
- `GoalDeadlineChanged`
- `ProgressUpdated`

### Habit Events

- `HabitCreated`
- `HabitCompleted`
- `HabitSkipped`
- `HabitBroken`
- `HabitArchived`
- `StreakUpdated`

### Calendar Events

- `MeetingCreated`
- `MeetingUpdated`
- `MeetingDeleted`
- `TimeBlockCreated`
- `ConflictDetected`
- `CalendarSynced`

### Journal Events

- `MorningJournal`
- `EveningJournal`
- `WeeklyReflection`
- `MonthlyReflection`
- `MoodChanged`
- `JournalCreated`

### Knowledge Events

- `NoteCreated`
- `KnowledgeCreated`
- `KnowledgeLinked`
- `KnowledgeSearched`
- `BookmarkSaved`

### Finance Events

- `ExpenseAdded`
- `IncomeAdded`
- `BudgetExceeded`
- `SubscriptionRenewed`
- `GoalReached`

### Health Events

- `WorkoutCompleted`
- `SleepLogged`
- `WaterLogged`
- `MoodLogged`
- `StressDetected`

### AI Events

- `PlanningGenerated`
- `TaskSuggested`
- `MemoryStored`
- `MemoryForgotten`
- `InsightGenerated`
- `RecommendationAccepted`
- `RecommendationRejected`

### System Events

- `Login`
- `Logout`
- `BackupCreated`
- `SyncCompleted`
- `ImportFinished`
- `SettingsChanged`

---

## Event Bus

Every event is published once.

Subscribers decide whether they care.

No direct coupling.

---

## Subscribers

- Analytics
- Gamification
- Notifications
- AI memory
- Timeline
- Weekly review
- Achievements
- Future automations

---

## Example

```text
TaskCompleted
 → Analytics updates productivity
 → XP System adds XP
 → Achievements checks badges
 → AI updates memory
 → Timeline shows completion
 → Weekly Review adds accomplishment
```

All independently.

---

## Correlation IDs

Complex workflows generate multiple events.

**Example — Finish Project:**

```text
Finish Project
 → TaskCompleted
 → MilestoneReached
 → ProjectCompleted
 → XPGranted
 → GoalProgressUpdated
```

All share one Correlation ID.

---

## Event Ordering

Events are immutable.

- Never edit
- Never delete
- Append only

---

## Replay

**Future feature.**

Replay events to rebuild:

- Timeline
- Analytics
- Achievements
- AI insights

Never rebuild the database.

Only derived systems.

---

## Event Retention

Keep forever.

Archive old events.

Never lose history.

---

## Event Versioning

Every event has a version.

Future changes remain backward compatible.

---

## Performance

Events should publish within **10 ms**.

Subscribers execute asynchronously when possible.

Never block user interaction.

---

## Failure Handling

```text
Subscriber fails
 → Retry
 → Log
 → Continue
```

One failure must never stop others.

---

## Event Naming

Past tense.

**Examples:** `TaskCompleted` · `ProjectCreated` · `HabitSkipped`

**Never:** `CompleteTask` · `CreateProject`

---

## Event Consumers

| Consumer | Consumes |
|---|---|
| Analytics | Everything |
| Notifications | High-priority events |
| Gamification | Completion events |
| AI | Contextual events |
| Timeline | Everything |

---

## AI Benefits

Events allow AI to answer:

- "What changed this week?"
- "Why am I stressed?"
- "What did I finish?"
- "What patterns do you see?"

Without expensive database scans.

---

## Golden Rule

Entities represent **what exists**.

Events represent **what happened**.

Never confuse the two.
