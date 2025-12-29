# Glossary: TaskFlow

## Purpose
<!-- هدف این فایل -->
This document defines exact meanings of domain terms to prevent AI agents from making assumptions. All agents MUST use these definitions consistently across all code and documentation.

**Rule:** If a term is not defined here, the AI agent MUST ask for clarification before proceeding.

---

## User Types

| Term | Definition | Permissions Summary | NOT to be confused with |
|------|------------|---------------------|------------------------|
| **Guest** | Unauthenticated visitor on public pages | Can only view landing, login, signup | User, Member |
| **User** | Any authenticated person (synonym: Member) | Base permissions in their teams | Guest, Admin |
| **Member** | Authenticated user with 'member' role in a team | Create/edit own tasks, view team tasks | Admin, Owner |
| **Admin** | User with 'admin' role in a specific team | Member permissions + manage team members, delete any task | Owner (no billing) |
| **Owner** | User who created a team (exactly one per team) | Admin permissions + billing + delete team + transfer ownership | Admin |

### Important Distinctions
<!-- تمایزات مهم -->
- A **User** can be **Member** in Team A, **Admin** in Team B, and **Owner** of Team C simultaneously
- **Admin** does NOT have billing access - only **Owner** does
- **Owner** cannot be removed from team - only transferred

---

## Core Entities

### Task
<!-- تسک -->
| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| id | UUID | Yes | Unique identifier |
| title | String(255) | Yes | Task title, 1-255 chars |
| description | Text | No | Optional detailed description |
| status | Enum | Yes | One of: todo, in_progress, done |
| priority | Enum | Yes | One of: low, medium, high |
| assignee_id | UUID | No | User assigned to this task |
| created_by | UUID | Yes | User who created the task |
| team_id | UUID | Yes | Team this task belongs to |
| due_date | Date | No | Optional deadline |
| completed_at | Timestamp | No | Set when status becomes 'done' |
| created_at | Timestamp | Yes | Auto-set on creation |
| updated_at | Timestamp | Yes | Auto-updated on any change |

**What Task is NOT:**
- Does NOT contain subtasks (out of scope for MVP)
- Does NOT contain time tracking data
- Does NOT contain file attachments (use links instead)

---

### Team
<!-- تیم -->
| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| id | UUID | Yes | Unique identifier |
| name | String(100) | Yes | Team display name |
| owner_id | UUID | Yes | Reference to Owner user |
| created_at | Timestamp | Yes | Auto-set on creation |

**What Team is NOT:**
- Does NOT contain billing information directly (separate billing service later)
- Does NOT have nested sub-teams

---

### Team Membership
<!-- عضویت تیم -->
| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| team_id | UUID | Yes | Reference to Team |
| user_id | UUID | Yes | Reference to User |
| role | Enum | Yes | One of: member, admin, owner |
| joined_at | Timestamp | Yes | When user joined team |

**Constraints:**
- Each team has exactly ONE owner
- A user can have only ONE role per team
- Unique constraint on (team_id, user_id)

---

## Status Values

### Task Status
<!-- وضعیت تسک -->
| Status | Meaning | UI Display (Persian) | Can transition to |
|--------|---------|---------------------|-------------------|
| `todo` | Not started, waiting to be picked up | انجام نشده | `in_progress` |
| `in_progress` | Currently being worked on | در حال انجام | `done`, `todo` |
| `done` | Completed successfully | انجام شده | `todo` (reopen) |

**State Machine:**
```
┌──────┐     start      ┌─────────────┐    complete    ┌──────┐
│ todo │ ──────────────►│ in_progress │ ──────────────►│ done │
└──────┘                └─────────────┘                └──────┘
   ▲                          │                           │
   │         pause            │         reopen            │
   └──────────────────────────┴───────────────────────────┘
```

### Priority Values
<!-- اولویت -->
| Priority | Meaning | UI Color | Sort Order |
|----------|---------|----------|------------|
| `high` | Urgent, do first | Red (#ef4444) | 1 |
| `medium` | Normal priority | Yellow (#f59e0b) | 2 |
| `low` | Can wait | Gray (#6b7280) | 3 |

---

## Actions (Verbs)

| Action | Exact Meaning | Database Effect | Reversible? |
|--------|---------------|-----------------|-------------|
| **Create** | Insert new record | INSERT | No (but can delete) |
| **Update** | Modify existing record | UPDATE | Yes (with history) |
| **Complete** | Set status='done' + completed_at=now() | UPDATE | Yes (reopen) |
| **Reopen** | Set status='todo' + completed_at=null | UPDATE | Yes |
| **Delete** | Remove record permanently | DELETE | No |
| **Archive** | NOT USED in MVP | - | - |
| **Assign** | Set assignee_id to a user | UPDATE | Yes (unassign) |
| **Unassign** | Set assignee_id to null | UPDATE | Yes |

**Critical Distinction:**
- **Delete** = permanent removal (hard delete)
- **Archive** = NOT implemented in MVP (do not use this term)

---

## API Terms

| Term | Meaning | Example |
|------|---------|---------|
| **Endpoint** | A specific API URL path | `/api/v1/tasks` |
| **Resource** | The entity being accessed | Task, Team, User |
| **Collection** | List of resources | `/tasks` returns array |
| **Instance** | Single resource | `/tasks/:id` returns object |
| **Payload** | Request/response body | JSON data |

---

## UI Terms

| Term (English) | Persian | Meaning |
|----------------|---------|---------|
| Dashboard | داشبورد | Main page after login showing tasks |
| Sidebar | نوار کناری | Left navigation panel |
| Modal | پنجره شناور | Popup dialog for forms |
| Toast | اعلان | Temporary notification message |
| Card | کارت | Visual container for a task |
| Badge | نشان | Small label (e.g., priority indicator) |

---

## Forbidden Interpretations
<!-- برداشت‌های ممنوع - AI نباید این اشتباهات رو بکنه -->

| ❌ Wrong Interpretation | ✅ Correct Interpretation |
|------------------------|--------------------------|
| "User" means any person | "User" means authenticated member only |
| "Delete" means hide from view | "Delete" means permanent removal |
| "Admin" has all permissions | "Admin" cannot access billing |
| "Task" includes subtasks | "Task" is atomic, no subtasks |
| "Team" can have sub-teams | "Team" is flat, no hierarchy |
| "Complete" just changes status | "Complete" sets status AND completed_at |
| Empty assignee means unassigned | Empty assignee_id (null) means unassigned |

---

## Abbreviations

| Abbr | Full Form | Usage |
|------|-----------|-------|
| UC | Use Case | UC-001, UC-002, ... |
| FR | Functional Requirement | FR-001, FR-002, ... |
| MVP | Minimum Viable Product | First release scope |
| API | Application Programming Interface | Backend endpoints |
| UI | User Interface | Frontend screens |
| DB | Database | PostgreSQL storage |
| JWT | JSON Web Token | Authentication token |
| RTL | Right-to-Left | Persian text direction |

---

## Version History
<!-- تاریخچه تغییرات -->
| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2024-02-01 | Initial glossary for MVP |
