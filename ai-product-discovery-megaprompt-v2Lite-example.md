# 🎯 نمونه عملی کامل
## از توضیحات پراکنده تا برنامه آماده

---

## 📝 گام 1: ورودی شما (می‌تواند پراکنده باشد)

```
سلام، میخوام یه اپ بسازم برای مدیریت هزینه‌ها

باید بتونم هزینه‌هامو ثبت کنم
دسته‌بندی داشته باشه مثل غذا، حمل و نقل، سرگرمی
یه صفحه dashboard که نشون بده این ماه چقدر خرج کردم
نمودار هم بخوایم
باید بتونم فیلتر کنم بر اساس تاریخ
export به PDF میخوام
احراز هویت با گوگل
از React استفاده کنیم
باید dark mode داشته باشه
responsive باشه برای موبایل
backend با Node.js
دیتابیس MongoDB
یه budget limit بذارم که اگه بیشتر خرج کردم بهم اطلاع بده
notification هم بخوایم
اینا رو هم باید داشته باشیم:
- تگ به هزینه‌ها اضافه کنم
- search
- یه صفحه reports
- backup اتوماتیک
آره و باید بتونم recurring expenses تعریف کنم
مثلاً اجاره هر ماه خودکار اضافه شه
```

---

## 🤖 گام 2: MegaPrompt را اجرا کنید

در چت وب Claude:

1. **Copy کنید:** تمام محتوای Artifact قبلی ("Smart Project Generator MegaPrompt")
2. **Paste کنید** در چت
3. **اضافه کنید:** متن بالا را در انتها بچسبانید

---

## 📤 گام 3: خروجی Claude (5 فایل منظم)

### ─────────────────────────────────
## 📄 PRD.md
### ─────────────────────────────────

```markdown
# اپلیکیشن مدیریت هزینه شخصی

## 🎯 هدف پروژه
یک ابزار مدیریت مالی شخصی که به کاربران کمک می‌کند هزینه‌های خود را ثبت، دسته‌بندی، و تحلیل کنند تا کنترل بهتری بر مخارج خود داشته باشند.

## 👥 کاربران هدف
افراد و خانواده‌هایی که می‌خواهند:
- هزینه‌های روزانه خود را پیگیری کنند
- درک بهتری از الگوی مصرف خود داشته باشند
- بودجه ماهانه تعیین کنند و به آن پایبند باشند
- از هشدار هوشمند هنگام تجاوز از بودجه بهره‌مند شوند

## ✨ ویژگی‌های اصلی

### 1. مدیریت هزینه‌ها
- ثبت هزینه با عنوان، مبلغ، تاریخ، و توضیحات
- دسته‌بندی (غذا، حمل و نقل، سرگرمی، و غیره)
- افزودن تگ به هزینه‌ها برای سازماندهی بهتر
- جستجوی سریع در هزینه‌ها

### 2. هزینه‌های تکرارشونده
- تعریف هزینه‌های ثابت ماهانه (مثل اجاره، اشتراک‌ها)
- افزودن خودکار به لیست هزینه‌ها

### 3. بودجه‌بندی و هشدار
- تعیین حد بودجه ماهانه
- نمایش پیشرفت در dashboard
- ارسال notification هنگام نزدیک شدن یا تجاوز از بودجه

### 4. داشبورد و تحلیل
- نمایش خلاصه هزینه‌های ماه جاری
- نمودار دایره‌ای برای توزیع هزینه‌ها بر اساس دسته
- نمودار خطی برای روند هزینه‌ها
- فیلتر بر اساس تاریخ (روز، هفته، ماه)

### 5. گزارش‌گیری
- صفحه reports با آمار تفصیلی
- export به PDF
- پشتیبان‌گیری خودکار از داده‌ها

## 🎨 رابط کاربری
- طراحی responsive برای موبایل و دسکتاپ
- پشتیبانی از Dark Mode
- رابط کاربری ساده و سریع
- نمایش بصری داده‌ها با نمودارها

## 🔧 نیازمندی‌های فنی
- **Frontend:** React 18 با TypeScript
- **Backend:** Node.js + Express
- **Database:** MongoDB
- **احراز هویت:** Google OAuth
- **Notifications:** Web Push Notifications
- **Export:** PDF generation library

## 📊 معیارهای موفقیت
- ثبت هزینه در کمتر از 10 ثانیه
- نمایش dashboard در کمتر از 2 ثانیه
- دقت 100% در محاسبات مالی
- پشتیبانی از 1000+ تراکنش برای هر کاربر

## 🚫 خارج از محدوده (فعلاً)
- اتصال به بانک و sync خودکار
- مدیریت چند کاربر/خانوادگی
- پیش‌بینی هزینه‌های آینده با AI
- مدیریت دارایی‌ها و سرمایه‌گذاری

## 📝 یادداشت‌های اضافی
این نسخه اول (MVP) است. تمرکز بر سادگی و سرعت استفاده.
```

### ─────────────────────────────────
## 📄 TASKS.md
### ─────────────────────────────────

```markdown
# 🎯 Development Tasks

## Phase 1: Setup & Foundation (2-3 hours)
- [ ] 1.1: Initialize React + TypeScript + Vite project
- [ ] 1.2: Setup Tailwind CSS with dark mode support
- [ ] 1.3: Create basic folder structure (components, pages, hooks, utils)
- [ ] 1.4: Setup Express backend with TypeScript
- [ ] 1.5: Connect MongoDB and create connection utility
- [ ] 1.6: Setup environment variables (.env) for both frontend/backend

## Phase 2: Authentication (3-4 hours)
- [ ] 2.1: Implement Google OAuth on backend
- [ ] 2.2: Create JWT token generation and validation
- [ ] 2.3: Build Login page with Google sign-in button
- [ ] 2.4: Implement protected route wrapper component
- [ ] 2.5: Store user session in localStorage/cookies
- [ ] 2.6: Create logout functionality

## Phase 3: Core Expense Management (5-6 hours)
- [ ] 3.1: Design MongoDB schema for expenses (title, amount, category, date, tags, userId)
- [ ] 3.2: Create backend API: POST /api/expenses (create expense)
- [ ] 3.3: Create backend API: GET /api/expenses (list expenses with filters)
- [ ] 3.4: Create backend API: PUT /api/expenses/:id (update expense)
- [ ] 3.5: Create backend API: DELETE /api/expenses/:id (delete expense)
- [ ] 3.6: Build "Add Expense" form component (with category dropdown, tag input)
- [ ] 3.7: Build "Expense List" component with edit/delete buttons
- [ ] 3.8: Implement search functionality in frontend

## Phase 4: Categories & Tags (2 hours)
- [ ] 4.1: Create predefined categories (Food, Transport, Entertainment, etc.)
- [ ] 4.2: Build category selector component
- [ ] 4.3: Implement tag input with autocomplete
- [ ] 4.4: Add category/tag filter in expense list

## Phase 5: Recurring Expenses (2-3 hours)
- [ ] 5.1: Design MongoDB schema for recurring expenses
- [ ] 5.2: Create backend API: POST /api/recurring-expenses
- [ ] 5.3: Create backend API: GET /api/recurring-expenses
- [ ] 5.4: Build "Add Recurring Expense" form
- [ ] 5.5: Implement cron job to auto-add recurring expenses monthly

## Phase 6: Budget & Notifications (3-4 hours)
- [ ] 6.1: Add budget field to user schema
- [ ] 6.2: Create backend API: POST /api/user/budget
- [ ] 6.3: Build budget setting component in settings page
- [ ] 6.4: Calculate total spent in current month
- [ ] 6.5: Show budget progress bar in dashboard
- [ ] 6.6: Implement notification service (web push)
- [ ] 6.7: Trigger notification when 80%, 100% of budget reached

## Phase 7: Dashboard & Visualizations (4-5 hours)
- [ ] 7.1: Install chart library (recharts or chart.js)
- [ ] 7.2: Build dashboard layout
- [ ] 7.3: Create "Total Spent This Month" card
- [ ] 7.4: Create pie chart for expenses by category
- [ ] 7.5: Create line chart for daily spending trend
- [ ] 7.6: Implement date range filter (day/week/month)
- [ ] 7.7: Add loading states for all data fetches

## Phase 8: Reports & Export (2-3 hours)
- [ ] 8.1: Create Reports page with detailed statistics
- [ ] 8.2: Calculate average daily/weekly/monthly spending
- [ ] 8.3: Show top categories and tags
- [ ] 8.4: Install PDF generation library (jsPDF or Puppeteer)
- [ ] 8.5: Implement "Export to PDF" button
- [ ] 8.6: Design PDF template with charts and tables

## Phase 9: Backup & Settings (2 hours)
- [ ] 9.1: Create Settings page
- [ ] 9.2: Implement dark/light mode toggle
- [ ] 9.3: Add backup functionality (export all data as JSON)
- [ ] 9.4: Implement data import from backup file
- [ ] 9.5: Add automatic daily backup to user's storage

## Phase 10: Polish & Deploy (3-4 hours)
- [ ] 10.1: Add loading spinners and skeleton screens
- [ ] 10.2: Implement error boundaries
- [ ] 10.3: Add toast notifications for success/error messages
- [ ] 10.4: Test responsive design on mobile/tablet
- [ ] 10.5: Optimize images and bundle size
- [ ] 10.6: Setup production environment variables
- [ ] 10.7: Deploy backend to Railway/Render
- [ ] 10.8: Deploy frontend to Vercel
- [ ] 10.9: Test production deployment

---

## 📋 How to Use with Claude Code

### Starting a task:
```bash
claude
> Build Task 1.1 from TASKS.md: Initialize React + TypeScript + Vite project. Follow CLAUDE.md for standards.
```

### After completing:
```bash
> Task 1.1 done. Review code and start Task 1.2.
```

### If you need to deviate:
```bash
> Task 3.2 needs modification: also add pagination to GET /api/expenses
```
```

### ─────────────────────────────────
## 📄 SPEC.md
### ─────────────────────────────────

```markdown
# Technical Specification

## Core Goal
Personal expense management application with budgeting, analytics, and notifications.

## Tech Stack
- **Frontend:** React 18 + TypeScript + Vite + Tailwind CSS
- **Backend:** Node.js 18+ + Express + TypeScript
- **Database:** MongoDB Atlas
- **Auth:** Google OAuth 2.0 + JWT
- **Charts:** Recharts
- **PDF:** jsPDF
- **Notifications:** Web Push API
- **Deploy:** Frontend (Vercel), Backend (Railway)

## Key Features (Technical View)

### 1. Authentication System
- Google OAuth 2.0 flow
- JWT token with 7-day expiry
- Refresh token mechanism
- Protected API routes with middleware

### 2. Expense CRUD
- RESTful API endpoints
- Input validation (Joi/Zod)
- Pagination (20 items per page)
- Search with text indexing
- Soft delete (keep records for backup)

### 3. Recurring Expenses
- Cron job runs daily at 00:00 UTC
- Checks all active recurring expenses
- Auto-creates expense if date matches
- Logs creation for audit

### 4. Budget Tracking
- Real-time calculation of spent amount
- Websocket or polling for live updates
- Notification triggers at 80%, 100%, 120%
- Budget resets on 1st of each month

### 5. Analytics & Reports
- Aggregate queries for category totals
- Date range queries with indexes
- Chart data serialization (JSON)
- PDF generation on-demand (not cached)

## Data Requirements

### User Schema
```typescript
{
  _id: ObjectId
  email: string (unique)
  name: string
  googleId: string (unique)
  budget: number
  createdAt: Date
  updatedAt: Date
}
```

### Expense Schema
```typescript
{
  _id: ObjectId
  userId: ObjectId (indexed)
  title: string
  amount: number
  category: string (enum)
  tags: string[]
  date: Date (indexed)
  isRecurring: boolean
  recurringId: ObjectId (optional)
  createdAt: Date
  updatedAt: Date
  deletedAt: Date (optional, for soft delete)
}
```

### RecurringExpense Schema
```typescript
{
  _id: ObjectId
  userId: ObjectId
  title: string
  amount: number
  category: string
  dayOfMonth: number (1-31)
  isActive: boolean
  createdAt: Date
}
```

## Performance Requirements
- Dashboard load: < 2 seconds
- Expense creation: < 500ms
- Search results: < 1 second
- PDF generation: < 5 seconds
- Support 1000+ expenses per user

## Security Requirements
- HTTPS only in production
- JWT stored in httpOnly cookies
- Input sanitization (prevent NoSQL injection)
- Rate limiting: 100 requests/15min per IP
- CORS restricted to frontend domain
- Environment variables for secrets

## Integration Points
- Google OAuth API (https://accounts.google.com)
- Web Push Notifications API (browser)
- MongoDB Atlas (cloud database)
```

### ─────────────────────────────────
## 📄 ARCHITECTURE.md
### ─────────────────────────────────

```markdown
# System Architecture

## High-Level Flow

```
┌──────────────────────────────────────────────┐
│            User (Browser)                    │
│  ┌────────────────────────────────────────┐ │
│  │  React Frontend                        │ │
│  │  ├─ Pages (Dashboard, Reports, etc)    │ │
│  │  ├─ Components (ExpenseForm, Charts)   │ │
│  │  └─ Hooks (useAuth, useFetch)          │ │
│  └────────────────────────────────────────┘ │
└──────────────┬───────────────────────────────┘
               │ HTTPS/JSON + JWT
               ↓
┌──────────────────────────────────────────────┐
│          Express API Server                  │
│  ┌────────────────────────────────────────┐ │
│  │  Routes:                               │ │
│  │  ├─ POST   /auth/google                │ │
│  │  ├─ GET    /api/expenses               │ │
│  │  ├─ POST   /api/expenses               │ │
│  │  ├─ PUT    /api/expenses/:id           │ │
│  │  ├─ DELETE /api/expenses/:id           │ │
│  │  ├─ POST   /api/recurring-expenses     │ │
│  │  ├─ POST   /api/user/budget            │ │
│  │  └─ GET    /api/reports/pdf            │ │
│  └────────────────────────────────────────┘ │
│  Middleware: Auth, Validation, ErrorHandler  │
└──────────────┬───────────────────────────────┘
               │ MongoDB Protocol
               ↓
┌──────────────────────────────────────────────┐
│        MongoDB Atlas (Cloud)                 │
│  ┌────────────────────────────────────────┐ │
│  │  Collections:                          │ │
│  │  • users                               │ │
│  │  • expenses (indexed: userId, date)    │ │
│  │  • recurringExpenses                   │ │
│  │  • notifications                       │ │
│  └────────────────────────────────────────┘ │
└──────────────────────────────────────────────┘

        ┌─────────────────────────┐
        │  Cron Job (Node-Cron)   │ Runs daily
        │  Check & Create         │ at 00:00 UTC
        │  Recurring Expenses     │
        └─────────────────────────┘
```

## Component Breakdown

### Frontend Components
```
src/
├── components/
│   ├── ui/
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   └── Modal.tsx
│   ├── features/
│   │   ├── ExpenseForm.tsx
│   │   ├── ExpenseList.tsx
│   │   ├── BudgetProgress.tsx
│   │   ├── CategoryChart.tsx
│   │   └── TrendChart.tsx
│   └── layouts/
│       ├── Header.tsx
│       ├── Sidebar.tsx
│       └── MainLayout.tsx
├── pages/
│   ├── Login.tsx
│   ├── Dashboard.tsx
│   ├── Expenses.tsx
│   ├── Reports.tsx
│   └── Settings.tsx
├── hooks/
│   ├── useAuth.ts
│   ├── useExpenses.ts
│   └── useBudget.ts
└── utils/
    ├── api.ts (axios instance)
    └── helpers.ts
```

### Backend Services
```
backend/
├── routes/
│   ├── auth.routes.ts
│   ├── expense.routes.ts
│   ├── recurring.routes.ts
│   └── report.routes.ts
├── controllers/
│   ├── auth.controller.ts
│   ├── expense.controller.ts
│   └── report.controller.ts
├── models/
│   ├── User.model.ts
│   ├── Expense.model.ts
│   └── RecurringExpense.model.ts
├── middleware/
│   ├── auth.middleware.ts
│   ├── validation.middleware.ts
│   └── error.middleware.ts
├── services/
│   ├── notification.service.ts
│   ├── pdf.service.ts
│   └── cron.service.ts
└── utils/
    └── db.ts
```

## Data Models (TypeScript)

```typescript
// User
interface User {
  _id: string
  email: string
  name: string
  googleId: string
  budget: number
  createdAt: Date
  updatedAt: Date
}

// Expense
interface Expense {
  _id: string
  userId: string
  title: string
  amount: number
  category: Category
  tags: string[]
  date: Date
  isRecurring: boolean
  recurringId?: string
  createdAt: Date
  updatedAt: Date
}

// Category
enum Category {
  FOOD = 'food',
  TRANSPORT = 'transport',
  ENTERTAINMENT = 'entertainment',
  UTILITIES = 'utilities',
  HEALTHCARE = 'healthcare',
  SHOPPING = 'shopping',
  OTHER = 'other'
}

// RecurringExpense
interface RecurringExpense {
  _id: string
  userId: string
  title: string
  amount: number
  category: Category
  dayOfMonth: number
  isActive: boolean
  createdAt: Date
}
```

## Key Interactions

### 1. User Login
```
User clicks "Sign in with Google"
→ Frontend redirects to Google OAuth
→ Google redirects back with auth code
→ Backend exchanges code for user info
→ Backend creates/finds user in DB
→ Backend returns JWT token
→ Frontend stores token & redirects to Dashboard
```

### 2. Add Expense
```
User fills form & clicks "Add"
→ Frontend validates input
→ POST /api/expenses with JWT
→ Backend verifies token
→ Backend saves to DB
→ Backend checks budget & triggers notification if needed
→ Backend returns created expense
→ Frontend updates UI & shows toast
```

### 3. View Dashboard
```
User navigates to Dashboard
→ Frontend fetches GET /api/expenses?month=current
→ Backend queries expenses for current month
→ Backend calculates totals by category
→ Backend returns data
→ Frontend renders charts
```

### 4. Auto-Create Recurring Expense
```
Cron job runs at 00:00 UTC
→ Fetch all active recurring expenses
→ Check if dayOfMonth matches today
→ For each match: create new expense
→ Log creation
→ Send notification to user
```
```

### ─────────────────────────────────
## 📄 CLAUDE.md
### ─────────────────────────────────

```markdown
# Quick Reference

## Stack
React 18 + TypeScript + Tailwind | Node.js + Express + MongoDB

## Commands
```bash
# Frontend
npm run dev           # localhost:5173
npm run build
npm run preview

# Backend
npm run dev           # localhost:3000
npm run build
npm start

# Database
npm run db:seed       # Add sample data
```

## File Structure
```
expense-app/
├── frontend/         # React app
├── backend/          # Express API
└── docs/            # All documentation
```

## Code Standards
✅ TypeScript strict mode
✅ Functional components with hooks
✅ Error handling in try/catch
✅ Input validation on backend
✅ Responsive design (Tailwind)

❌ No console.log in production
❌ No inline styles
❌ No any type in TypeScript
❌ No hardcoded values

## Data Flow
User → Frontend → API → MongoDB

## Current Focus
Building authentication system (Tasks 2.1-2.6)

## Environment Variables
```env
# Frontend (.env)
VITE_API_URL=http://localhost:3000
VITE_GOOGLE_CLIENT_ID=xxx

# Backend (.env)
PORT=3000
MONGODB_URI=mongodb://...
GOOGLE_CLIENT_ID=xxx
GOOGLE_CLIENT_SECRET=xxx
JWT_SECRET=xxx
```

## Quick Debugging
- Check browser console for frontend errors
- Check terminal for backend errors
- MongoDB logs in Atlas dashboard
- Use Postman for API testing
```

---

## ✅ شما الان دارید:

1. **PRD.md** → برای توضیح به دیگران (زبان انسانی)
2. **TASKS.md** → لیست کامل تسک‌های مرتب
3. **SPEC.md** → جزئیات فنی
4. **ARCHITECTURE.md** → نمودار و ساختار
5. **CLAUDE.md** → خلاصه برای Claude Code

---

## 🚀 گام بعدی:

```bash
# 1. فایل‌ها را ذخیره کنید
mkdir expense-app
cd expense-app
mkdir docs

# docs/PRD.md, docs/TASKS.md, etc. را ذخیره کنید
# CLAUDE.md را در root بگذارید

# 2. Claude Code را شروع کنید
claude

# 3. اولین تسک را بسازید
> Build Task 1.1 from TASKS.md
```

---

## 💰 هزینه این روش:

| مرحله | توکن |
|-------|------|
| تولید 5 فایل (چت وب) | ~2,000 |
| هر session Claude Code | ~300 (فقط CLAUDE.md) |
| **10 session Claude Code** | ~5,000 |
| **جمع کل** | **~7,000 توکن** |

### مقایسه با روش سنتی:
| روش سنتی | این روش | صرفه‌جویی |
|----------|---------|-----------|
| 50,000 توکن | 7,000 توکن | **86%** 🎉 |

---

این همان چیزی است که می‌خواستید! 🎯
