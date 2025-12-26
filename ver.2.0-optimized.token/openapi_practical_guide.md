# 🎯 راهنمای کاربردی OpenAPI
## از صفر تا صد با ابزارهای رایگان

---

## 📚 فهرست

1. [چرا OpenAPI؟](#why-openapi)
2. [ابزارهای ضروری](#essential-tools)
3. [مثال واقعی: Task Manager API](#real-example)
4. [Workflow عملی](#practical-workflow)
5. [Integration با Claude/ChatGPT/Gemini](#ai-integration)
6. [مشکلات رایج و راه‌حل](#troubleshooting)

---

## 🤔 چرا OpenAPI؟ {#why-openapi}

### **قبل از OpenAPI:**
```
شما: "API ساختیم، حالا باید document کنیم"
Frontend Dev: "endpoint چی بود؟ response چه شکلیه؟"
Backend Dev: "نمیدونم، کد رو ببین!"
→ هدر رفت، bug زیاد، documentation قدیمی
```

### **بعد از OpenAPI:**
```
شما: OPENAPI.yaml می‌نویسید (5 دقیقه)
     ↓
Frontend: Client SDK خودکار (1 دقیقه)
Backend: Validation خودکار
Testing: Contract test خودکار
Docs: Interactive documentation خودکار
→ همه چیز sync، هیچ confusion نیست
```

---

## 🛠️ ابزارهای ضروری (همه رایگان) {#essential-tools}

### **1. Swagger Editor (نوشتن و validate)**
```bash
# Option A: Online (بدون نصب)
https://editor.swagger.io

# Option B: Local با Docker
docker run -p 8080:8080 swaggerapi/swagger-editor

# Option C: VSCode Extension
# نصب: "OpenAPI (Swagger) Editor" by 42Crunch
```

### **2. Prism (Mock Server)**
```bash
# نصب
npm install -g @stoplight/prism-cli

# اجرا
prism mock your-api.yaml

# خروجی:
# → http://localhost:4010 (API mock در حال اجرا)
```

### **3. OpenAPI Generator (SDK Generator)**
```bash
# نصب
npm install -g @openapitools/openapi-generator-cli

# تولید TypeScript client
openapi-generator-cli generate \
  -i api.yaml \
  -g typescript-axios \
  -o ./src/api-client

# تولید Python client
openapi-generator-cli generate \
  -i api.yaml \
  -g python \
  -o ./python-client
```

### **4. Swagger UI (Interactive Docs)**
```bash
# Serve documentation
npx swagger-ui-dist serve api.yaml

# یا با Docker
docker run -p 8080:8080 \
  -e SWAGGER_JSON=/api.yaml \
  -v $(pwd):/usr/share/nginx/html \
  swaggerapi/swagger-ui
```

### **5. Dredd (Contract Testing)**
```bash
# نصب
npm install -g dredd

# تست که backend با OpenAPI spec match می‌کنه
dredd api.yaml http://localhost:3000
```

---

## 💼 مثال واقعی: Task Manager API {#real-example}

### **فایل OPENAPI.yaml کامل:**

```yaml
openapi: 3.0.0
info:
  title: Task Manager API
  version: 1.0.0
  description: Simple task management API
  contact:
    name: Your Name
    email: you@example.com

servers:
  - url: http://localhost:3000/api/v1
    description: Development
  - url: https://api.taskmanager.com/v1
    description: Production

tags:
  - name: Auth
    description: Authentication endpoints
  - name: Tasks
    description: Task management
  - name: Users
    description: User management

components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

  schemas:
    User:
      type: object
      required:
        - id
        - email
        - name
      properties:
        id:
          type: string
          format: uuid
          example: "123e4567-e89b-12d3-a456-426614174000"
        email:
          type: string
          format: email
          example: "user@example.com"
        name:
          type: string
          minLength: 2
          maxLength: 50
          example: "John Doe"
        createdAt:
          type: string
          format: date-time
          example: "2024-01-15T10:30:00Z"

    Task:
      type: object
      required:
        - id
        - title
        - status
        - userId
      properties:
        id:
          type: string
          format: uuid
        title:
          type: string
          minLength: 1
          maxLength: 200
          example: "Complete project documentation"
        description:
          type: string
          maxLength: 2000
          example: "Write comprehensive docs for the API"
        status:
          type: string
          enum: [todo, in_progress, done]
          example: "todo"
        priority:
          type: string
          enum: [low, medium, high]
          default: medium
          example: "high"
        dueDate:
          type: string
          format: date
          example: "2024-12-31"
        userId:
          type: string
          format: uuid
        createdAt:
          type: string
          format: date-time
        updatedAt:
          type: string
          format: date-time

    TaskInput:
      type: object
      required:
        - title
      properties:
        title:
          type: string
          minLength: 1
          maxLength: 200
        description:
          type: string
          maxLength: 2000
        status:
          type: string
          enum: [todo, in_progress, done]
        priority:
          type: string
          enum: [low, medium, high]
        dueDate:
          type: string
          format: date

    LoginRequest:
      type: object
      required:
        - email
        - password
      properties:
        email:
          type: string
          format: email
        password:
          type: string
          format: password
          minLength: 8

    LoginResponse:
      type: object
      properties:
        success:
          type: boolean
        token:
          type: string
          example: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
        user:
          $ref: '#/components/schemas/User'

    Error:
      type: object
      properties:
        success:
          type: boolean
          example: false
        error:
          type: string
          example: "Error message"
        code:
          type: string
          example: "VALIDATION_ERROR"

    PaginatedTasks:
      type: object
      properties:
        success:
          type: boolean
        data:
          type: array
          items:
            $ref: '#/components/schemas/Task'
        pagination:
          type: object
          properties:
            page:
              type: integer
              example: 1
            limit:
              type: integer
              example: 20
            total:
              type: integer
              example: 150
            totalPages:
              type: integer
              example: 8

paths:
  /auth/register:
    post:
      summary: Register new user
      tags: [Auth]
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required:
                - email
                - password
                - name
              properties:
                email:
                  type: string
                  format: email
                password:
                  type: string
                  format: password
                  minLength: 8
                name:
                  type: string
                  minLength: 2
      responses:
        '201':
          description: User created successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/LoginResponse'
        '400':
          description: Validation error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
        '409':
          description: Email already exists
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'

  /auth/login:
    post:
      summary: Login user
      tags: [Auth]
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/LoginRequest'
      responses:
        '200':
          description: Login successful
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/LoginResponse'
        '401':
          description: Invalid credentials
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'

  /users/me:
    get:
      summary: Get current user profile
      tags: [Users]
      security:
        - bearerAuth: []
      responses:
        '200':
          description: User profile
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                  data:
                    $ref: '#/components/schemas/User'
        '401':
          description: Unauthorized
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'

  /tasks:
    get:
      summary: List all tasks for current user
      tags: [Tasks]
      security:
        - bearerAuth: []
      parameters:
        - name: page
          in: query
          schema:
            type: integer
            default: 1
            minimum: 1
        - name: limit
          in: query
          schema:
            type: integer
            default: 20
            minimum: 1
            maximum: 100
        - name: status
          in: query
          schema:
            type: string
            enum: [todo, in_progress, done]
        - name: priority
          in: query
          schema:
            type: string
            enum: [low, medium, high]
        - name: search
          in: query
          schema:
            type: string
          description: Search in title and description
      responses:
        '200':
          description: Tasks retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PaginatedTasks'
        '401':
          description: Unauthorized
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'

    post:
      summary: Create new task
      tags: [Tasks]
      security:
        - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/TaskInput'
      responses:
        '201':
          description: Task created
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                  data:
                    $ref: '#/components/schemas/Task'
        '400':
          description: Validation error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
        '401':
          description: Unauthorized

  /tasks/{taskId}:
    get:
      summary: Get task by ID
      tags: [Tasks]
      security:
        - bearerAuth: []
      parameters:
        - name: taskId
          in: path
          required: true
          schema:
            type: string
            format: uuid
      responses:
        '200':
          description: Task retrieved
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                  data:
                    $ref: '#/components/schemas/Task'
        '404':
          description: Task not found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
        '401':
          description: Unauthorized

    put:
      summary: Update task
      tags: [Tasks]
      security:
        - bearerAuth: []
      parameters:
        - name: taskId
          in: path
          required: true
          schema:
            type: string
            format: uuid
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/TaskInput'
      responses:
        '200':
          description: Task updated
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                  data:
                    $ref: '#/components/schemas/Task'
        '404':
          description: Task not found
        '401':
          description: Unauthorized

    delete:
      summary: Delete task
      tags: [Tasks]
      security:
        - bearerAuth: []
      parameters:
        - name: taskId
          in: path
          required: true
          schema:
            type: string
            format: uuid
      responses:
        '204':
          description: Task deleted successfully
        '404':
          description: Task not found
        '401':
          description: Unauthorized

  /tasks/{taskId}/status:
    patch:
      summary: Update task status only
      tags: [Tasks]
      security:
        - bearerAuth: []
      parameters:
        - name: taskId
          in: path
          required: true
          schema:
            type: string
            format: uuid
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required:
                - status
              properties:
                status:
                  type: string
                  enum: [todo, in_progress, done]
      responses:
        '200':
          description: Status updated
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                  data:
                    $ref: '#/components/schemas/Task'
        '404':
          description: Task not found
        '401':
          description: Unauthorized
```

---

## 🔄 Workflow عملی {#practical-workflow}

### **مرحله 1: طراحی API (5-10 دقیقه)**
```bash
# 1. فایل OPENAPI.yaml بالا را بسازید (از مثال بالا)
# 2. Validate کنید
npx swagger-cli validate task-manager-api.yaml

# ✅ Output: "API is valid"
```

### **مرحله 2: Mock Server (1 دقیقه)**
```bash
# Mock API را start کنید
prism mock task-manager-api.yaml

# Output:
# [HTTP SERVER] Listening on http://localhost:4010
# [VALIDATOR] Your API will be validated
```

**حالا می‌توانید test کنید:**
```bash
# Login test (بدون backend!)
curl -X POST http://localhost:4010/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "test@example.com", "password": "password123"}'

# Response: Mock data based on schema!
{
  "success": true,
  "token": "eyJhbGci...",
  "user": {
    "id": "123e4567-e89b-12d3-a456-426614174000",
    "email": "test@example.com",
    "name": "John Doe"
  }
}
```

### **مرحله 3: Generate Frontend Client (2 دقیقه)**
```bash
# تولید TypeScript client
openapi-generator-cli generate \
  -i task-manager-api.yaml \
  -g typescript-axios \
  -o frontend/src/api

# فایل‌های تولید شده:
# frontend/src/api/
# ├── api.ts          # همه API classes
# ├── configuration.ts
# ├── base.ts
# └── index.ts
```

**استفاده در React:**
```typescript
// frontend/src/App.tsx
import { AuthApi, TasksApi, Configuration } from './api'

const config = new Configuration({
  basePath: 'http://localhost:4010/api/v1', // Mock server!
  accessToken: localStorage.getItem('token') || undefined,
})

const authApi = new AuthApi(config)
const tasksApi = new TasksApi(config)

// Login
const loginResult = await authApi.authLoginPost({
  email: 'user@example.com',
  password: 'password123',
})

// Get tasks
const tasks = await tasksApi.tasksGet({
  page: 1,
  limit: 20,
  status: 'todo',
})

// Create task
const newTask = await tasksApi.tasksPost({
  title: 'New Task',
  description: 'Task description',
  priority: 'high',
})

// همه TypeScript types خودکار!
// IDE autocomplete کامل!
```

### **مرحله 4: Build Backend با AI (Claude/ChatGPT/Gemini)**

#### **با Claude Code:**
```bash
claude

# در Claude Code:
> Build Express backend for task-manager-api.yaml
  - Use TypeScript
  - Implement all endpoints from OPENAPI.yaml
  - Add JWT authentication
  - Use MongoDB for database
  - Match response schemas exactly
```

#### **با GitHub Copilot (ChatGPT):**
```
@workspace Create Express server matching task-manager-api.yaml

Requirements:
1. TypeScript
2. Implement POST /auth/login
3. Implement GET /tasks with pagination
4. JWT authentication matching bearerAuth schema
5. Validate requests against OpenAPI spec
6. Return responses matching exact schema

Reference AI-CONTEXT.md for code standards.
```

#### **با Gemini CLI:**
```bash
gemini-cli --context AI-CONTEXT.md \
  --file task-manager-api.yaml \
  "Create Express TypeScript server implementing all endpoints from OpenAPI spec"
```

### **مرحله 5: Auto-Validate Backend**
```bash
# در backend، نصب کنید:
npm install express-openapi-validator

# در app.ts:
import { OpenApiValidator } from 'express-openapi-validator'

app.use(
  OpenApiValidator.middleware({
    apiSpec: './task-manager-api.yaml',
    validateRequests: true,   // Validate incoming requests
    validateResponses: true,  // Validate outgoing responses
  })
)

// اگر response با OpenAPI match نکنه، error می‌ده!
```

### **مرحله 6: Contract Testing**
```bash
# Backend را start کنید
npm run dev  # http://localhost:3000

# Test که همه endpoints با spec match می‌کنند
dredd task-manager-api.yaml http://localhost:3000

# Output:
# pass: POST /auth/register
# pass: POST /auth/login
# pass: GET /tasks
# fail: POST /tasks (response doesn't match schema)
#       ↑ می‌فهمید کجا مشکل داره!
```

---

## 🤖 Integration با AI Tools {#ai-integration}

### **Pattern 1: API-First با Claude Code**
```bash
# 1. OpenAPI را بنویسید
# 2. Mock server start کنید
prism mock api.yaml &

# 3. Frontend با mock بسازید
claude
> Build React app using api-client/ folder
  Connect to http://localhost:4010

# 4. Backend بسازید
claude
> Build Express backend matching api.yaml
  All responses must match schemas exactly
```

### **Pattern 2: Iterative با GitHub Copilot**
```typescript
// در VSCode, endpoint template:
// @workspace implement POST /tasks from task-manager-api.yaml

export const createTask = async (req: Request, res: Response) => {
  // Copilot auto-completes based on OpenAPI!
  const { title, description, status, priority, dueDate } = req.body
  
  // Validation is automatic (if using express-openapi-validator)
  const task = await Task.create({
    title,
    description,
    status: status || 'todo',
    priority: priority || 'medium',
    dueDate,
    userId: req.user.id,
  })
  
  res.status(201).json({
    success: true,
    data: task,
  })
}
```

### **Pattern 3: Quick Scripts با Gemini CLI**
```bash
# تولید sample data
gemini-cli --file api.yaml \
  "Generate 10 sample tasks matching Task schema in JSON format"

# تولید test cases
gemini-cli --file api.yaml \
  "Generate Jest test cases for all /tasks endpoints"
```

---

## 🐛 مشکلات رایج و راه‌حل {#troubleshooting}

### **مشکل 1: OpenAPI validation errors**
```
Error: should have required property 'status'
```

**راه‌حل:**
```yaml
# مطمئن شوید required fields در schema تعریف شده:
Task:
  required:  # ← این خط مهمه!
    - id
    - title
    - status
```

### **مشکل 2: Prism mock server نمی‌خواند**
```
Error: Cannot read file at path
```

**راه‌حل:**
```bash
# مسیر کامل بدهید
prism mock $(pwd)/api.yaml

# یا cd به دایرکتوری فایل
cd docs/
prism mock OPENAPI.yaml
```

### **مشکل 3: Generated client compile نمی‌شود**
```
Error: Property 'xyz' does not exist on type...
```

**راه‌حل:**
```yaml
# در OpenAPI، همه properties را define کنید:
properties:
  xyz:  # ← نباید undefined باشه
    type: string
```

### **مشکل 4: Backend response با schema match نمی‌کنه**
```
Error: should be object
```

**راه‌حل:**
```typescript
// بجای:
res.json(tasks)

// این را بنویسید (match schema):
res.json({
  success: true,
  data: tasks,
  pagination: { ... }
})
```

---

## 🎯 Checklist نهایی

- [ ] OPENAPI.yaml نوشته شده
- [ ] Validation با swagger-cli انجام شده
- [ ] Mock server با Prism اجرا می‌شود
- [ ] Frontend client generate شده
- [ ] Backend endpoints implement شده
- [ ] Auto-validation روی backend فعال است
- [ ] Contract testing با Dredd انجام شده
- [ ] Documentation با Swagger UI قابل دسترسی است

---

## 🚀 مرحله بعد

با این setup، می‌توانید:

1. **Frontend و Backend موازی** توسعه دهید (با mock)
2. **TypeScript types** همیشه sync باشند
3. **API contract** guaranteed باشد
4. **Documentation** همیشه updated باشد
5. **Testing** خودکار باشد

**همه اینها با یک فایل YAML!** 🎉
