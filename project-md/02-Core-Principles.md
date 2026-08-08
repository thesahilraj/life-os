# 02 — Core Principles

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Immutable |
| **Priority** | Critical |

---

## Purpose

This document defines the immutable rules that govern every decision made during the design, development, and evolution of LifeOS.

These principles override feature requests, implementation shortcuts, and design trends.

If a proposed solution violates these principles, it must be redesigned.

They sit under `01-Vision.md`. Vision defines *why*. This file defines *what must never be broken*.

---

## The Golden Rule

LifeOS is not a productivity application.

**LifeOS is an Operating System for Human Life.**

Every feature should help the user think less and live more.

---

## First Principles

### Principle 1 — Reduce Mental Load

Every interaction must reduce cognitive effort.

- Never make the user remember something the system can remember.
- Never ask the user to organize information manually if AI can infer it.

### Principle 2 — Reduce Decisions

Decision fatigue is the enemy.

The system should narrow choices instead of presenting unlimited options.

**Good example**

Today:
- Finish proposal
- Attend meeting
- Workout

**Bad example**

> You have 42 overdue tasks.

### Principle 3 — One Source of Truth

Every piece of information must have one canonical location.

Never duplicate information across modules.

- Tasks belong to Tasks.
- Events belong to Calendar.
- Goals belong to Goals.

Everything else **references** them.

### Principle 4 — AI First

AI is not a feature.

AI is the operating layer.

Every module must be AI-aware.

### Principle 5 — Human First

The user always has the final decision.

- AI may recommend.
- AI may explain.
- AI may warn.
- AI must **never** silently make meaningful changes.

---

## ADHD Principles

The interface must be designed for executive dysfunction.

- Never overwhelm.
- Never punish inconsistency.
- Always encourage restarting.
- Momentum matters more than perfection.

---

## Dashboard Principles

The dashboard answers only one question:

> **What should I do right now?**

Never turn the dashboard into an analytics page.

---

## Navigation Principles

Everything important should be reachable in three clicks or fewer.

Never hide primary actions behind complex menus.

---

## Feature Principles

Every feature must satisfy **all** of the following:

1. It reduces stress.
2. It reduces thinking.
3. It saves time.
4. It has a clear purpose.
5. It integrates naturally with existing modules.

If not, reject the feature.

---

## Simplicity

Every screen should have one primary purpose.

- Avoid multifunction pages.
- The user should immediately understand what the page is for.

---

## AI Behavior

The AI should behave like a trusted **Chief of Staff**.

It should:

- remember
- plan
- prioritize
- coach
- challenge assumptions
- identify conflicts
- detect overload
- encourage healthy pacing

It should never:

- guilt users
- pretend certainty
- invent facts
- make hidden decisions
- override user choices

---

## Automation

Automation exists to remove repetitive work.

Automation must never remove control.

Every meaningful action requires confirmation.

---

## Notifications

Notifications must earn the user's attention.

- Never notify without purpose.
- Prefer fewer, higher-value notifications.

---

## Information Architecture

LifeOS organizes information around **life domains**, not file types.

Examples:

- Career
- Health
- Learning
- Finance
- Projects
- Relationships
- Knowledge
- Journal
- Calendar
- Tasks

---

## Visual Design

Inspired by Apple.

- Minimal
- Calm
- Readable
- Whitespace is a feature
- Motion is intentional
- Avoid visual noise

---

## Performance

Performance is a feature.

- Pages should feel instant.
- Animations should never reduce responsiveness.
- Lazy load everything possible.
- Optimize continuously.

---

## Accessibility

Accessibility is mandatory.

- Keyboard-first
- Screen-reader compatible
- Accessible color contrast
- Visible focus states
- Responsive layouts
- Large touch targets

---

## Data

- Never ask twice.
- Reuse existing information.
- Infer context when safe.
- Avoid duplicate data entry.

---

## Error Handling

Errors should explain:

1. What happened
2. Why it happened
3. How to fix it

Never expose raw stack traces to users.

---

## Security

Privacy first.

- Store the minimum required data.
- Encrypt sensitive information.
- Validate every input.
- Never trust client-side data.

---

## Memory

AI memory should be intentional.

**Remember:**

- Goals
- Preferences
- Recurring routines
- Work style
- Learning style

**Never remember:**

- Passwords
- Financial credentials
- Sensitive personal information without explicit consent

---

## Gamification

Gamification should reinforce progress.

- Never manipulate users.
- Reward consistency.
- Reward learning.
- Reward healthy habits.
- Avoid addictive mechanics.

---

## Development Principles

- Write production-ready code from the beginning.
- Avoid technical debt.
- Avoid shortcuts.
- Prefer maintainability over cleverness.

---

## Architecture Principles

- Modular
- Scalable
- Reusable
- Loosely coupled
- Strongly typed
- Testable
- Observable

---

## Code Quality

- No duplicated logic
- No hardcoded values
- Strict TypeScript
- Reusable components
- Clear naming
- Comprehensive validation
- Predictable APIs

---

## Definition of Done

A feature is complete only if:

- [ ] UX reviewed
- [ ] Responsive
- [ ] Accessible
- [ ] Secure
- [ ] Tested
- [ ] Documented
- [ ] Typed
- [ ] Error handling complete
- [ ] Loading states included
- [ ] Empty states included
- [ ] AI integration complete
- [ ] Analytics integrated (where appropriate)

---

## Rule for Every Future Decision

Ask these questions:

1. Does this reduce mental load?
2. Does this reduce friction?
3. Does this reduce decision fatigue?
4. Does this make LifeOS feel more like an operating system?

If any answer is **No**, redesign the solution.

---

## Closing Statement

LifeOS should not become the application with the most features.

It should become the application the user trusts the most.

When in doubt:

- Choose clarity over complexity.
- Choose calm over excitement.
- Choose usefulness over novelty.
- Choose long-term maintainability over short-term speed.
