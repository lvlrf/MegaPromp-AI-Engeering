# 🔍 راهنمای انتخاب ابزار
## Claude Code vs GitHub Copilot vs Gemini CLI

---

## 📊 مقایسه سریع

| ویژگی | Claude Code | GitHub Copilot (ChatGPT) | Gemini CLI |
|-------|-------------|--------------------------|------------|
| **قیمت** | Pro: $20/ماه<br>Max: $100/ماه | $10/ماه | رایگان (محدود)<br>Pro: $20/ماه |
| **Context Window** | 200K tokens | ~16K tokens | 1M tokens (Gemini 1.5) |
| **Auto-load Context** | ✅ بله | ❌ خیر | ❌ خیر |
| **Multi-file Edit** | ✅ عالی | ⚠️ محدود | ⚠️ محدود |
| **OpenAPI Support** | ✅ عالی | ✅ خوب | ✅ عالی |
| **Persian Support** | ✅ عالی | ✅ خوب | ✅ متوسط |
| **IDE Integration** | Terminal | VSCode | Terminal |
| **Speed** | متوسط | سریع | سریع |
| **Code Quality** | عالی | خوب | خوب |

---

## 🎯 کدام یکی را انتخاب کنم؟

### **سناریو 1: پروژه کامل از صفر**
```
✅ BEST: Claude Code
چرا؟
- Multi-file editing قوی
- Context window بزرگ
- درک عمیق از architecture
- می‌تواند کل feature را بسازد

مثال:
"Build complete authentication system with JWT, 
password reset, email verification, and rate limiting"
→ Claude همه فایل‌ها را می‌سازد
```

### **سناریو 2: کار روی کد موجود**
```
✅ BEST: GitHub Copilot
چرا؟
- درون VSCode کار می‌کند
- Autocomplete سریع
- Inline suggestions
- Refactoring سریع

مثال:
در حال نوشتن هستید، Copilot پیشنهاد می‌دهد:
// Add validation
const validateTask = (task) => {
  // [TAB] → Copilot کل تابع را complete می‌کند
}
```

### **سناریو 3: Prototype سریع**
```
✅ BEST: Gemini CLI
چرا؟
- رایگان
- Context window عظیم (1M!)
- سریع
- خوب برای experimentation

مثال:
gemini-cli "Create a quick Express server with 3 endpoints"
→ کد آماده در 10 ثانیه
```

### **سناریو 4: API-First Development**
```
✅ BEST: Claude Code + OpenAPI
چرا؟
- می‌تواند OPENAPI.yaml را بخواند
- همه endpoints را implement می‌کند
- Response schemas را match می‌کند
- Validation logic می‌نویسد

مثال:
"Implement all endpoints from api.yaml with validation"
→ Backend کامل با error handling
```

### **سناریو 5: Learning/Practice**
```
✅ BEST: Gemini CLI (رایگان!)
چرا؟
- هزینه ندارد
- برای تمرین عالی است
- Context زیاد

بعداً: Copilot (در VSCode بهتره)
بعد از مهارت: Claude Code (برای پروژه‌های واقعی)
```

---

## 💰 Cost Comparison (پروژه متوسط)

### **پروژه: Task Manager با 20 endpoint**

#### **روش 1: فقط Claude Code**
```
Setup: 1 session (2K tokens)
Authentication: 3 sessions (6K tokens)
CRUD Tasks: 5 sessions (10K tokens)
Testing: 2 sessions (4K tokens)
Polish: 2 sessions (4K tokens)
───────────────────────────
Total: 26K tokens

با اشتراک Pro ($20/ماه):
26K tokens = ~8-10 features

با اشتراک Max ($100/ماه):
26K tokens = ~40-50 features

هزینه برای این پروژه: $0 (در محدودیت Pro)
```

#### **روش 2: فقط Copilot**
```
اشتراک: $10/ماه
محدودیت: unlimited autocomplete

برای این پروژه:
- نوشتن دستی بیشتر
- زمان: +50% بیشتر
- کیفیت: خوب اما نیاز به review بیشتر

هزینه: $10/ماه
```

#### **روش 3: فقط Gemini CLI (Free)**
```
محدودیت رایگان:
- 60 requests/minute
- 1500 requests/day

برای این پروژه:
- 30-40 request لازم است
- رایگان کافی است!

هزینه: $0
```

#### **روش 4: Hybrid (بهترین!)** ⭐
```
Claude Code: Features اصلی (10 sessions)
Copilot: Autocomplete و refactor (daily use)
Gemini: Quick scripts و utilities (free)

هزینه کل: $20/ماه (Claude Pro) + $10/ماه (Copilot)
= $30/ماه

اما:
- سریع‌ترین development
- بهترین کیفیت
- کمترین friction
```

---

## 🛠️ Workflow پیشنهادی (Hybrid)

### **Step 1: Planning & Design (Web Chat - رایگان!)**
```
در Claude Web یا ChatGPT Web:
1. MegaPrompt را اجرا کنید
2. 6 فایل بگیرید (PRD, TASKS, SPEC, ARCH, OPENAPI, AI-CONTEXT)
3. Review کنید

هزینه: $0 (web chat رایگان است!)
زمان: 5 دقیقه
```

### **Step 2: Setup (Claude Code)**
```bash
claude
> Setup project structure based on ARCHITECTURE.md
  - Initialize TypeScript
  - Setup Express
  - Configure MongoDB
  - Setup environment variables

هزینه: 1 session (~2K tokens)
زمان: 5 دقیقه
```

### **Step 3: Core Development (Claude Code + Copilot)**
```
روی VSCode با Copilot فعال:

# هر feature:
1. Claude Code می‌سازد (یک بار)
claude
> Build authentication system (Tasks 2.1-2.6)

2. Copilot refine می‌کند (continuous)
[در حال edit] → Copilot autocomplete

هزینه: 10-15 sessions Claude (~20K tokens)
زمان: 2-3 ساعت
```

### **Step 4: Utilities & Scripts (Gemini CLI - رایگان)**
```bash
# Sample data generation
gemini-cli "Generate 50 sample tasks as JSON"

# Test data
gemini-cli "Create test cases for authentication"

# Migration scripts
gemini-cli "Write MongoDB migration for tasks collection"

هزینه: $0
زمان: 10 دقیقه
```

### **Step 5: Polish (Copilot)**
```typescript
// در VSCode:
// - Error handling
// - Comments
// - Refactoring
// - Performance optimization

→ Copilot suggestions را accept کنید

هزینه: $0 (در اشتراک ماهانه)
زمان: 1 ساعت
```

**نتیجه:**
- **زمان کل:** ~4-5 ساعت (به جای 20 ساعت دستی!)
- **هزینه:** $30/ماه (برای unlimited projects)
- **کیفیت:** Production-ready

---

## 🎯 Recommendations برای سطوح مختلف

### **مبتدی (تازه شروع کرده)**
```
1️⃣ شروع: Gemini CLI (رایگان)
   - یاد بگیرید چطور prompt بنویسید
   - پروژه‌های کوچک بسازید
   
2️⃣ بعد: GitHub Copilot ($10/ماه)
   - VSCode setup کنید
   - با autocomplete راحت شوید
   
3️⃣ وقتی آماده شدید: Claude Code ($20/ماه)
   - پروژه‌های واقعی بسازید
```

### **متوسط (چند پروژه ساخته)**
```
✅ GitHub Copilot: روزانه
✅ Claude Code: برای features جدید
✅ Gemini CLI: برای quick tasks

Budget: $30/ماه
ROI: عالی
```

### **حرفه‌ای (Full-time developer)**
```
✅ Claude Code Max ($100/ماه): unlimited usage
✅ GitHub Copilot Business ($19/ماه): team features
✅ Gemini Pro ($20/ماه): big context

Budget: $139/ماه
ROI: استثنایی (صدها ساعت صرفه‌جویی)
```

---

## 📈 Token Usage Optimization

### **بد:**
```bash
# هر بار کل context می‌فرستید
claude
> [10 فایل paste می‌کنید]
  Build feature X

Token usage: 15K per session ❌
```

### **خوب:**
```bash
# فقط AI-CONTEXT.md در root
claude
> Build Task 2.1 from TASKS.md

Token usage: 300-500 per session ✅
Savings: 97%! 🎉
```

### **بهترین:**
```bash
# OpenAPI-first workflow
1. OpenAPI.yaml (one time)
2. Mock server (prism)
3. Frontend با generated client
4. Backend implement endpoints

Token usage: minimal
Frontend & backend parallel! ⚡
```

---

## 🎁 Pro Tips

### **Tip 1: Version Control**
```bash
# همه مستندات را commit کنید
git add docs/
git commit -m "Add project documentation"

# AI-CONTEXT.md هم commit شود
git add AI-CONTEXT.md
git commit -m "Add AI context file"

چرا؟
- تیم می‌توانند استفاده کنند
- CI/CD می‌تواند validate کند
- Version history دارید
```

### **Tip 2: Progressive Enhancement**
```
Week 1: Core features با Claude Code
Week 2: Refinement با Copilot
Week 3: Polish با Copilot
Week 4: Utilities با Gemini

= کیفیت ماکزیمم، هزینه مینیمم
```

### **Tip 3: Learning Path**
```
Month 1: Gemini CLI (free) - یاد بگیرید
Month 2: Copilot ($10) - عادت کنید
Month 3+: Claude Code ($20) - productive شوید

Total learning cost: $30 (فقط 2 ماه!)
```

### **Tip 4: Team Setup**
```
Junior devs: Gemini CLI / Copilot
Senior devs: Claude Code Max
Team lead: همه سه!

Result: هماهنگی عالی، هزینه بهینه
```

---

## ⚠️ هشدارها

### **Claude Code**
❌ **نکنید:**
- هر چیز کوچک را بپرسید (wasteful)
- بدون TASKS.md شروع کنید

✅ **بکنید:**
- از TASKS.md پیروی کنید
- AI-CONTEXT.md updated نگه دارید
- Batching: چند task مرتبط را با هم بسازید

### **GitHub Copilot**
❌ **نکنید:**
- هر suggestion را قبول کنید (review کنید!)
- برای complex features تکیه کنید

✅ **بکنید:**
- برای autocomplete و boilerplate
- برای refactoring
- برای test writing

### **Gemini CLI**
❌ **نکنید:**
- برای production code (review لازم است)
- بدون validation استفاده کنید

✅ **بکنید:**
- برای prototyping
- برای learning
- برای quick scripts

---

## 🎯 جمع‌بندی نهایی

### **بهترین Setup برای شما:**

```
اگر بودجه محدود دارید:
→ Gemini CLI (free) + مستندات خوب

اگر می‌خواهید productive باشید:
→ Copilot ($10) + Claude Web Chat (free)

اگر حرفه‌ای کار می‌کنید:
→ Claude Code Pro ($20) + Copilot ($10) = $30/ماه

اگر تیم دارید:
→ Claude Code Max ($100) + Copilot Business ($19 × team size)
```

### **با OpenAPI:**

```
همیشه OpenAPI را اول بنویسید!

OpenAPI → Mock → Frontend (parallel) Backend (parallel) → Integration → Test

= سریع‌ترین development ممکن! ⚡
```

---

**شما الان دارید:**

1. ✅ MegaPrompt جامع (کار با هر سه ابزار)
2. ✅ راهنمای OpenAPI کامل
3. ✅ مقایسه ابزارها
4. ✅ Workflows بهینه
5. ✅ Cost optimization tips

**آماده‌اید شروع کنید! 🚀**

سوال دارید؟ کدام tool را می‌خواهید شروع کنید؟
