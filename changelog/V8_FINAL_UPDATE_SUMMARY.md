# MegaPrompt V8 - آپدیت نهایی (تغییرات اعمال شده)

## ✅ تمام تغییرات درخواستی شما اعمال شد

---

## 1️⃣ نقش‌ها - لیست کامل و جامع

### ✅ نقش‌های اضافه شده:

**Business & Strategy:**
- ✅ VC Advisor (Venture Capital)
- ✅ Head of Product
- ✅ Program Manager
- ✅ Product Manager

**Technical Leadership:**
- ✅ Tech Lead
- ✅ Engineering Manager
- ✅ Solution Architect
- ✅ Staff/Principal Engineer

**Operations & Infrastructure:**
- ✅ DevOps Engineer
- ✅ MLOps Engineer
- ✅ DevSecOps Engineer
- ✅ SRE (Site Reliability Engineer)

**Quality & Security:**
- ✅ Security Reviewer
- ✅ Penetration Tester
- ✅ QA Lead
- ✅ QA Engineer

**Data & Analytics:**
- ✅ Data Engineer
- ✅ Data Analyst
- ✅ ML Engineer
- ✅ Analytics Engineer

**Project Management:**
- ✅ Project Manager
- ✅ Scrum Master
- ✅ Agile Coach

**Specialized:**
- ✅ Database Architect
- ✅ Performance Engineer
- ✅ UX Consultant
- ✅ Technical Writer
- ✅ Strategic Advisor

**جمع**: 30+ نقش تخصصی که AI می‌تواند بر اساس نیاز استفاده کند.

---

## 2️⃣ UI/UX قالب آماده - پرامپت Extraction

### ✅ اضافه شد: TEMPLATE ANALYSIS & EXTRACTION PROMPT

**کاربرد**:
وقتی قالب آماده دارید، این پرامپت رو به AI Agent Coding بدید.

**چی کار می‌کنه**:
```markdown
1. Structure Analysis
   - کدوم فولدرها و فایل‌ها نیاز دارم؟
   - کدوم‌ها رو باید پاک کنم؟

2. Component Mapping
   - هر کامپوننت چیکار می‌کنه؟
   - کدوم‌ها رو باید customize کنم؟

3. Data Flow Analysis
   - Data از کجا میاد؟
   - کدوم API endpoint ها لازمه؟

4. API Endpoints Needed
   - لیست endpoint های مورد نیاز برای backend

5. Backend Integration Points
   - کجاها باید به backend وصل بشه؟
   - چه تغییراتی لازمه؟

6. Customization Plan
   - مرحله به مرحله چیکار کنم؟

7. Output Files
   - TEMPLATE_INTEGRATION_GUIDE.md
   - BACKEND_API_SPEC.md
   - CUSTOMIZATION_CHECKLIST.md
```

**مثال خروجی**:
```markdown
# Template Integration Guide

## فایل‌های حذف شدنی:
- ❌ components/Pricing.jsx (نداریم)
- ❌ pages/Billing.jsx (نداریم)

## فایل‌های تغییر یافته:
- ✏️ config/api.js → تغییر API_URL
- ✏️ components/Header.jsx → logo + menu

## Backend API های لازم:
POST /api/auth/login
GET  /api/dashboard/stats
POST /api/tasks
...

## Customization Checklist:
- [ ] Change logo
- [ ] Update colors
- [ ] Connect to backend
- [ ] Test all flows
```

**فایل**: `docs/30_design/UI_MODE.md` (Mode 2)

---

## 3️⃣ PRD_IMPLEMENTATION_MATRIX.md - شرطی شد

### ✅ تغییر: فقط اگر پروژه بزرگه ساخته میشه

**قبل**:
```
همیشه ساخته می‌شد (حتی برای پروژه‌های کوچیک)
```

**الان**:
```
if (tasks > 20):
    ساخته می‌شود ✓
    دلیل: نیاز به traceability
else:
    ساخته نمی‌شود
    دلیل: overhead غیرضروری
```

**چرا این تغییر؟**
- پروژه کوچیک (10-15 task): نیاز نیست، اضافه‌ست
- پروژه متوسط/بزرگ (20+ task): خیلی مفیده

**مثال**:
```
پروژه با 47 task:
✅ PRD_IMPLEMENTATION_MATRIX.md ساخته می‌شه

پروژه با 12 task:
❌ PRD_IMPLEMENTATION_MATRIX.md ساخته نمی‌شه
```

**توضیحات در فایل**:
```markdown
PRD_IMPLEMENTATION_MATRIX.md
# CONDITIONAL: Only if tasks > 20
# Purpose: Track which tasks implement which features
# Small projects (<20 tasks): Skip this
```

---

## 4️⃣ تأیید برخلاف پیشنهاد - سیستم اخطار

### ✅ اضافه شد: User Override Warning System

**زمانی که شما برخلاف پیشنهاد AI انتخاب می‌کنید:**

**مثال**:
```
AI: "توصیه می‌کنم PostgreSQL"
شما: "MongoDB می‌خوام"

AI باید:
⚠️ "تو MongoDB انتخاب کردی (برخلاف پیشنهاد من).

دلیل پیشنهاد PostgreSQL:
- Data شما relational است
- JOIN queries سریع‌تر
- ACID transactions

عواقب MongoDB:
- JOIN queries پیچیده‌تر
- احتمال data inconsistency
- برای این use case بهینه نیست

ولی چون تو تایید کردی، من با MongoDB پیش می‌رم.

این تأیید نهایی تو هست؟
1. بله، با MongoDB بساز (ریسک‌ها رو می‌پذیرم)
2. فکر دوباره، بذار PostgreSQL

انتخاب؟"
```

**بعد از تأیید نهایی**:
```
AI: "باشه! با MongoDB می‌سازم.
این تصمیم توی DECISIONS.md ثبت می‌شه.

تا زمانی که تو تغییرش ندی، من همین رو دنبال می‌کنم."
```

**قوانین کلیدی**:
- ✅ همیشه عواقب رو نشون بده
- ✅ همیشه تأیید نهایی بگیر
- ✅ تصمیم رو توی DECISIONS.md ثبت کن
- ✅ بعد از تأیید، احترام بذار به تصمیم کاربر
- ✅ تا زمانی که کاربر تغییرش نده، همون رو دنبال کن

**فایل**: Global Non-Negotiables (Rule #5)

---

## 5️⃣ بدون اجازه تغییر نده - قانون قوی شد

### ✅ اضافه شد: NO UNAUTHORIZED CHANGES (CRITICAL)

**قانون طلایی**:
> "Never change, add, or remove ANYTHING without explicit user permission"

### ❌ ممنوع (بدون اجازه):
```
- حذف هیچ فایلی
- اضافه کردن هیچ فیچری
- حذف هیچ فیچری
- تغییر هیچ تصمیمی
- تغییر انتخاب تکنولوژی
- رد کردن هیچ مرحله‌ای
- فرض کردن کاربر چی می‌خواد
```

### ✅ مجاز:
```
- پیشنهاد دادن
- نشون دادن گزینه‌ها
- توضیح عواقب
- درخواست اجازه
- منتظر تأیید موندن
```

### مثال رفتار درست:
```
AI: "💡 پیشنهاد: Redis اضافه کنیم؟
     10x سریع‌تر می‌شه
     هزینه: +$5/month
     
     می‌خوای اضافه کنم؟"

شما: "نه"

AI: "باشه! بدون Redis ادامه می‌دم."
✅ Redis اضافه نمی‌کنه
```

### مثال رفتار غلط:
```
AI (فکر می‌کنه): "Redis خوبه، خودم اضافه‌ش می‌کنم"
[Adds Redis without asking]
❌ نقض قانون!
```

### عواقب نقض:
```
اگر AI بدون اجازه چیزی اضافه/حذف/تغییر داد:
1. فوراً به کاربر اطلاع بده
2. عذرخواهی کن
3. تغییر رو برگردون
4. بپرس کاربر چی می‌خواد
```

**فایل**: Global Non-Negotiables (Rule #6)

---

## 6️⃣ مدل‌ها - لیست کامل + ترکیبی

### ✅ لیست کامل مدل‌ها:

#### Claude (Anthropic):
- Claude Sonnet 4.5 ⭐ (متوازن)
- Claude Opus 4.1 (قوی‌ترین)
- Claude Haiku 4.5 (سریع‌ترین)

#### OpenAI:
- GPT-4o (قوی در UI/UX)
- o1 (reasoning بالا)
- o1-mini (سریع‌تر)
- GPT-4 Turbo

#### Google:
- Gemini 2.0 Pro (جدید)
- Gemini 2.0 Flash (سریع، ارزان)
- Gemini 1.5 Pro

#### xAI:
- Grok 2 (real-time data)

#### Others:
- DeepSeek-V3 (open-source)
- Qwen 2.5 (خوب در code)

### ✅ پیشنهادات ترکیبی:

AI تحلیل می‌کنه و 4 strategy پیشنهاد می‌ده:

**Strategy 1: Quality-First**
```
High tasks → Claude Opus 4.1
Medium tasks → Claude Sonnet 4.5
Low tasks → Gemini Flash 2.0

زمان: 10h | هزینه: $32 | کیفیت: ★★★★★
```

**Strategy 2: Balanced** ⭐ (توصیه)
```
High tasks → Claude Opus 4.1
Medium tasks → GPT-4o
Low tasks → Gemini Flash 2.0

زمان: 9h | هزینه: $28 | کیفیت: ★★★★☆
```

**Strategy 3: Budget-Optimized**
```
High tasks → Claude Sonnet 4.5
Medium tasks → Gemini Flash 2.0
Low tasks → Gemini Flash 2.0

زمان: 12h | هزینه: $18 | کیفیت: ★★★☆☆
```

**Strategy 4: Speed-Optimized** (موازی)
```
همه tasks به صورت موازی:
- Claude Opus: 2 tasks
- Claude Sonnet: 8 tasks
- GPT-4o: 7 tasks
- Gemini Flash: 30 tasks

زمان: 5h | هزینه: $35 | کیفیت: ★★★★☆
```

### ✅ تخصص مدل‌ها:

```
🏗️ Architecture → Claude Opus, o1
🔒 Security → Claude Opus, GPT-4o
⚙️ Backend → Claude Sonnet, GPT-4o
🎨 Frontend → GPT-4o, Claude Sonnet
📱 Mobile → GPT-4o, Gemini Pro
🧪 Testing → Gemini Flash, Claude Haiku
📊 Data → Claude Sonnet, Gemini Pro
🚀 DevOps → Claude Sonnet, GPT-4o
🤖 ML/AI → Gemini Pro, Claude Opus
⚡ Prototypes → Gemini Flash, Claude Haiku
🌐 Real-time → Grok 2
```

### ✅ جدول مقایسه:

| Model              | Speed  | Cost   | Quality | Best For              |
|--------------------|--------|--------|---------|------------------------|
| Claude Opus 4.1    | ●●●○○  | $$$$$  | ★★★★★   | Complex reasoning      |
| Claude Sonnet 4.5  | ●●●●○  | $$$    | ★★★★☆   | Balanced tasks        |
| Claude Haiku 4.5   | ●●●●●  | $      | ★★★☆☆   | Simple, fast          |
| GPT-4o             | ●●●●○  | $$$$   | ★★★★☆   | UI/UX, creativity     |
| o1                 | ●●○○○  | $$$$$$ | ★★★★★   | Hard reasoning        |
| o1-mini            | ●●●○○  | $$$    | ★★★★☆   | Fast reasoning        |
| Gemini 2.0 Pro     | ●●●●○  | $$$    | ★★★★☆   | Multimodal, code      |
| Gemini Flash 2.0   | ●●●●●  | $      | ★★★☆☆   | Volume tasks          |
| Grok 2             | ●●●●●  | $$$    | ★★★☆☆   | Real-time             |

**فایل**: Multi-Agent Decision Framework

---

## 📊 خلاصه کلی تغییرات

### ✅ اضافه شد:
1. ✅ 30+ نقش تخصصی
2. ✅ Template Extraction Prompt (UI/UX Mode 2)
3. ✅ PRD_IMPLEMENTATION_MATRIX شرطی (tasks > 20)
4. ✅ User Override Warning System
5. ✅ NO UNAUTHORIZED CHANGES (قوی شد)
6. ✅ لیست کامل مدل‌ها (10+ مدل)
7. ✅ 4 Strategy ترکیبی
8. ✅ جدول تخصص مدل‌ها
9. ✅ جدول مقایسه مدل‌ها

### ✅ تغییر کرد:
- نقش‌ها: از محدود به جامع (30+ نقش)
- UI/UX: پرامپت extraction برای قالب آماده
- PRD_IMPLEMENTATION_MATRIX: از همیشه به شرطی
- اخطارها: سیستم اخطار قوی برای override
- مدل‌ها: از ساده به جامع با ترکیب

### ✅ هیچ چیز پاک نشد:
- همه فایل‌های قبلی نگه داشته شد
- همه ساختار قبلی محفوظ ماند
- فقط بهبود و اضافه شد

---

## 🎯 وضعیت نهایی

### تمام درخواست‌های شما:

1. ✅ نقش‌ها جامع (DevOps, MLOps, VC, etc.)
2. ✅ UI/UX قالب آماده (پرامپت extraction)
3. ✅ PRD_IMPLEMENTATION_MATRIX واضح شد
4. ✅ اخطار برای override
5. ✅ بدون اجازه تغییر نده (قوی شد)
6. ✅ مدل‌های کامل + ترکیبی

### فایل‌های تولید شده:

1. **MEGAPROMPT_V8_FINAL.md** - نسخه نهایی با تمام تغییرات
2. **V8_FINAL_UPDATE_SUMMARY.md** - این سند (خلاصه تغییرات)

---

## 🚀 آماده استفاده!

MegaPrompt V8 با تمام تغییرات درخواستی شما کامل شد.

**هیچ سوال یا تغییر دیگری نیست؟**

اگه تمام شد، می‌تونی ازش استفاده کنی! 🎉
