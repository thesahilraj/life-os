# 07 — Engineering Architecture

| Field | Value |
|---|---|
| **Version** | 1.0 |
| **Status** | Approved |
| **Priority** | Critical |

---

## Purpose

This document defines the engineering architecture of LifeOS.

It serves as the single source of truth for:

- Frontend architecture
- Backend architecture
- Database
- AI integration
- APIs
- Security
- Performance
- Scalability
- Deployment
- Development standards

Every implementation decision must align with this document.

It sits under Vision through Domain Model. Domain entities (`06-Domain-Model.md`) define *what* is stored; this document defines *how* the system is built.

---

## Engineering Philosophy

LifeOS is built for long-term maintainability.

**Prioritize:**

- Simplicity
- Modularity
- Predictability
- Testability
- Performance
- Developer experience

Avoid premature optimization.

Avoid unnecessary abstractions.

---

## Technology Stack

### Frontend

- Next.js 15 (App Router)
- React 19
- TypeScript (strict mode)
- Tailwind CSS v4
- shadcn/ui
- Framer Motion
- React Hook Form
- Zod
- TanStack Query
- Lucide Icons

### Backend

- Next.js Route Handlers
- Next.js Server Actions
- Prisma ORM
- MySQL 8
- Redis (optional, phase 2)

### AI

- OpenAI
- Vercel AI SDK
- Structured outputs
- Embeddings (future)
- Memory layer
- Prompt templates

### Storage

| Role | Technology |
|---|---|
| Primary | MySQL |
| Files | Cloudinary (future) |
| Local (dev) | Local storage |

---

## High-Level Architecture

```text
Browser
  │
  ▼
Next.js Frontend
  │
  ▼
Server Actions / Route Handlers
  │
  ▼
Business Services
  │
  ▼
Repositories
  │
  ▼
Prisma ORM
  │
  ▼
MySQL
```

---

## Project Structure

```text
src/
├── app/
├── actions/
├── features/
├── components/
├── services/
├── repositories/
├── lib/
├── hooks/
├── providers/
├── store/
├── utils/
├── types/
├── middleware/
├── config/
└── styles/
```

---

## Layered Architecture

### Presentation Layer

Responsible for:

- UI
- Forms
- Navigation
- Animations
- Accessibility

No business logic.

### Feature Layer

Contains:

- Dashboard
- Tasks
- Projects
- Habits
- Journal
- Finance
- Calendar
- Learning
- Knowledge

Each feature owns:

- Components
- Hooks
- Services
- Types
- Validation

### Service Layer

Contains business logic.

**Examples:** `TaskService` · `GoalService` · `PlannerService` · `CalendarService`

Never directly accesses UI.

### Repository Layer

Responsible for database communication.

Only Prisma lives here.

Never expose Prisma outside repositories.

### Infrastructure Layer

- Authentication
- Logging
- Storage
- Email
- AI
- Integrations
- Configuration

---

## State Management

Use local state whenever possible.

**Preferred order:**

```text
React State
 → Context
 → TanStack Query
 → Global Store
```

Avoid unnecessary global state.

---

## Server Actions

Use for:

- Forms
- CRUD
- Authenticated mutations
- Simple workflows

---

## Route Handlers

Use for:

- Public APIs
- Webhooks
- External integrations
- Streaming
- Background jobs

---

## Authentication

**Preferred:** Better Auth

**Requirements:**

- Google login
- Email login
- Passkeys (future)
- Session-based authentication

---

## Authorization

Single-user system.

Still implement proper authorization.

- Every query filters by user
- Never trust client IDs

---

## Validation

Every input validated using Zod.

Never trust frontend validation.

Server validates everything.

---

## Error Handling

Every request returns:

- Success, or
- Typed error

Never return raw exceptions.

---

## Logging

| Environment | Style |
|---|---|
| Development | Pretty logs |
| Production | Structured logs |

Every important event logged.

---

## Folder Rules

- Components never access the database
- Repositories never render UI
- Services never know about React

Maintain strict separation.

---

## AI Architecture

One coordinator AI.

**Specialist agents:**

- Planner
- Coach
- Knowledge
- Finance
- Health
- Learning
- Journal
- Calendar

The coordinator decides who should answer.

---

## AI Context

Every AI request includes only relevant:

- Goal
- Project
- Task
- Calendar
- Recent journal
- Relevant memory

Never send unnecessary data.

---

## AI Memory

| Horizon | Contents |
|---|---|
| Short-term | Conversation context |
| Long-term | Goals, preferences, patterns |

Memory retrieval is explicit.

---

## Search

Global search index.

**Supports:**

- Tasks
- Projects
- Notes
- Journal
- Knowledge
- Calendar

**Future:** Semantic search

---

## Performance Goals

| Surface | Target |
|---|---|
| Dashboard | < 1 second perceived |
| Search | < 100 ms |
| Navigation | Instant |

Lazy load everything possible.

---

## Caching

```text
Browser Cache
 → React Cache
 → Server Cache
 → Database
```

Never cache sensitive data.

---

## Security

- HTTPS only
- Secure cookies
- CSRF protection
- Rate limiting
- Parameterized queries
- Input validation
- Content Security Policy

---

## Database Principles

- Normalize data
- Avoid duplication
- Use UUID v7
- Soft delete
- `createdAt` / `updatedAt` / `deletedAt`
- Audit fields everywhere

---

## API Principles

- REST internally
- Consistent naming
- Version when necessary
- Typed responses
- Never expose internal implementation

---

## Background Jobs

**Future:**

- Calendar sync
- AI summaries
- Weekly review
- Analytics
- Notifications

Use queues when introduced.

---

## File Uploads

**Future:** Images · Documents · Voice notes

- Validate type and size
- Store metadata separately

---

## Notifications

- In-app
- Email (future)
- Push (future)

Never spam.

---

## Offline Strategy

| Phase | Capability |
|---|---|
| Phase 1 | Read-only cache |
| Phase 2 | Offline edits + conflict resolution |

---

## Accessibility

Mandatory:

- WCAG AA
- Keyboard-first
- Reduced motion
- Screen reader support
- Focus management

---

## Testing Strategy

- Unit tests
- Integration tests
- E2E tests
- Accessibility tests
- Performance audits

---

## Deployment

| Environment | Approach |
|---|---|
| Development | Docker Compose |
| Production | Vercel (frontend) + managed MySQL + Cloudinary |
| Ops | Monitoring |

---

## Monitoring

- Error tracking
- Performance
- API latency
- Database performance
- AI usage
- Search latency

---

## Coding Standards

- Strict TypeScript
- No `any`
- No duplicated logic
- Reusable components
- SOLID principles
- Feature-first architecture
- Document complex logic

---

## Definition of Done

Every feature must include:

- Validation
- Error states
- Loading states
- Empty states
- Responsive UI
- Accessibility
- Tests
- Documentation
- Analytics (where appropriate)
- AI integration (where appropriate)

---

## Architecture Decision Rule

Before introducing any new dependency, abstraction, or service, ask:

1. Does it simplify the system?
2. Is it maintainable?
3. Can it be removed easily?
4. Does it solve a real problem?

If not, do not add it.

---

## Closing Principle

Architecture exists to make future development easier.

If the architecture becomes more complicated than the product, the architecture has failed.
