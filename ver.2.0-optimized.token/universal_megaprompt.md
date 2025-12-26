# 🌐 Universal MegaPrompt Generator
## Works with Claude Code, ChatGPT Code, Gemini CLI + OpenAPI Spec

---

## 🎯 OVERVIEW

This MegaPrompt generates **6 optimized files** that work across all AI coding tools:
1. **PRD.md** - Human-readable product requirements
2. **TASKS.md** - Sequential development checklist
3. **SPEC.md** - Technical specification
4. **ARCHITECTURE.md** - System design & data models
5. **OPENAPI.yaml** - API specification (OpenAPI 3.0)
6. **AI-CONTEXT.md** - Ultra-compact context (replaces CLAUDE.md)

---

## 🤖 THE UNIVERSAL MEGAPROMPT (Copy from here ↓)

```
You are a technical project organizer specializing in multi-platform AI-assisted development.

I will provide my project idea (possibly disorganized). Your task:
1. Organize my thoughts without adding/removing information
2. Generate 6 files optimized for Claude Code, ChatGPT Code, and Gemini CLI
3. Include OpenAPI specification for API-first development

---

## OUTPUT: 6 FILES

### ──────────────────────────────────
### 📄 File 1: PRD.md
### ──────────────────────────────────

**Purpose:** Human-readable documentation for stakeholders  
**Language:** Natural language (Persian/English based on user input)

**Structure:**
```markdown
# [Project Name]

## 🎯 Goal
[One paragraph: what, why, for whom]

## 👥 Target Users
[Who uses this? Their needs]

## ✨ Core Features
1. [Feature name] - [Description as user described]
2. [Feature name] - [Description as user described]
...

## 🎨 UI/UX Requirements
[Design requirements mentioned]

## 🔧 Technical Requirements
[Stack, integrations mentioned]

## 📊 Success Metrics
[How to measure success]

## 🚫 Out of Scope
[Explicitly excluded features]

## 📝 Additional Notes
[Other context provided]
```

---

### ──────────────────────────────────
### 📄 File 2: TASKS.md
### ──────────────────────────────────

**Purpose:** Sequential development checklist (works with all AI tools)

**Structure:**
```markdown
# 🎯 Development Tasks

## Phase 1: Setup & Foundation
- [ ] 1.1: [Task description - specific & actionable]
- [ ] 1.2: [Next task]
...

## Phase 2: Core Features
- [ ] 2.1: [Feature task]
...

## Phase 3: Integration & Testing
...

## Phase 4: Polish & Deploy
...

---

## 🤖 Tool-Specific Commands

### For Claude Code:
```bash
claude
> Build Task 1.1 from TASKS.md following AI-CONTEXT.md
```

### For ChatGPT Code:
```bash
# In VSCode with GitHub Copilot Chat
@workspace Build Task 1.1 from TASKS.md. Reference AI-CONTEXT.md for standards.
```

### For Gemini CLI:
```bash
gemini-cli --context AI-CONTEXT.md "Implement Task 1.1 from TASKS.md"
```
```

---

### ──────────────────────────────────
### 📄 File 3: SPEC.md
### ──────────────────────────────────

**Purpose:** Concise technical specification (max 600 tokens)

**Structure:**
```markdown
# Technical Specification

## Core Goal
[One sentence technical summary]

## Tech Stack
- **Frontend:** [Technologies]
- **Backend:** [Technologies]
- **Database:** [Technologies]
- **APIs:** [External services]
- **Tools:** [Development tools]

## Key Features (Technical)
1. **[Feature]**: [Technical description]
2. **[Feature]**: [Technical description]
...

## API Requirements
- RESTful endpoints (see OPENAPI.yaml for details)
- Authentication: [Method]
- Rate limiting: [Policy]

## Data Requirements
- [Data to store]
- [Data to process]
- [Data to display]

## Performance Requirements
- Load time: [Target]
- Response time: [Target]
- Scalability: [Target]

## Security Requirements
- Authentication: [Method]
- Authorization: [Rules]
- Data protection: [Measures]

## Integration Points
- [External API 1]
- [External API 2]
...
```

---

### ──────────────────────────────────
### 📄 File 4: ARCHITECTURE.md
### ──────────────────────────────────

**Purpose:** Visual system design (ASCII diagrams for AI compatibility)

**Structure:**
```markdown
# System Architecture

## High-Level Flow (ASCII Diagram)
```
[User] → [Frontend] → [API Gateway] → [Services] → [Database]
                          ↓
                    [External APIs]
```

## Component Breakdown

### Frontend Components
- [Component 1]: [Purpose]
- [Component 2]: [Purpose]
...

### Backend Services
- [Service 1]: [Purpose]
- [Service 2]: [Purpose]
...

### Database Schema (ASCII)
```
┌─────────────┐      ┌─────────────┐
│   Table 1   │──────│   Table 2   │
└─────────────┘      └─────────────┘
```

## Data Models (TypeScript/JSON)
```typescript
interface ModelName {
  id: string
  field1: type
  field2: type
  ...
}
```

## API Flow Examples
1. [User action] → [API endpoint] → [Database operation] → [Response]
2. [User action] → [API endpoint] → [External API call] → [Response]
...

## File Structure
```
project/
├── frontend/
│   ├── src/
│   └── ...
├── backend/
│   ├── src/
│   └── ...
└── docs/
```
```

---

### ──────────────────────────────────
### 📄 File 5: OPENAPI.yaml ⭐ NEW!
### ──────────────────────────────────

**Purpose:** API specification (OpenAPI 3.0 standard)  
**Why Important:** 
- Auto-generates client SDKs
- Provides API documentation
- Enables API-first development
- Works with Postman, Swagger, etc.

**Structure:**
```yaml
openapi: 3.0.0
info:
  title: [Project Name] API
  version: 1.0.0
  description: [Brief API description]

servers:
  - url: http://localhost:3000/api
    description: Development server
  - url: https://api.production.com
    description: Production server

components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

  schemas:
    # Data models (from ARCHITECTURE.md)
    User:
      type: object
      properties:
        id:
          type: string
          format: uuid
        email:
          type: string
          format: email
        name:
          type: string
      required:
        - email
        - name

    Error:
      type: object
      properties:
        success:
          type: boolean
          example: false
        error:
          type: string
          example: "Error message"

paths:
  # Authentication endpoints
  /auth/login:
    post:
      summary: User login
      tags: [Authentication]
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                email:
                  type: string
                  format: email
                password:
                  type: string
                  format: password
      responses:
        '200':
          description: Login successful
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                  token:
                    type: string
                  user:
                    $ref: '#/components/schemas/User'
        '401':
          description: Invalid credentials
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'

  # CRUD endpoints
  /items:
    get:
      summary: List all items
      tags: [Items]
      security:
        - bearerAuth: []
      parameters:
        - name: page
          in: query
          schema:
            type: integer
            default: 1
        - name: limit
          in: query
          schema:
            type: integer
            default: 20
      responses:
        '200':
          description: Items retrieved successfully
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                  data:
                    type: array
                    items:
                      $ref: '#/components/schemas/Item'
                  pagination:
                    type: object

    post:
      summary: Create new item
      tags: [Items]
      security:
        - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ItemInput'
      responses:
        '201':
          description: Item created
        '400':
          description: Validation error

  /items/{id}:
    get:
      summary: Get item by ID
      tags: [Items]
      security:
        - bearerAuth: []
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Item retrieved
        '404':
          description: Item not found

    put:
      summary: Update item
      tags: [Items]
      security:
        - bearerAuth: []
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ItemInput'
      responses:
        '200':
          description: Item updated
        '404':
          description: Item not found

    delete:
      summary: Delete item
      tags: [Items]
      security:
        - bearerAuth: []
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '204':
          description: Item deleted
        '404':
          description: Item not found

# Add more endpoints as needed...
```

**Usage Tips:**
- Import into Postman for testing
- Generate client SDK with openapi-generator
- Host docs with Swagger UI
- Use as single source of truth for API contract

---

### ──────────────────────────────────
### 📄 File 6: AI-CONTEXT.md
### ──────────────────────────────────

**Purpose:** Ultra-compact context (max 400 tokens) for ALL AI tools  
**This replaces:** CLAUDE.md (now universal)

**Structure:**
```markdown
# AI Development Context

## Stack
[Tech stack in one line]

## Quick Start
```bash
# Development
[command to start dev server]

# Build
[command to build]

# Test
[command to run tests]
```

## Project Structure
```
[Minimal tree showing key folders]
```

## Code Standards
✅ [3-5 key rules to follow]
❌ [3-5 things to avoid]

## API Contract
See OPENAPI.yaml for all endpoints. Key routes:
- POST /auth/login - Authentication
- GET /items - List items
- [2-3 more important routes]

## Data Flow
[Simple one-line flow diagram]

## Environment Variables
```env
[List 5-7 critical env vars]
```

## Current Phase
[What we're building now - from TASKS.md]

## Tool-Specific Notes

### Claude Code
- Reads this file automatically
- Use: `claude` then describe task

### ChatGPT Code (GitHub Copilot)
- Mention this file in prompts
- Use: `@workspace` to reference project context

### Gemini CLI
- Pass as context: `--context AI-CONTEXT.md`
- Use: `gemini-cli --context AI-CONTEXT.md "your prompt"`

## Quick Commands by Tool

### Claude Code
```bash
claude
> Build authentication following OPENAPI.yaml spec
```

### GitHub Copilot Chat (ChatGPT)
```
@workspace Implement POST /auth/login from OPENAPI.yaml
Reference AI-CONTEXT.md for standards
```

### Gemini CLI
```bash
gemini-cli --context AI-CONTEXT.md \
  "Implement GET /items endpoint as defined in OPENAPI.yaml"
```
```

---

## ⚙️ PROCESSING RULES

1. **Organize, don't add:** Rearrange information logically without adding features
2. **Preserve details:** Keep ALL information provided by user
3. **OpenAPI first:** Design API contract before implementation
4. **Token efficiency:** Keep files under token limits specified
5. **Tool agnostic:** Make files work with Claude, ChatGPT, and Gemini
6. **Language:** PRD in user's language, technical docs in English
7. **Clarification:** Mark unclear items as [NEEDS CLARIFICATION: question]

---

## 📤 OUTPUT FORMAT

Generate files in this order:
1. PRD.md
2. TASKS.md
3. SPEC.md
4. ARCHITECTURE.md
5. OPENAPI.yaml
6. AI-CONTEXT.md

Separate each with:
```
───────────────────────────────────────
## 📄 [FILENAME]
───────────────────────────────────────
```

---

## 🎯 NOW PROCESS MY PROJECT

[USER PASTES THEIR PROJECT DESCRIPTION HERE]

```

---

## 🔥 HOW TO USE (Step-by-Step)

### **Step 1: Generate Files**
1. Copy the MegaPrompt above
2. Paste into Claude/ChatGPT/Gemini web chat
3. Add your project description (can be messy)
4. Get 6 organized files

### **Step 2: Save Files**
```bash
mkdir my-project
cd my-project
mkdir docs

# Save files:
docs/PRD.md              # Human documentation
docs/TASKS.md            # Development checklist
docs/SPEC.md             # Technical spec
docs/ARCHITECTURE.md     # System design
docs/OPENAPI.yaml        # API specification ⭐
AI-CONTEXT.md            # Root level! (for AI tools)
```

### **Step 3: Setup OpenAPI Tools**
```bash
# Install OpenAPI tools
npm install -g @stoplight/prism-cli     # API mocking
npm install -g @openapitools/openapi-generator-cli  # SDK generation

# Mock API for frontend development
prism mock docs/OPENAPI.yaml

# Generate client SDK
openapi-generator-cli generate \
  -i docs/OPENAPI.yaml \
  -g typescript-axios \
  -o src/api-client
```

### **Step 4: Start Coding**

#### With **Claude Code**:
```bash
claude
> Build Task 1.1 from TASKS.md. Use OPENAPI.yaml for API endpoints.
```

#### With **GitHub Copilot** (ChatGPT):
```
# In VSCode, open Copilot Chat
@workspace Build authentication system from TASKS.md Task 2.1
Follow OPENAPI.yaml spec for /auth/login endpoint
Reference AI-CONTEXT.md for standards
```

#### With **Gemini CLI**:
```bash
gemini-cli --context AI-CONTEXT.md \
  --file docs/OPENAPI.yaml \
  "Implement the login endpoint as specified in OPENAPI.yaml"
```

---

## 🌟 WHY OPENAPI SPEC IS CRUCIAL

### **1. API-First Development**
```
Traditional: Code → Document API
API-First:   Design API → Generate Code
             ↑ Better!
```

### **2. Auto-Generate Everything**
```bash
# Generate TypeScript client
openapi-generator-cli generate -g typescript-axios

# Generate Python client  
openapi-generator-cli generate -g python

# Generate server stubs
openapi-generator-cli generate -g nodejs-express-server

# Generate documentation
openapi-generator-cli generate -g html
```

### **3. Mock API Before Backend**
```bash
# Start mock server (instant!)
prism mock OPENAPI.yaml

# Frontend can develop against mock
# Backend builds to match spec
```

### **4. Test API Contract**
```bash
# Validate OpenAPI file
npx swagger-cli validate OPENAPI.yaml

# Test against running API
npx dredd OPENAPI.yaml http://localhost:3000
```

### **5. Interactive Documentation**
```bash
# Serve Swagger UI
npx swagger-ui-dist-serve OPENAPI.yaml

# Or use Redoc
npx redoc-cli serve OPENAPI.yaml
```

---

## 🎯 TOOL COMPARISON

| Feature | Claude Code | GitHub Copilot | Gemini CLI |
|---------|------------|----------------|------------|
| **Auto-loads context** | ✅ AI-CONTEXT.md | ❌ Must mention | ❌ Must pass flag |
| **Best for** | Full features | Code completion | Quick scripts |
| **OpenAPI support** | ✅ Excellent | ⚠️ Moderate | ✅ Good |
| **Multi-file edits** | ✅ Yes | ⚠️ Limited | ⚠️ Limited |
| **Cost** | Included in Pro/Max | Included in Copilot | Free tier available |
| **Command** | `claude` | `@workspace` | `gemini-cli` |

### **When to use each:**

**Claude Code:**
- Building entire features (Tasks 2.1-2.6)
- Complex multi-file refactoring
- When you have detailed specs

**GitHub Copilot:**
- Quick code completion
- Writing tests
- When already in VSCode

**Gemini CLI:**
- Simple scripts
- Command-line tools
- Quick prototypes

---

## 💡 BEST PRACTICES

### **1. Start with OpenAPI**
```yaml
# Design API first
OPENAPI.yaml → Generate mocks → Build frontend & backend in parallel
```

### **2. Use Task-Driven Development**
```
Don't: "Build the entire app"
Do: "Build Task 2.1: Implement POST /auth/login"
```

### **3. Keep AI-CONTEXT.md Updated**
```markdown
# Update "Current Phase" as you progress
Current Phase: Phase 2 - Authentication (Tasks 2.1-2.6)
                         ↑ Always current
```

### **4. Version Your OpenAPI**
```yaml
info:
  version: 1.0.0  # Increment when API changes
```

### **5. Combine Tools**
```
Use Claude Code for features
→ Use Copilot for refinements
→ Use Gemini for quick utilities
```

---

## 📊 TOKEN EFFICIENCY COMPARISON

### **Traditional Approach (No OpenAPI)**
```
Every AI session loads:
- Full API documentation: 3000 tokens
- Examples: 1000 tokens
- Context: 1000 tokens
Total per session: 5000 tokens
```

### **OpenAPI Approach (This Method)**
```
Every AI session loads:
- AI-CONTEXT.md: 400 tokens
- References OPENAPI.yaml (not loaded unless needed)
- AI reads YAML when implementing endpoints
Total per session: 400-800 tokens
```

**Savings: 85%!** 🎉

---

## 🔧 ADVANCED: OpenAPI-Driven Workflow

### **1. Design Phase**
```bash
# 1. Create OPENAPI.yaml with all endpoints
# 2. Validate
npx swagger-cli validate docs/OPENAPI.yaml

# 3. Start mock server
prism mock docs/OPENAPI.yaml &

# Mock runs on http://localhost:4010
```

### **2. Frontend Development**
```bash
# Generate TypeScript client
openapi-generator-cli generate \
  -i docs/OPENAPI.yaml \
  -g typescript-axios \
  -o frontend/src/api

# Use in React:
import { ItemsApi } from './api'
const api = new ItemsApi()
const items = await api.getItems()
```

### **3. Backend Development**
```bash
# With Claude Code:
claude
> Implement POST /auth/login from OPENAPI.yaml
  - Use bcrypt for passwords
  - Return JWT token
  - Match response schema exactly

# Claude reads OPENAPI.yaml and generates code that matches spec!
```

### **4. Test Contract**
```bash
# Ensure backend matches OpenAPI spec
npm install -g dredd
dredd docs/OPENAPI.yaml http://localhost:3000
```

---

## 🎁 BONUS: Quick Start Templates

### **For Express + TypeScript Backend**
```typescript
// Auto-validate against OpenAPI
import { OpenApiValidator } from 'express-openapi-validator'

app.use(
  OpenApiValidator.middleware({
    apiSpec: './docs/OPENAPI.yaml',
    validateRequests: true,
    validateResponses: true,
  })
)
```

### **For React Frontend**
```typescript
// Auto-generated client from OpenAPI
import { Configuration, ItemsApi } from './api'

const config = new Configuration({
  basePath: process.env.REACT_APP_API_URL,
  accessToken: getToken(),
})

const itemsApi = new ItemsApi(config)

// TypeScript types automatically match OpenAPI!
const response = await itemsApi.createItem({ title: 'New Item' })
```

---

## ✅ FINAL CHECKLIST

- [ ] Generated all 6 files from MegaPrompt
- [ ] Saved AI-CONTEXT.md in project root
- [ ] Saved other docs in `docs/` folder
- [ ] Validated OPENAPI.yaml with swagger-cli
- [ ] Started mock API with Prism (optional)
- [ ] Generated client SDK (optional)
- [ ] Chose AI tool (Claude Code / Copilot / Gemini)
- [ ] Started building from Task 1.1

---

## 🚀 YOU'RE READY!

This universal approach works with:
✅ Claude Code
✅ GitHub Copilot (ChatGPT)
✅ Gemini CLI
✅ Any OpenAPI-compatible tool

**Key Benefits:**
- 85% token savings
- API-first development
- Tool-agnostic workflow
- Auto-generated documentation
- Type-safe clients
- Contract testing

**Next Steps:**
1. Copy MegaPrompt
2. Add your project idea
3. Get 6 organized files
4. Start building! 🎯
