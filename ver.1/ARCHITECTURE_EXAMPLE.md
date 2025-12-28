# Architecture: TaskFlow

## 1. System Overview
<!-- نمای کلی سیستم -->

```
                                    ┌─────────────────┐
                                    │   CDN (Static)  │
                                    └────────┬────────┘
                                             │
┌─────────────┐                    ┌─────────▼─────────┐
│   Client    │◄──────────────────►│   API Gateway     │
│  (PWA/Web)  │                    │   (nginx/traefik) │
└─────────────┘                    └─────────┬─────────┘
                                             │
                    ┌────────────────────────┼────────────────────────┐
                    │                        │                        │
           ┌────────▼────────┐    ┌─────────▼─────────┐    ┌─────────▼─────────┐
           │  Auth Service   │    │   Task Service    │    │ Notification Svc  │
           │   (Port 3001)   │    │   (Port 3002)     │    │   (Port 3003)     │
           └────────┬────────┘    └─────────┬─────────┘    └─────────┬─────────┘
                    │                       │                        │
           ┌────────▼────────┐    ┌─────────▼─────────┐    ┌─────────▼─────────┐
           │  PostgreSQL     │    │   PostgreSQL      │    │      Redis        │
           │  (auth_db)      │    │   (task_db)       │    │   (queue/cache)   │
           └─────────────────┘    └───────────────────┘    └───────────────────┘
```

---

## 2. Microservices

### Service: auth-service
<!-- سرویس: احراز هویت -->
- **Responsibility**: User authentication, authorization, team membership
- **Tech Stack**: Python 3.12, FastAPI
- **Database**: PostgreSQL (auth_db)
- **Exposes**: 
  - REST API: /auth/*
  - gRPC: ValidateToken, GetUserPermissions
- **Consumes**: None
- **Scaling Strategy**: 
  - Horizontal scaling behind load balancer
  - Stateless (JWT tokens)
  - Redis for session blacklist

**Key Endpoints:**
| Method | Path | Description |
|--------|------|-------------|
| POST | /auth/signup | Create new user |
| POST | /auth/login | Login, return JWT |
| POST | /auth/logout | Invalidate token |
| POST | /auth/refresh | Refresh JWT |
| GET | /auth/me | Get current user |
| POST | /auth/invite | Create team invite |
| POST | /auth/invite/accept | Accept invite |

---

### Service: task-service
<!-- سرویس: مدیریت تسک‌ها -->
- **Responsibility**: Task CRUD, team management, task queries
- **Tech Stack**: Python 3.12, FastAPI
- **Database**: PostgreSQL (task_db)
- **Exposes**: 
  - REST API: /tasks/*, /teams/*
  - Events: task.created, task.completed, task.assigned
- **Consumes**: 
  - auth-service (gRPC): ValidateToken
- **Scaling Strategy**: 
  - Horizontal scaling
  - Read replicas for query-heavy operations
  - Shard by team_id when > 100 teams

**Key Endpoints:**
| Method | Path | Description |
|--------|------|-------------|
| GET | /teams | List user's teams |
| POST | /teams | Create team |
| GET | /teams/:id/tasks | List tasks in team |
| POST | /teams/:id/tasks | Create task |
| PATCH | /tasks/:id | Update task |
| DELETE | /tasks/:id | Delete task |
| POST | /tasks/:id/complete | Mark complete |

---

### Service: notification-service
<!-- سرویس: نوتیفیکیشن -->
- **Responsibility**: Send emails, push notifications, in-app notifications
- **Tech Stack**: Python 3.12, FastAPI + Celery
- **Database**: Redis (queue), PostgreSQL (notification_log)
- **Exposes**: 
  - REST API: /notifications/* (for in-app)
- **Consumes**: 
  - Events: task.created, task.completed, task.assigned
  - Email provider API (SMTP or service like Mailgun)
- **Scaling Strategy**: 
  - Celery workers scale independently
  - Rate limiting per user/channel

---

## 3. Data Model

### Database: auth_db

#### Entity: users
<!-- موجودیت: کاربران -->
```sql
CREATE TABLE users (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email           VARCHAR(255) UNIQUE NOT NULL,
    password_hash   VARCHAR(255) NOT NULL,
    name            VARCHAR(100) NOT NULL,
    email_verified  BOOLEAN DEFAULT FALSE,
    created_at      TIMESTAMP DEFAULT NOW(),
    updated_at      TIMESTAMP DEFAULT NOW()
);
```

#### Entity: teams
<!-- موجودیت: تیم‌ها -->
```sql
CREATE TABLE teams (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name        VARCHAR(100) NOT NULL,
    owner_id    UUID REFERENCES users(id),
    created_at  TIMESTAMP DEFAULT NOW()
);
```

#### Entity: team_members
<!-- موجودیت: عضویت تیم -->
```sql
CREATE TABLE team_members (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    team_id     UUID REFERENCES teams(id) ON DELETE CASCADE,
    user_id     UUID REFERENCES users(id) ON DELETE CASCADE,
    role        VARCHAR(20) NOT NULL CHECK (role IN ('member', 'admin', 'owner')),
    joined_at   TIMESTAMP DEFAULT NOW(),
    UNIQUE(team_id, user_id)
);
```

#### Entity: invites
<!-- موجودیت: دعوت‌نامه‌ها -->
```sql
CREATE TABLE invites (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    team_id     UUID REFERENCES teams(id) ON DELETE CASCADE,
    email       VARCHAR(255) NOT NULL,
    role        VARCHAR(20) NOT NULL,
    token       VARCHAR(64) UNIQUE NOT NULL,
    expires_at  TIMESTAMP NOT NULL,
    created_by  UUID REFERENCES users(id),
    created_at  TIMESTAMP DEFAULT NOW()
);
```

---

### Database: task_db

#### Entity: tasks
<!-- موجودیت: تسک‌ها -->
```sql
CREATE TABLE tasks (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    team_id         UUID NOT NULL,  -- از auth_db میاد، FK نداریم چون DB جداست
    title           VARCHAR(255) NOT NULL,
    description     TEXT,
    status          VARCHAR(20) DEFAULT 'todo' CHECK (status IN ('todo', 'in_progress', 'done')),
    priority        VARCHAR(10) DEFAULT 'medium' CHECK (priority IN ('low', 'medium', 'high')),
    assignee_id     UUID,  -- user id from auth service
    created_by      UUID NOT NULL,
    due_date        DATE,
    completed_at    TIMESTAMP,
    created_at      TIMESTAMP DEFAULT NOW(),
    updated_at      TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_tasks_team_status ON tasks(team_id, status);
CREATE INDEX idx_tasks_assignee ON tasks(assignee_id);
```

#### Entity: comments
<!-- موجودیت: کامنت‌ها -->
```sql
CREATE TABLE comments (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    task_id     UUID REFERENCES tasks(id) ON DELETE CASCADE,
    user_id     UUID NOT NULL,
    content     TEXT NOT NULL,
    created_at  TIMESTAMP DEFAULT NOW()
);
```

### Relationships
```
users (1) ──────< team_members >────── (N) teams
teams (1) ──────< tasks (N)
tasks (1) ──────< comments (N)
users (1) ──────< invites (N)
```

---

## 4. API Contracts

### Auth Service

#### POST /auth/signup
<!-- ثبت‌نام کاربر جدید -->
- **Auth**: Public
- **Request**: 
```json
{
  "email": "user@example.com",
  "password": "min8chars",
  "name": "علی محمدی"
}
```
- **Response (201)**: 
```json
{
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "name": "علی محمدی"
  },
  "token": "jwt_token"
}
```
- **Errors**: 
  - 400: Invalid input
  - 409: Email already exists

#### POST /auth/login
<!-- ورود -->
- **Auth**: Public
- **Request**: 
```json
{
  "email": "user@example.com",
  "password": "password"
}
```
- **Response (200)**: 
```json
{
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "name": "علی محمدی",
    "teams": [{"id": "uuid", "name": "تیم من", "role": "owner"}]
  },
  "token": "jwt_token",
  "refresh_token": "refresh_token"
}
```
- **Errors**: 
  - 401: Invalid credentials
  - 423: Account locked

---

### Task Service

#### POST /teams/:teamId/tasks
<!-- ایجاد تسک -->
- **Auth**: Member, Admin, Owner
- **Request**: 
```json
{
  "title": "طراحی صفحه اصلی",
  "description": "طراحی UI صفحه اصلی با فیگما",
  "priority": "high",
  "assignee_id": "uuid",
  "due_date": "2024-02-15"
}
```
- **Response (201)**: 
```json
{
  "id": "uuid",
  "title": "طراحی صفحه اصلی",
  "status": "todo",
  "priority": "high",
  "assignee": {
    "id": "uuid",
    "name": "سارا احمدی"
  },
  "due_date": "2024-02-15",
  "created_at": "2024-02-01T10:00:00Z"
}
```
- **Errors**: 
  - 400: Invalid input
  - 403: Not a team member
  - 404: Team not found

#### PATCH /tasks/:id
<!-- ویرایش تسک -->
- **Auth**: Creator, Assignee, Admin, Owner
- **Request**: 
```json
{
  "title": "عنوان جدید",
  "status": "in_progress"
}
```
- **Response (200)**: Updated task object
- **Errors**: 
  - 403: Not authorized
  - 404: Task not found

---

## 5. Event Bus / Message Queue
<!-- سیستم پیام‌رسانی -->

Using Redis Pub/Sub for MVP, migrate to RabbitMQ/Kafka if needed.

| Event | Producer | Consumer(s) | Payload |
|-------|----------|-------------|---------|
| task.created | task-service | notification-service | `{task_id, team_id, created_by, assignee_id}` |
| task.completed | task-service | notification-service | `{task_id, completed_by, created_by}` |
| task.assigned | task-service | notification-service | `{task_id, assignee_id, assigned_by}` |
| user.signup | auth-service | notification-service | `{user_id, email}` |
| invite.created | auth-service | notification-service | `{invite_id, email, team_name}` |

---

## 6. Scaling Strategy
<!-- استراتژی مقیاس‌پذیری -->

| Component | Current Setup | Warning Threshold | Scale Action |
|-----------|--------------|-------------------|--------------|
| auth-service | 1 instance | CPU > 70% for 5min | Add instance |
| task-service | 1 instance | CPU > 70% for 5min | Add instance |
| notification-service | 1 worker | Queue > 1000 jobs | Add worker |
| PostgreSQL (auth) | 1 instance, 10GB | Storage > 7GB | Upgrade instance |
| PostgreSQL (task) | 1 instance, 20GB | Storage > 14GB | Add read replica |
| Redis | 1 instance, 1GB | Memory > 700MB | Upgrade instance |

### Scaling Milestones
<!-- نقاط عطف مقیاس‌پذیری -->

**Phase 1: MVP (0-100 users)**
- Single instance per service
- Shared PostgreSQL server
- Redis for cache + queue

**Phase 2: Growth (100-1000 users)**
- 2 instances per service behind LB
- Separate DB per service
- Add read replicas

**Phase 3: Scale (1000+ users)**
- Kubernetes deployment
- Database sharding by team_id
- Dedicated notification queue (RabbitMQ)

---

## 7. Notification System
<!-- سیستم نوتیفیکیشن -->

| Event | Channel | Template | Recipient |
|-------|---------|----------|-----------|
| task.assigned | Email, In-app | "تسک {title} به شما اختصاص داده شد" | Assignee |
| task.completed | In-app | "{user} تسک {title} را تکمیل کرد" | Task creator |
| task.due_soon | Email, In-app | "تسک {title} فردا سررسید می‌شود" | Assignee |
| invite.created | Email | "به تیم {team} دعوت شدید" | Invitee |
| user.welcome | Email | "به TaskFlow خوش آمدید" | New user |

### Notification Preferences
<!-- تنظیمات نوتیفیکیشن -->
Users can control:
- Email notifications: on/off per type
- In-app notifications: always on
- Quiet hours: don't send emails during specified hours

---

## 8. Security Considerations
<!-- ملاحظات امنیتی -->

### Authentication & Authorization
- All API endpoints require JWT (except /auth/login, /auth/signup)
- JWT expires in 15 minutes, refresh token in 7 days
- Passwords hashed with bcrypt (cost factor 12)
- Rate limiting: 100 requests/minute per IP
- CORS: whitelist frontend domain only

### Input/Output Security
- SQL injection prevention: parameterized queries only
- XSS prevention: sanitize all user input
- Error responses: never leak internal details

### 🔐 Secrets Management Architecture
<!-- معماری مدیریت اطلاعات حساس -->

**Development (Local):**
```
/.env                 ← Local secrets (gitignored)
/.env.example         ← Template (committed)
```

**Production (Recommended Flow):**
```
┌─────────────────────────────────────────────────────────┐
│                    Secret Manager                        │
│         (AWS Secrets Manager / HashiCorp Vault)         │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│              CI/CD Pipeline (GitHub Actions)             │
│   - Pulls secrets at deploy time                        │
│   - Injects as environment variables                    │
│   - Never logs or exposes secrets                       │
└────────────────────────┬────────────────────────────────┘
                         │
           ┌─────────────┼─────────────┐
           ▼             ▼             ▼
      ┌─────────┐   ┌─────────┐   ┌─────────┐
      │  Auth   │   │  Task   │   │ Notif   │
      │ Service │   │ Service │   │ Service │
      └─────────┘   └─────────┘   └─────────┘
```

**Required Secrets per Service:**

| Service | Secret | Purpose |
|---------|--------|---------|
| auth-service | `DATABASE_URL` | PostgreSQL connection |
| auth-service | `JWT_SECRET` | Token signing (min 32 chars) |
| auth-service | `REFRESH_SECRET` | Refresh token signing |
| task-service | `DATABASE_URL` | PostgreSQL connection |
| task-service | `AUTH_SERVICE_KEY` | Internal service auth |
| notification-service | `REDIS_URL` | Queue connection |
| notification-service | `SMTP_PASSWORD` | Email sending |
| all | `SENTRY_DSN` | Error tracking (optional) |

**Docker Compose (Development):**
```yaml
services:
  auth-service:
    env_file:
      - ./services/auth-service/.env
    environment:
      - NODE_ENV=development
```

**Kubernetes (Production):**
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: auth-service-secrets
type: Opaque
stringData:
  DATABASE_URL: ${DATABASE_URL}  # Injected by CI/CD
  JWT_SECRET: ${JWT_SECRET}
---
apiVersion: apps/v1
kind: Deployment
spec:
  template:
    spec:
      containers:
        - name: auth-service
          envFrom:
            - secretRef:
                name: auth-service-secrets
```

**⚠️ Critical Rules:**
- NEVER commit `.env` files
- NEVER log secrets (mask in logs)
- Rotate secrets every 90 days
- Use different secrets per environment
- If secret leaks: rotate immediately
