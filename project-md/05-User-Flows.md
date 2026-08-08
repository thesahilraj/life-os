# 05 — User Flows

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Critical |

---

## Purpose

Define every major interaction between the user and LifeOS.

This document focuses on **experiences**.

- Not pages
- Not APIs
- Not implementation

It sits under Vision, Core Principles, Product Requirements, and Information Architecture. Flows must honor those documents.

---

## UX Philosophy

LifeOS should never feel like software.

It should feel like an intelligent companion.

The user should never wonder:

> "What should I open?"

LifeOS always knows.

---

## Core User Journey

```text
Wake Up
 → Open LifeOS
 → Understand Today
 → Plan
 → Execute
 → Reflect
 → Improve
 → Sleep
 → Repeat
```

---

## Primary Daily Flow

```text
Morning
 → AI Briefing
 → Today's Plan
 → Deep Work
 → Meetings
 → Quick Capture
 → Review
 → Tomorrow Planning
```

---

## Morning Flow

### Goal

Remove uncertainty.

When the user opens LifeOS, they should immediately know:

- What matters today
- What can wait
- How much time exists
- What AI recommends

### Screen: Dashboard

**Displays:**

- Greeting
- Energy
- Mood
- Calendar
- Top 3 priorities
- XP
- Level
- Focus recommendation
- Habit reminder
- Quick Start button

### AI Briefing

**Example:**

> Good morning.
>
> You have:
> - 2 meetings
> - 1 assignment due tomorrow
> - Startup work estimated at 2 hours
> - You slept 7h 20m
>
> **Recommendation:** Finish client work before 1 PM.

### Possible Actions

- Start Focus Session
- Reschedule
- Capture Thought
- Review Calendar
- Skip Planning

---

## Planning Flow

The user selects **Plan My Day**.

AI asks:

> How are you feeling?

**Choices:**

- Focused
- Average
- Low Energy
- Stressed

AI adjusts planning accordingly.

### Planning Engine

**Inputs:**

- Calendar
- Deadlines
- Energy
- Habits
- Goals
- Project priorities
- Time estimates

**Outputs:**

- Top 3 priorities
- Suggested schedule
- Breaks
- Focus blocks

### Planning Rules

- Never exceed available time
- Never overload
- Respect meetings
- Group similar work
- Reduce context switching

---

## Deep Work Flow

User starts a **Focus Session**.

Screen changes. Distractions removed.

**Only shows:**

- Task
- Timer
- Notes
- Progress
- Music
- AI check-in

### During Focus

- Quick notes
- Quick questions
- Break reminder
- Task completion
- Mood update

### Completion

- Celebrate
- Award XP
- Suggest next task
- Or suggest break

---

## Quick Capture Flow

**Shortcut:** `Ctrl + K`  
**Or:** Floating button

User types:

> "Call dentist tomorrow."

AI understands:

- Task
- Tomorrow
- Reminder
- Health area

Creates instantly.

No forms. No extra steps.

### Quick Capture Supports

- Task
- Goal
- Project
- Idea
- Journal
- Expense
- Reminder
- Bookmark
- Question
- Voice note

---

## Project Flow

User opens a project.

Dashboard shows:

- Progress
- Milestones
- Upcoming tasks
- Risks
- AI insights
- Knowledge
- Recent activity
- Calendar

### AI Suggestions

> You're blocked.
>
> Would you like me to break this task into smaller steps?

---

## Calendar Flow

User opens Calendar.

LifeOS shows:

- Meetings
- Tasks
- Habits
- Deadlines
- Energy
- Free time
- AI suggestions

**Example:**

> Move workout to evening.
>
> Morning has two important meetings.

---

## Habit Flow

```text
Daily habit appears
 → Complete
 → Animation
 → XP
 → Streak
 → Encouragement
```

Never punish missed habits.

Simply continue.

---

## Journal Flow

### Morning

Intentions.

### Evening

Reflection.

**Questions:**

- What went well?
- What was difficult?
- What should improve tomorrow?

AI generates:

- Summary
- Mood trend
- Insights
- Patterns

---

## Knowledge Flow

User captures an idea.

AI asks:

> Should this remain temporary, or become Permanent Knowledge?

- If temporary → store as Note
- If permanent → add to Knowledge Base

---

## Learning Flow

User selects **Learn**.

Dashboard displays:

- Courses
- Books
- Revision
- Progress
- Learning goal
- AI recommendation

**Example:**

> Continue React course.
>
> Estimated 25 minutes.

---

## Finance Flow

**Dashboard shows:**

- Today's spending
- Budget
- Subscriptions
- Savings
- Upcoming payments
- AI suggestions

**Example:**

> You've spent 70% of your food budget.

---

## Health Flow

**Dashboard shows:**

- Sleep
- Mood
- Water
- Exercise
- Stress
- Energy
- AI recommendation

**Example:**

> Low sleep detected.
>
> Reduce workload today.

---

## Weekly Review Flow

Every Sunday, AI prepares:

- Wins
- Missed goals
- Completed projects
- Habits
- Mood
- Learning
- Health
- Finance
- Recommendations

---

## Monthly Review Flow

AI generates:

- Achievements
- Progress
- Challenges
- Focus areas
- Suggested goals
- Planning adjustments

---

## Search Flow

`Ctrl + K`

User types:

- Project name
- Task
- Idea
- Question
- AI conversation

Everything searchable.

---

## Notification Flow

Notifications must answer:

- Why now?
- What action?
- Can this wait?

**Priority levels:**

| Level | Meaning |
|---|---|
| Critical | Act now |
| Important | Act today |
| Informational | Useful, not urgent |

Everything else waits.

---

## Failure Flow

User misses deadlines.

AI does **not** say:

> "You failed."

Instead:

> Let's reorganize.
>
> Would you like me to build a realistic recovery plan?

---

## Overwhelm Flow

AI detects:

- Too many overdue tasks
- High stress
- Low completion
- Multiple reschedules

LifeOS switches to **Recovery Mode**.

Displays:

- One task
- One priority
- Everything else hidden

---

## Night Flow

Dashboard asks:

> Ready to end the day?

AI summarizes:

- Today's progress
- Tomorrow's priorities
- Lessons learned
- XP earned
- Current streak
- Sleep reminder

---

## Ideal User Day

```text
Wake up
 → LifeOS Briefing
 → Plan
 → Deep Work
 → Meetings
 → Quick Capture
 → Exercise
 → Journal
 → Review
 → Sleep
```

Everything else happens naturally.

---

## UX Rule

The user should never think:

> "What do I do now?"

LifeOS should always answer that question.

- Without overwhelming
- Without interrupting
- Without controlling

Only guiding.
