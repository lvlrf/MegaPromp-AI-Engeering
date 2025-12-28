# Agent Handoff Quickstart (v6.7)

هدف: وقتی جلسه قطع شد یا ایجنت Block شد، بدون سردرگمی ادامه بدهید.

## 1) شروع یا ادامه
- شروع: `codex` (در روت ریپو)
- ادامه جلسه قبلی: `codex resume`

## 2) اگر ایجنت روی Block رفت (سؤال‌های «تصمیم اجرایی»)
علامت‌ها:
- می‌گوید apps/ وجود ندارد
- می‌گوید run commands / tech stack مشخص نیست
- RFC می‌زند و STOP می‌کند

راه‌حل استاندارد:
1) در `docs/PRD_NOTES.md` بخش **Foundational Setup Decisions (LOCKED)** را اضافه/تکمیل کنید.
2) در `docs/PRD_IMPLEMENTATION_MATRIX.md` Bindingها را اضافه کنید.
3) `codex resume` و بگویید وارد Phase 2 Plan شود.

پرامپت آماده:
```text
Update docs/PRD_NOTES.md:
- Add/complete "Foundational Setup Decisions (LOCKED)" with explicit stack + monorepo layout + ports + env + run commands.
Update docs/PRD_IMPLEMENTATION_MATRIX.md with Implementation Bindings.
Then proceed to Phase 2 plan (no code until plan is written).
```

## 3) چگونه سؤال‌ها را کم کنیم؟
- PRD_AI را کوتاه و «اجراپذیر» نگه دارید.
- Run commands را واقعی بنویسید (نه placeholder).
- پورت‌ها و env را صریح بنویسید.
- Bindingها را کامل کنید تا ایجنت حدس نزند.

## 4) اگر UI را هنوز دقیق نکرده‌اید
دو حالت:
- MUST: اجزای قطعی (RTL, layout, navigation, fields)
- MAY: آزادی خلاقیت

این را در `docs/UIUX.md` بنویسید تا ایجنت گرفتار «حدس UI» نشود.

## 5) دادن UI Template به AI
اگر template دارید:
- فایل‌های template را در repo اضافه کنید (مثلاً `ui_template/`).
- در `docs/UIUX.md` صریح بگویید:
  - «از این template به‌عنوان reference استفاده کن»
  - «فقط این فایل‌ها را تغییر بده»
  - «اگر نیاز به تبدیل بود، plan بده و قبل از اجرا stop کن»

## 6) چک‌لیست وضعیت تسک‌ها
در `docs/PRD_NOTES.md` از این الگو استفاده کنید:
- 🔲 T001 — Repo skeleton
- ✅ T002 — OpenAPI lint wired
- 🔲 T003 — DB migrations baseline

