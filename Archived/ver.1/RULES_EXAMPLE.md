# Coding Rules: TaskFlow

## 1. Language & Versions (MUST)
<!-- زبان و نسخه‌ها - اجباری -->
- **Backend**: Python 3.12
- **Frontend**: TypeScript 5.3+
- **Node.js**: 20 LTS
- **Database**: PostgreSQL 16
- **Cache/Queue**: Redis 7

---

## 2. Frameworks (MUST)
<!-- فریم‌ورک‌ها - اجباری -->

### Backend
- **Web Framework**: FastAPI 0.110+
- **ORM**: SQLAlchemy 2.0 (async)
- **Validation**: Pydantic v2
- **Task Queue**: Celery 5.3 + Redis
- **Testing**: pytest + pytest-asyncio

### Frontend
- **UI Framework**: React 18
- **Build**: Vite 5
- **Styling**: Tailwind CSS 3.4
- **State**: Zustand (client) + TanStack Query (server)
- **Testing**: Vitest + React Testing Library

---

## 3. Project Structure
<!-- ساختار پروژه -->

```
/taskflow
  /services
    /auth-service
      /src
        /api            # FastAPI routers
        /core           # Business logic, use cases
        /data           # Repositories, database access
        /models         # Pydantic models, SQLAlchemy models
        /utils          # Helpers, no business logic
      /tests
        /unit
        /integration
      main.py           # FastAPI app entry
      Dockerfile
      requirements.txt
    /task-service
      /src
        /api
        /core
        /data
        /models
        /utils
      /tests
      main.py
      Dockerfile
      requirements.txt
    /notification-service
      ...
  /frontend
    /src
      /components       # Reusable UI components
        /ui             # Primitive components (Button, Input)
        /features       # Feature-specific components
      /pages            # Route components
      /hooks            # Custom React hooks
      /stores           # Zustand stores
      /api              # API client, react-query hooks
      /utils            # Helper functions
      /types            # TypeScript types
    /public
    /tests
    vite.config.ts
    tailwind.config.js
  /infra
    /docker
    /k8s              # برای فاز بعدی
    docker-compose.yml
  /docs
    PROJECT.md
    SPEC.md
    ARCHITECTURE.md
    FRONTEND.md
    RULES.md
```

---

## 4. Naming Conventions
<!-- قراردادهای نام‌گذاری -->

| Type | Convention | Example |
|------|------------|---------|
| Python files | snake_case | `user_service.py` |
| Python classes | PascalCase | `UserService` |
| Python functions | snake_case | `create_user()` |
| Python constants | UPPER_SNAKE | `MAX_RETRIES` |
| TypeScript files | kebab-case | `user-service.ts` |
| React components | PascalCase file & export | `TaskCard.tsx` |
| TypeScript functions | camelCase | `createUser()` |
| CSS classes | kebab-case (Tailwind) | `text-primary` |
| Database tables | snake_case, plural | `users`, `team_members` |
| Database columns | snake_case | `created_at` |
| API endpoints | kebab-case, plural nouns | `/api/v1/team-members` |
| Environment vars | UPPER_SNAKE | `DATABASE_URL` |

---

## 5. Error Handling (MUST)
<!-- مدیریت خطا - اجباری -->

### Backend
All errors MUST be logged with context:
```python
# ✅ Correct
logger.error("Failed to create task", extra={
    "user_id": user_id,
    "team_id": team_id,
    "error": str(e)
})

# ❌ Wrong
print(f"Error: {e}")
```

All API errors MUST return consistent format:
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "عنوان تسک نمی‌تواند خالی باشد",
    "details": {
      "field": "title",
      "reason": "required"
    }
  }
}
```

Standard error codes:
| Code | HTTP Status | Description |
|------|-------------|-------------|
| VALIDATION_ERROR | 400 | Input validation failed |
| UNAUTHORIZED | 401 | Not authenticated |
| FORBIDDEN | 403 | Not authorized |
| NOT_FOUND | 404 | Resource not found |
| CONFLICT | 409 | Resource already exists |
| RATE_LIMITED | 429 | Too many requests |
| INTERNAL_ERROR | 500 | Server error |

### Frontend
```typescript
// ✅ Correct - Typed error handling
try {
  await createTask(data);
} catch (error) {
  if (error instanceof ApiError) {
    toast.error(error.message);
  } else {
    toast.error('خطای غیرمنتظره');
    captureException(error);
  }
}

// ❌ Wrong
try {
  await createTask(data);
} catch (e) {
  console.log(e);
}
```

---

## 6. Forbidden Patterns (MUST NOT)
<!-- الگوهای ممنوع -->

### Backend
- ❌ No global mutable state
- ❌ No hardcoded secrets (use env vars)
- ❌ No `print()` for logging (use `logging` module)
- ❌ No raw SQL strings (use parameterized queries)
- ❌ No `*` imports (explicit imports only)
- ❌ No blocking calls in async functions
- ❌ No business logic in API routes (use services)

### Frontend
- ❌ No `any` type (use `unknown` if needed)
- ❌ No `console.log` in production
- ❌ No inline styles (use Tailwind)
- ❌ No direct DOM manipulation
- ❌ No API calls in components (use hooks)
- ❌ No prop drilling > 2 levels (use context/store)

### Database
- ❌ No DELETE without WHERE
- ❌ No SELECT * (specify columns)
- ❌ No storing plain-text passwords
- ❌ No N+1 queries

---

## 7. Required Patterns (MUST)
<!-- الگوهای اجباری -->

### Backend
- ✅ All functions must have type hints
- ✅ All API endpoints must validate input with Pydantic
- ✅ All database queries must use async
- ✅ All external calls must have timeout
- ✅ All secrets must come from environment
- ✅ All log messages must include request_id

```python
# ✅ Correct
async def create_task(
    task_data: TaskCreate,
    user_id: UUID,
    team_id: UUID
) -> Task:
    """Create a new task in the team."""
    ...
```

### Frontend
- ✅ All components must be functional
- ✅ All props must be typed
- ✅ All API calls must use react-query
- ✅ All forms must have validation
- ✅ All interactive elements must be keyboard accessible

```typescript
// ✅ Correct
interface TaskCardProps {
  task: Task;
  onComplete: (id: string) => void;
}

export function TaskCard({ task, onComplete }: TaskCardProps) {
  ...
}
```

---

## 8. Testing Requirements
<!-- الزامات تست -->

### Backend
- Unit tests for all business logic (core/)
- Integration tests for all API endpoints
- Minimum coverage: 80%
- Test naming: `test_<action>_<scenario>_<expected>`

```python
# ✅ Correct
def test_create_task_with_valid_data_returns_task():
    ...

def test_create_task_without_title_raises_validation_error():
    ...
```

### Frontend
- Unit tests for utility functions
- Component tests for complex components
- E2E tests for critical flows (login, create task)
- Minimum coverage: 70%

---

## 9. Git Conventions
<!-- قراردادهای گیت -->

### Branch Naming
```
feature/TASK-123-add-user-login
bugfix/TASK-456-fix-task-completion
hotfix/critical-security-patch
```

### Commit Message Format
```
type(scope): subject

body (optional)

footer (optional)
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

Examples:
```
feat(task): add task completion endpoint
fix(auth): resolve token refresh race condition
docs(readme): update installation steps
```

### PR Requirements
- Must pass all CI checks
- Must have at least 1 approval (if team)
- Must have descriptive title and description
- Must reference related issue/task
- Must not have merge conflicts

---

## 10. API Design Rules
<!-- قوانین طراحی API -->

### Versioning
- URL-based: `/api/v1/...`
- Only increment on breaking changes

### Request/Response
- Always use JSON
- Always include `Content-Type: application/json`
- Use camelCase in JSON (matches frontend)
- Use snake_case in Python (auto-convert with Pydantic)

### Pagination
```json
{
  "items": [...],
  "pagination": {
    "page": 1,
    "per_page": 20,
    "total": 150,
    "total_pages": 8
  }
}
```

### Filtering
- Use query params: `?status=done&priority=high`
- Support multiple values: `?status=todo,in_progress`

---

## 11. Security Rules (MUST)
<!-- قوانین امنیتی - اجباری -->

### 🔐 Secrets Management (CRITICAL - NO EXCEPTIONS)
<!-- مدیریت اطلاعات حساس - بدون استثنا -->

**NEVER put these in source code:**
- ❌ API keys / tokens
- ❌ Database passwords  
- ❌ JWT secrets
- ❌ OAuth client secrets
- ❌ Encryption keys
- ❌ Any credentials

**ALWAYS use environment variables:**
```python
# ✅ CORRECT
import os
from functools import lru_cache
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    database_url: str
    jwt_secret: str
    redis_url: str
    api_key: str
    
    class Config:
        env_file = ".env"

@lru_cache
def get_settings() -> Settings:
    return Settings()

# Usage
settings = get_settings()
db = connect(settings.database_url)
```

```python
# ❌ WRONG - ABSOLUTELY FORBIDDEN
DATABASE_URL = "postgresql://admin:MyP@ssw0rd@localhost/taskflow"
JWT_SECRET = "super-secret-key-123"
API_KEY = "sk-proj-abc123xyz789"
```

**Required files:**

`.env.example` (MUST commit - template only):
```env
# Database
DATABASE_URL=postgresql://user:password@host:5432/dbname

# Auth
JWT_SECRET=generate-min-32-char-random-string
JWT_EXPIRY_MINUTES=15
REFRESH_TOKEN_DAYS=7

# Redis
REDIS_URL=redis://localhost:6379

# External Services
SMTP_HOST=smtp.example.com
SMTP_USER=
SMTP_PASSWORD=

# Optional
SENTRY_DSN=
```

`.env` (NEVER commit - real values):
```env
DATABASE_URL=postgresql://taskflow:real_password_here@db.server.com:5432/taskflow_prod
JWT_SECRET=aK3mP9xL2nQ8vR5tY7wB4cF6hJ0dG1sU
...
```

`.gitignore` (MUST include):
```gitignore
# Secrets - NEVER commit
.env
.env.local
.env.*.local
.env.production
*.pem
*.key
*.p12
secrets/
config/local.py
config/production.py

# Logs (may contain sensitive data)
*.log
logs/
```

### 🛡️ Authentication & Authorization
- ✅ All endpoints must validate JWT (except public)
- ✅ All passwords must be hashed with bcrypt (cost 12+)
- ✅ JWT expiry: 15 minutes max
- ✅ Refresh tokens: httpOnly cookie, 7 days max
- ✅ Always check permissions, not just authentication

### 🔒 Input Validation
- ✅ All inputs must be sanitized
- ✅ Use Pydantic for all request validation
- ✅ Limit string lengths
- ✅ Validate file types and sizes
- ✅ Escape output for XSS prevention

### 🚫 Error Handling (Security)
```python
# ✅ CORRECT - Generic message to user
except Exception as e:
    logger.error(f"Login failed: {e}", extra={"email": email})
    raise HTTPException(401, "Invalid credentials")

# ❌ WRONG - Exposes internal info
except Exception as e:
    raise HTTPException(401, f"Database error: {e}")
```

### 🌐 Network Security
- ✅ Rate limiting on all public endpoints (100/min per IP)
- ✅ CORS must whitelist only known origins
- ✅ HTTPS only in production
- ✅ Security headers (CSP, X-Frame-Options, etc.)

### 📋 Security Checklist Before Deploy
- [ ] No secrets in code or git history
- [ ] .env.example exists with all required vars
- [ ] .gitignore includes all sensitive files
- [ ] Rate limiting configured
- [ ] CORS configured correctly
- [ ] HTTPS enforced
- [ ] SQL injection prevention verified
- [ ] XSS prevention verified

---

## 12. Documentation Rules
<!-- قوانین مستندسازی -->

### Code Comments
- ✅ Document "why", not "what"
- ✅ Use docstrings for public functions
- ❌ Don't comment obvious code

### API Documentation
- Auto-generate from Pydantic models (FastAPI)
- Keep examples up to date
- Document all error responses

### README per Service
Each service must have README with:
- What it does
- How to run locally
- Environment variables needed
- How to run tests
