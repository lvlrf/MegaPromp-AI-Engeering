# MegaPrompt AI Engineering (Vibe Coding Playbook)

این ریپو برای این ساخته شده که «مستنداتِ اجرایی» تولید کنید تا ایجنت‌های کدنویسی (Codex / Claude / Gemini و …) کمترین سؤال را بپرسند و مرحله‌به‌مرحله جلو بروند.

## خروجیِ مطلوبِ مستندات برای جلوگیری از Block شدن ایجنت

اگر فقط PRD/Spec بنویسید، ایجنت معمولاً روی «تصمیم‌های اجرایی» گیر می‌کند (Tech Stack / Run Commands / ساختار مونوریپو / پورت‌ها و env).  
پس در کنار PRD، باید دو چیز را *قفل* کنید:

1) **Foundational Setup Decisions (LOCKED)**  
2) **Implementation Bindings (Traceability Matrix)**

این دو مورد باعث می‌شوند ایجنت مجبور نشود RFC بزند و متوقف شود.

---

## Quick Start (برای استفاده با Codex CLI)

1) از داخل ریپوی پروژه‌تان (نه این ریپو) فایل‌های زیر را داشته باشید:
- `docs/PRD.md` (برای انسان، فارسی)
- `docs/PRD_AI.md` (برای ایجنت، مختصر و اجرایی)
- `docs/PRD_NOTES.md` (لاگ اجرایی + تصمیم‌ها)
- `docs/PRD_IMPLEMENTATION_MATRIX.md` (Implementation Bindings)
- `docs/TASKS.md` (تسک‌های Atomic)

2) به Codex این پرامپت را بدهید (کپی/پیست):
- ابتدا Phase 1 فقط خواندن و فهمیدن
- اگر تصمیم‌های اجرایی قفل نشده‌اند: فقط در `docs/PRD_NOTES.md` بخش «LOCKED» را بساز و گزینه‌ها را پیشنهاد بده و **STOP**
- اگر قفل هستند: Plan بنویس، سپس Execute

نمونه پرامپت:
```text
Hard rules:
- Do NOT add new features beyond docs.
- Phase 1: read-only (no code changes).
- If you are missing any "Foundational Setup Decisions", write them as options under docs/PRD_NOTES.md > LOCKED DECISIONS and STOP.
- Otherwise produce a small-task plan (Phase 2) then execute (Phase 3).
- Maintain docs/PRD_NOTES.md with:
  - repo snapshot
  - extracted requirements checklist
  - LOCKED decisions
  - Implementation Bindings (or link to PRD_IMPLEMENTATION_MATRIX.md)
  - assumptions
  - plan
  - progress log with checkboxes (🔲 / ✅)

Phase 1 — Read & Understand:
1) Read docs/PRD_AI.md, docs/SPEC.md, docs/TASKS.md, docs/RULES.md, docs/ARCHITECTURE.md, docs/UIUX.md, docs/OPENAPI.yaml (if exists).
2) Inspect repo structure and identify missing/blocked parts.
3) Summarize how to run (commands, ports, env).
No code changes yet.

Phase 2 — Plan:
Write a step-by-step plan with atomic tasks + verification commands.
Do not implement until plan is written.

Phase 3 — Execute:
Execute task-by-task, run verification commands, report results.
Only ask me if truly blocked by missing critical info; otherwise make the safest assumption and record it.
```

---

## انتخاب Reasoning Level در Codex (Low/Medium/High/Extra High)

قاعده عملی:
- **Medium (default)**: ساخت اسکلت پروژه، CRUDهای ساده، روتین روزمره.
- **High**: طراحی معماری، همگام‌سازی پیچیده، مایگریشن‌ها، سناریوهای چندمرحله‌ای، دیباگ سخت.
- **Extra high**: مسائل پیچیده با ریسک بالا (امنیت، پرداخت، کانکارنسی/لاک، Race condition، طراحی دیتابیس جدی).
- **Low**: تغییرات کوچک، به‌روزرسانی متن، ریفکتور محدود.

---

## Token / Cost (مصرف توکن را چطور ببینم؟)

- اگر Codex CLI را با API Key اجرا می‌کنید، مصرف و هزینه معمولاً از **Usage/Billing** همان اکانت API قابل مشاهده است (داشبورد OpenAI).
- اگر خروجیِ «usage summary» داخل ترمینال ندارید، بهترین راه همان داشبورد Usage است.
- پیشنهاد عملی: هر Session را کوتاه و مرحله‌ای نگه دارید (Plan → اجرای چند تسک)، تا ردیابی هزینه و کنترل مسیر ساده‌تر شود.

---

## Skills یعنی چی و آیا لازم است؟

Skill یعنی «دستورالعمل‌های تکرارشونده و قابل‌استفاده مجدد» (مثل استاندارد تست، ساختار فولدر، الگوی API error handling، قواعد Git).  
دو روش رایج:
1) **Skills آماده (عمومی)**: خوب است، اما به پروژه شما کامل فیت نمی‌شود.
2) **Skills اختصاصی شما**: بهترین گزینه برای کاهش سؤال و جلوگیری از Loop.

پیشنهاد این ریپو: skills را به‌شکل فایل‌های کوتاه Markdown در پروژه‌تان نگه دارید (مثلاً `docs/skills/*.md`) و در `AGENTS.md` یا `docs/PRD_AI.md` به آن‌ها ارجاع بدهید.

---

## اجرای Codex روی ویندوز: غیر از CMD و PowerShell چه گزینه‌هایی دارم؟

- Windows Terminal (ترکیب چند شِل)
- VS Code Integrated Terminal
- Git Bash
- Cmder / ConEmu
- WSL (Ubuntu روی ویندوز) — برای تجربه نزدیک‌تر به لینوکس

---

## کار همزمان با دو ایجنت (برای سرعت)

هدف: تداخل نخورند.

الگوی پیشنهادی:
1) **تقسیم دامنه** (Backend vs Frontend vs Docs) و ممنوعیت دست زدن به فایل‌های مشترک.
2) هر ایجنت یک «Lock List» در `docs/PRD_NOTES.md` می‌نویسد:
   - «این فایل‌ها را من تغییر می‌دهم»
3) اگر Git دارید:
   - هر ایجنت روی یک branch یا worktree جدا.
4) ادغام:
   - یک نفر (Integrator) فقط merge و رفع conflict را انجام می‌دهد.

نمونه پرامپت برای ایجنت دوم:
```text
You are Agent B. Your scope is ONLY apps/web and docs/30_design.
Do not touch backend or shared OpenAPI unless explicitly assigned.
Before any change, write your lock list to docs/PRD_NOTES.md and proceed.
```

---

## UI Brainstorming قبل از کدنویسی

اگر UI را دقیق نگفتید و می‌خواهید مدل دستش باز باشد:
- در `docs/UIUX.md` دو بخش اضافه کنید:
  1) MUST (غیرقابل مذاکره)
  2) MAY (اختیاری/خلاقیت آزاد)

برای گرفتن وایرفریم/طرح:
- از چت برای «تصویرسازی و سناریو» استفاده کنید (حتی با عکس/اسکیس).
- سپس خروجی را به UIUX اضافه کنید تا ایجنت کدنویسی سرخود مسیر را حدس نزند.

---

## فایل‌های این ریپو

- `docs/CODEX.md`: تنظیمات و الگوهای پرامپت برای Codex CLI (aligned to v6.7)
- `docs/EXECUTOR_CORE.md`: قوانین هسته‌ای اجرای پروژه توسط ایجنت
- `MEGAPROMPT_GENERATOR_V5.6.txt`: مگاپرامپت تولید مستندات (به‌روزشده برای جلوگیری از Block)
- `EXECUTOR_CORE_V5.txt`: نسخه قابل‌کپی برای پروژه‌ها

