# Codex CLI — Project Execution Instructions (v6.7 aligned)

این فایل را داخل **ریپوی پروژه** نگه دارید تا Codex دقیقاً بداند چطور بدون سؤال اضافه جلو برود.

> اصل کلیدی: اگر «تصمیم‌های اجرایی» قفل نشده باشند، Codex طبق Hard Rules حق حدس بزرگ ندارد و Block می‌شود.

---

## 0) Minimal Setup (Config.toml)

مسیر پیش‌فرض: `~/.codex/config.toml`

نمونه پیشنهادی (حداقلی و امن):
```toml
# Choose sandbox mode that matches your risk tolerance.
# - workspace-write: can edit repo files
# - danger-full-access: can run arbitrary commands (only if you trust the repo)
sandbox_mode = "workspace-write"

approval_policy = "never" # only if you accept autonomous execution

[sandbox_workspace_write]
network_access = true

[features]
web_search_request = true
skills = true
```

نکته‌ها:
- `danger-full-access` فقط وقتی منطقی است که به محیط/کد اعتماد کامل دارید.
- اگر `approval_policy=never` بگذارید، Codex کمتر وسط کار توقف می‌کند (اما ریسک را بالا می‌برد).

---

## 1) Reasoning Level انتخابی (Low / Medium / High / Extra high)

پیشنهاد عملی:
- **Medium**: اجرای اکثر تسک‌های MVP
- **High**: طراحی معماری، پرداخت، همگام‌سازی، کانکارنسی
- **Extra high**: امنیت/پرداخت/کانکارنسی حساس
- **Low**: تغییرات کوچک، آپدیت داک‌ها

قاعده: اگر تسک «قفل/کانکارنسی/پول/امنیت» دارد → High یا Extra high.

---

## 2) Hard Rules (غیرقابل مذاکره)

- Do NOT add new features beyond what is explicitly specified in repo docs.
- Phase 1 is read-only (no code changes).
- If anything critical is missing, write an RFC in `docs/PRD_NOTES.md` and STOP.
- Only ask user questions when truly blocked by missing critical information.
- Keep a running log in `docs/PRD_NOTES.md` with checkboxes:
  - 🔲 planned
  - ✅ done

---

## 3) Phase Protocol (3 فاز استاندارد)

### Phase 1 — Read & Understand (NO code changes)
1) Read:
   - `docs/PRD_AI.md`
   - `docs/SPEC.md`
   - `docs/TASKS.md`
   - `docs/RULES.md`
   - `docs/ARCHITECTURE.md`
   - `docs/UIUX.md`
   - `docs/40_api/OPENAPI.yaml` (اگر وجود دارد)
2) Repo snapshot: ساختار فولدرها/فایل‌های کلیدی
3) Runbook: فرمان‌های اجرا، پورت‌ها، env
4) Identify missing/blocked parts

**Guardrail:** اگر بخش «LOCKED DECISIONS» در `docs/PRD_NOTES.md` وجود ندارد یا ناقص است → Phase 1 را تمام کن و فقط RFC/Options بنویس و STOP.

### Phase 2 — Plan (قبل از کد)
برای هر تسک:
- خروجی/نتیجه مورد انتظار
- فایل‌هایی که تغییر می‌کند
- فرمان‌های تست/verify

### Phase 3 — Execute (تسک به تسک)
بعد از هر تسک:
- گزارش تغییرات (مسیر فایل‌ها + خلاصه)
- اجرای verify
- آپدیت چک‌باکس‌ها در PRD_NOTES

---

## 4) Foundational Setup Decisions (LOCKED) — جلوگیری از Block

این بخش باید در `docs/PRD_NOTES.md` باشد و قبل از شروع کد *قفل* شود:

- Tech Stack (API/Worker/Web)
- Monorepo layout (`apps/…`)
- Ports
- Env var conventions
- Local run commands (Windows + Linux/macOS اگر لازم است)
- Lint/Test tooling

اگر هنوز قفل نشده:
- 2–3 گزینه پیشنهاد بده
- ریسک/مزایا را کوتاه بنویس
- **STOP** تا کاربر انتخاب کند

---

## 5) Implementation Bindings (Traceability)

هدف: هر قابلیت دقیقاً معلوم باشد به چه چیزهایی وصل است:
- Use case / requirement
- API endpoint
- DB tables/entities
- Worker jobs
- UI pages/components
- Tests

این فایل را بساز/آپدیت کن:
- `docs/PRD_IMPLEMENTATION_MATRIX.md`

---

## 6) Shell Compatibility (Windows)

برای جلوگیری از گیر کردن به تفاوت CMD و PowerShell:

### PowerShell (پیشنهادی)
- فعال‌سازی venv:
  - `.\.venv\Scripts\Activate.ps1`
- set env موقت:
  - `$env:KEY="value"`

### CMD
- فعال‌سازی venv:
  - `.venv\Scripts\activate.bat`
- set env موقت:
  - `set KEY=value`

**Rule:** هر وقت دستور می‌نویسی، اگر ویندوز در scope است، نسخه PowerShell + CMD را کنار هم بده.

---

## 7) Token / Cost Tracking

- اگر Codex را با API Key اجرا می‌کنید، ردیابی مصرف و هزینه معمولاً در داشبورد Usage/Billing همان اکانت API انجام می‌شود.
- برای کنترل هزینه: sessionها را کوتاه، مرحله‌ای و بر اساس Plan اجرا کنید.

---

## 8) Prompt Templates (کپی/پیست)

### A) شروع استاندارد (بدون سؤال اضافه)
```text
Follow docs/CODEX.md exactly.

Phase 1 only: read and summarize docs + repo snapshot. No code changes.
If LOCKED decisions are missing, write options in docs/PRD_NOTES.md and STOP.

If LOCKED decisions are present, proceed to Phase 2 plan then Phase 3 execute.
Keep docs/PRD_NOTES.md updated with checkboxes (🔲/✅).
```

### B) خروج از حالت Block (قفل کردن تصمیم‌ها)
```text
Update docs/PRD_NOTES.md:
- Add a section "Foundational Setup Decisions (LOCKED)" and record the decisions below as LOCKED.
- Add/Update docs/PRD_IMPLEMENTATION_MATRIX.md (Implementation Bindings).
Then proceed to Phase 2 plan. Do not start coding until the plan is written.
```

