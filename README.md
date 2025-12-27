# راهنمای اجرایی فرآیند Vibe Coding (v5) — Multi‑Agent + Spec‑First + Read‑Only PRD

این سند برای قرار دادن در GitHub ریپو تهیه شده و کل فرآیند را قدم‌به‌قدم توضیح می‌دهد: از تولید سندها (Generator) تا اجرای تسک‌ها توسط AI coding agents (Executor) و همچنین مسیر کار با OpenSpec / OpenAPI.

---

## 0) خروجی‌هایی که باید در ریپو داشته باشید

### فایل‌های Entry Point (در روت ریپو)
- `CLAUDE.md` (Claude Code)
- `CODEX.md` (Codex)
- `GEMINI.md` (Gemini CLI)
- `.cursorrules` (Cursor)
- `.github/copilot-instructions.md` (GitHub Copilot)

### داکیومنت‌های مرجع (داخل پوشه docs)
- `docs/00_context/PRD.md`  (انسانی، **Immutable**)
- `docs/00_context/PRD_NOTES.md` (AI‑writable: سوال‌ها/ابهام‌ها/پچ‌ها)
- `docs/00_context/GLOSSARY.md` (تعاریف دامنه برای جلوگیری از drift)
- `docs/00_context/DECISIONS.md` (ADR‑lite)
- `docs/10_product/SPEC.md` (Use Cases / Functional Reqs / Traceability)
- `docs/10_product/TASKS.md` (تسک‌های اتمیک با Acceptance Criteria)
- `docs/20_engineering/ARCHITECTURE.md`
- `docs/20_engineering/RULES.md`
- `docs/30_design/UIUX.md` (Design Contract)
- `docs/40_api/OPENAPI.yaml` (Spec‑First contract)
- `docs/90_ops/CHANGELOG.md` (ثبت تغییرات: یک ورودی برای هر تسک)

---

## 1) قوانین غیرقابل مذاکره (Non‑Negotiables)

1) **PRD دست نخورَد**
   - `docs/00_context/PRD.md` فقط برای انسان است و هیچ AI agent اجازه‌ی ویرایش آن را ندارد.
   - اگر چیزی مبهم/متناقض/قابل بهبود است، فقط در `docs/00_context/PRD_NOTES.md` نوشته می‌شود.

2) **اجرای تسک‌ها فقط از TASKS**
   - هیچ کاری خارج از `docs/10_product/TASKS.md` انجام نمی‌شود.
   - یک تسک در هر مرحله (One‑Task‑At‑A‑Time).

3) **ChangeLog اجباری**
   - هر تسک که Done شد، یک ورودی در `docs/90_ops/CHANGELOG.md` ثبت می‌شود (تغییرات، فایل‌ها، تست‌ها/کامندها).

4) **Stop Condition**
   - اگر agent برای ادامه نیاز به تصمیم/اطلاعات دارد: سوال‌ها + گزینه‌ها را در `PRD_NOTES.md` می‌نویسد و **STOP** می‌کند.

---

## 2) فرآیند کلی: Generator → Approval → Executor

### مرحله A — Generator (ولخرج و کامل)
هدف: تبدیل ایده/طوفان ذهنی شما به «مجموعه سندهای قابل اجرا برای agentها».

**گام‌ها:**
1) ایده/شرح پروژه را به Generator بدهید (MegaPrompt Generator v5).
2) Generator باید:
   - سوال‌های رفع ابهام بپرسد
   - خلاصه‌ی فهم + ریسک‌ها + پیشنهادها + گزینه‌ها را ارائه دهد
   - در نهایت یک درخت فایل پیشنهادی ارائه کند
   - سپس **متوقف شود** و تایید شما را بگیرد (Approval Gate)

3) بعد از تایید شما، Generator فایل‌ها را تولید/آپدیت می‌کند.

**خروجی این مرحله:** docs کامل + entrypointهای ابزارها آماده.

---

### مرحله B — Commit & Baseline
1) تغییرات docs و entrypointها را commit کنید.
2) اگر از Branch استفاده می‌کنید: یک برنچ `docs-baseline` یا `v5-init` بسازید.
3) مطمئن شوید `PRD.md` واقعی (انسانی) پر شده یا حداقل اسکلت آن آماده است.

---

### مرحله C — Executor (کم‌هزینه و خودکار)
در این مرحله، agentها فقط تسک‌ها را اجرا می‌کنند.

**گام‌های عمومی:**
1) در `docs/10_product/TASKS.md` مطمئن شوید Task `T-001` دقیق و قابل اجراست:
   - Files to touch
   - Acceptance Criteria
   - Verification Steps

2) به ابزار مورد نظر (Codex / Claude / Gemini / Copilot / Cursor) پیام شروع بدهید (نمونه‌ها در انتهای همین سند).

3) بعد از هر تسک:
   - verify steps اجرا شود
   - CHANGELOG به‌روزرسانی شود
   - سپس Task بعدی

---

## 3) مسیر OpenSpec / OpenAPI (Spec‑First)

شما دو مسیر دارید؛ هر دو قابل استفاده‌اند:

### مسیر 1: استفاده از OpenSpec (openspec.dev) برای تولید/ویرایش OpenAPI
**هدف:** ساخت/ویرایش `docs/40_api/OPENAPI.yaml` با یک ابزار متمرکز.

**گام‌ها (پیشنهادی):**
1) به OpenSpec بروید و پروژه/اسپک را باز کنید.
2) `OPENAPI.yaml` را وارد (import) کنید یا از صفر بسازید.
3) ساختار را کامل کنید:
   - `info`, `servers`
   - `paths` (endpointها)
   - `components/schemas`
   - `securitySchemes` (اگر auth دارید)
   - پاسخ استاندارد خطا (مثل `ErrorResponse`)

4) خروجی را export کنید و جایگزین `docs/40_api/OPENAPI.yaml` کنید.
5) commit کنید.

> توصیه: در SPEC.md و TASKS.md ارجاع دقیق به endpointها/Schemaها بدهید تا drift کمتر شود.

---

### مسیر 2: ویرایش مستقیم فایل و اعتبارسنجی محلی
اگر ترجیح می‌دهید YAML را مستقیم نگه دارید، این چرخه را اضافه کنید:

**ابزارهای پیشنهادی (اختیاری ولی مفید):**
- `swagger-cli` برای validate
- `prism` برای mock server

**گام‌ها:**
1) Validate:
   - اجرا: `swagger-cli validate docs/40_api/OPENAPI.yaml`
2) Mock (برای تست frontend یا قراردادها):
   - اجرا: `prism mock docs/40_api/OPENAPI.yaml`
3) اگر agent backend می‌سازد:
   - backend باید با OPENAPI تطبیق داشته باشد (spec-first)

> اگر تیم/پروژه بزرگ‌تر شد، می‌توانید contract testing هم اضافه کنید.

---

## 4) چک‌لیست قبل از شروع کدنویسی (برای کاهش دوباره‌کاری)

- [ ] PRD.md توسط انسان تکمیل شده و «حداقل» Problem/Goals/Non‑Goals/Flows را دارد.
- [ ] GLOSSARY اصطلاحات کلیدی دامنه را دارد.
- [ ] SPEC.md حداقل 3–5 Use Case اصلی دارد و UC↔FR نگاشت شده.
- [ ] TASKS.md اتمیک است (تسک‌های خیلی بزرگ شکسته شده‌اند).
- [ ] RULES.md شامل تست/امنیت/محدودیت‌هاست.
- [ ] UIUX.md قرارداد RTL و stateها را مشخص کرده.
- [ ] OPENAPI.yaml اگر API دارید، حداقل اسکلت endpointها را دارد.
- [ ] CHANGELOG آماده است.

---

## 5) آیا MegaPromptها کوتاه هستند؟ کافی است؟

بله، **عمداً** کوتاه طراحی شده‌اند — مخصوصاً Executorها.

### چرا کوتاهی خوب است؟
- Executor باید «runner» باشد نه «نویسنده»؛ هرچه prompt طولانی‌تر شود، احتمال:
  - تکرار/توکن‌سوزی
  - drift (برداشت‌های ناخواسته)
  - و رفتار غیرقابل پیش‌بینی
  بیشتر می‌شود.

### اصل مهم این معماری
- **Docs = Source of Truth**
- **Executor Prompt = پروتکل اجرا + Stop Conditions**
بنابراین اگر Docs درست نوشته شوند، Executor کوتاه کاملاً کافی است.

### چه زمانی لازم است prompt را بلندتر کنیم؟
فقط اگر:
- RULES.md ناقص باشد
- TASKS.md معیار پذیرش و verify نداشته باشد
- یا پروژه در محیط خاصی (مثل mono-repo پیچیده) نیاز به پروتکل‌های اضافی دارد

در غیر این صورت، بلند کردن prompt معمولاً هزینه را زیاد و کیفیت را غیرپایدار می‌کند.

---

## 6) پیام شروع (Start Command Prompts) برای هر ابزار

### 6.1) Codex
«ابتدا فایل `CODEX.md` را کامل بخوان. سپس `docs/10_product/TASKS.md` را باز کن و فقط Task `T-001` را اجرا کن.
فقط فایل‌هایی را تغییر بده که در همان Task در بخش “Files to Touch” آمده.
بعد از اتمام، `docs/90_ops/CHANGELOG.md` را با یک ورودی برای T-001 آپدیت کن.
خروجی چت: DONE/BLOCKED + Task انجام‌شده + Task بعدی.»

### 6.2) Claude Code
«طبق `CLAUDE.md` پیش برو. Task `T-001` را از `docs/10_product/TASKS.md` اجرا کن، verification steps را انجام بده،
و `docs/90_ops/CHANGELOG.md` را آپدیت کن. اگر ابهام داشتی، در `docs/00_context/PRD_NOTES.md` بنویس و STOP کن.»

### 6.3) Gemini CLI
«اول فایل `GEMINI.md` را کامل بخوان. سپس `docs/10_product/TASKS.md` را باز کن و فقط `T-001` را انجام بده.
بعد از اتمام، `docs/90_ops/CHANGELOG.md` را آپدیت کن. اگر ابهامی بود، فقط در `docs/00_context/PRD_NOTES.md` بنویس و STOP کن.»

### 6.4) GitHub Copilot
«طبق `.github/copilot-instructions.md` عمل کن. فقط Task `T-001` را از `docs/10_product/TASKS.md` اجرا کن.
PRD را تغییر نده. پس از پایان، `docs/90_ops/CHANGELOG.md` را با جزئیات تغییرات و تست‌ها آپدیت کن.
خروجی کوتاه: DONE/BLOCKED + Task بعدی.»

### 6.5) Cursor
«طبق `.cursorrules` عمل کن. `docs/10_product/TASKS.md` → Task `T-001` را انجام بده.
فقط فایل‌های مشخص‌شده را تغییر بده. بعدش `docs/90_ops/CHANGELOG.md` را آپدیت کن.
اگر ابهام بود، در `docs/00_context/PRD_NOTES.md` بنویس و STOP کن.»

---

## 7) توصیه‌های عملی برای کم‌کردن دوباره‌کاری (Best Practices)

1) تسک‌ها را “کوچک‌تر از چیزی که فکر می‌کنی” بنویس.
2) برای هر تسک، **Files to touch** را محدود کن (جلوی refactor ناخواسته را می‌گیرد).
3) Verification steps را واقعی بنویس (دستور و انتظار خروجی).
4) هر تصمیم مهم را ADR ثبت کن تا agentها بحث‌های قبلی را تکرار نکنند.
5) اگر UI مهم است، UIUX.md را دقیق نگه دار (صفحه‌ها + stateها).

---

## 8) اگر می‌خواهید این فرآیند را CI‑Friendly کنید (اختیاری)
می‌توانید در CI:
- validate OpenAPI
- lint/format
- اجرای تست‌ها
- enforce CHANGELOG updates برای PRها
اضافه کنید.

(این بخش را می‌توانیم بعداً دقیق‌تر با stack واقعی پروژه‌تان تکمیل کنیم.)
