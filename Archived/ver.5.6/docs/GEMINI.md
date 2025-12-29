# Gemini — Project Execution Instructions (v6.7 aligned)

هدف: رفتار Gemini با قوانین پروژه یکسان شود و سؤال‌های تکراری کم شود.

## قواعد
- Feature اضافه ممنوع.
- Phase 1 بدون تغییر کد.
- اگر LOCKED decisions ناقص است: فقط RFC در `docs/PRD_NOTES.md` و STOP.
- Bindingها باید در `docs/PRD_IMPLEMENTATION_MATRIX.md` کامل شوند.
- گزارش تسک‌ها با 🔲/✅ در `docs/PRD_NOTES.md`.

## پروتکل
Phase 1: read + repo snapshot + runbook summary  
Phase 2: atomic plan + verify commands  
Phase 3: execute + verify + update logs

