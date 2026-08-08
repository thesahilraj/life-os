# 13 — Frontend Architecture

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Critical |
| **Priority** | Highest |

---

## Purpose

This document defines the frontend architecture of LifeOS.

It specifies:

- Project structure
- UI system
- Component architecture
- Navigation
- State management
- Dashboard
- Animations
- Accessibility
- Responsive design
- Performance

This is the source of truth for every frontend decision.

It sits under Engineering Architecture, User Flows, and Core Principles. Engineering defines the stack; this document defines how the UI is structured and experienced.

---

## Frontend Philosophy

The frontend should feel:

- Calm
- Fast
- Predictable
- Minimal

AI should enhance the experience, not dominate it.

The interface should reduce thinking, not increase it.

---

## Design Inspiration

- Apple
- Linear
- Raycast
- Arc Browser
- Notion
- Superhuman
- Things 3

None should be copied directly.

Only adopt proven interaction patterns.

---

## Technology Stack

| Concern | Choice |
|---|---|
| Framework | Next.js 15 (App Router) |
| Language | TypeScript (strict) |
| Styling | Tailwind CSS v4 |
| Component library | shadcn/ui |
| Animation | Motion |
| Forms | React Hook Form |
| Validation | Zod |
| Data fetching | TanStack Query |
| UI state | Zustand |
| Theme | next-themes |
| Icons | Lucide |
| Charts | Recharts |
| Command palette | cmdk |
| Accessibility | React Aria (where required) |

---

## Project Structure

```text
src/
├── app/
├── features/
│   ├── dashboard/
│   ├── tasks/
│   ├── projects/
│   ├── goals/
│   ├── journal/
│   ├── calendar/
│   ├── habits/
│   ├── finance/
│   ├── health/
│   ├── learning/
│   ├── settings/
│   └── ai/
├── components/
│   ├── ui/
│   ├── shared/
│   ├── layout/
│   └── animations/
├── hooks/
├── store/
├── providers/
├── styles/
├── lib/
├── utils/
└── types/
```

---

## Route Structure

| Route | Surface |
|---|---|
| `/` | Dashboard |
| `/tasks` | Tasks |
| `/projects` | Projects |
| `/goals` | Goals |
| `/calendar` | Calendar |
| `/journal` | Journal |
| `/habits` | Habits |
| `/knowledge` | Knowledge |
| `/learning` | Learning |
| `/finance` | Finance |
| `/health` | Health |
| `/analytics` | Analytics |
| `/settings` | Settings |
| `/search` | Search |
| `/ai` | AI |

---

## Layout Hierarchy

```text
App
 └─ Sidebar
     └─ Topbar
         └─ Page
             └─ Widgets
                 └─ Components
```

---

## Navigation

| Layer | Mechanism |
|---|---|
| Primary | Sidebar |
| Secondary | Breadcrumbs |
| Context | Tabs |
| Quick | Command palette |

---

## Sidebar

Always visible on desktop.

Collapsible.

Icons + labels.

**Contains:**

- Dashboard
- Tasks
- Projects
- Goals
- Calendar
- Habits
- Journal
- Knowledge
- Learning
- Finance
- Health
- Analytics
- Settings
- AI

---

## Topbar

Contains:

- Search
- Quick Capture
- Notifications
- AI status
- Profile
- Theme switch
- Command palette

---

## Dashboard

**Purpose:** Answer one question —

> What should I do right now?

**Contains:**

- AI brief
- Today's priorities
- Upcoming calendar
- Habits
- Focus timer
- XP
- Level
- Recent activity
- Quick Capture

---

## Component Hierarchy

```text
Page
 └─ Feature Container
     └─ Section
         └─ Widget
             └─ Card
                 └─ Primitive
```

Never skip layers unnecessarily.

---

## Component Rules

- One responsibility per component
- Maximum ~250 lines per component where practical
- Separate business logic
- Avoid deeply nested props
- Favor composition

---

## Shared Components

- Button
- Card
- Dialog
- Drawer
- Sheet
- Popover
- Tooltip
- Badge
- Avatar
- Tabs
- Command
- Table
- Calendar
- Chart
- Progress
- Empty State
- Skeleton

---

## AI Panel

Persistent but unobtrusive.

**Can:**

- Chat
- Plan
- Search
- Summarize
- Create
- Review

Should understand current page context.

---

## Command Palette

**Shortcut:** `Ctrl + K`

**Supports:**

- Navigation
- Search
- Quick actions
- AI commands
- Recent items
- Tool execution
- Natural language

**Example:** `"Create task tomorrow 3 PM"`

---

## Global Search

Unified search across:

- Tasks
- Projects
- Goals
- Notes
- Knowledge
- Calendar
- Journal
- AI conversations
- Settings

**Future:** Semantic search

---

## State Management

```text
React State
 → Context
 → TanStack Query
 → Zustand
```

Never use global state for server data.

---

## Forms

React Hook Form + Zod.

**Validation:**

```text
Client → Server
```

Same schema.

---

## Loading Strategy

Every page has:

- Skeleton
- Optimistic UI
- Progressive loading
- Streaming where useful

---

## Empty States

Every module includes:

- Explanation
- Primary action
- Helpful illustration
- AI suggestion

---

## Error States

Human-readable.

Explain:

- What happened
- How to recover

Offer retry.

Never expose stack traces.

---

## Theme

- Light
- Dark
- System

**Future:** Dynamic accent colors

---

## Design Tokens

Centralized — no magic values:

- Spacing
- Radius
- Typography
- Elevation
- Animation
- Opacity

---

## Typography

Readable. Consistent.

**Hierarchy:**

- Display
- Heading
- Title
- Body
- Caption
- Mono

---

## Grid System

| Breakpoint | Columns |
|---|---|
| Desktop | 12 |
| Tablet | 8 |
| Mobile | 4 |

Responsive by default.

---

## Animations

Motion should communicate, not decorate.

**Use for:**

- Transitions
- Expansion
- Success
- Context changes

Avoid excessive motion.

Respect reduced-motion preferences.

---

## Accessibility

Required for every feature:

- WCAG AA
- Keyboard navigation
- Visible focus
- Screen reader support
- High contrast
- Reduced motion

---

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + K` | Command palette |
| `N` | New task |
| `J` | Journal |
| `G` | Go to |
| `/` | Search |
| `?` | Shortcut help |
| `Esc` | Close overlays |

---

## Responsive Strategy

| Surface | Expectation |
|---|---|
| Desktop | Primary experience |
| Tablet | Fully supported |
| Mobile | PWA-friendly |

No feature loss.

---

## Performance

- Lazy loading
- Code splitting
- Streaming
- Memoization where justified
- Image optimization
- Font optimization
- Avoid unnecessary re-renders

---

## Offline UX

**Future phases:**

- View cached content
- Queue local changes
- Sync when online
- Clearly indicate sync status

---

## AI Integration

Every major page exposes to the AI Context Engine:

- Current entity
- Current context
- Selection
- Recent activity

Never manually duplicate context.

---

## Frontend Testing

- Unit tests
- Component tests
- Accessibility tests
- Visual regression
- E2E
- Performance audits

---

## Design Principles

Every screen must answer:

1. Where am I?
2. What matters now?
3. What can I do next?
4. How do I go back?

If those answers are not obvious, the design is incomplete.

---

## Golden Rule

Users should spend their time thinking about their life, not learning the interface.

The interface disappears.

The work remains.
