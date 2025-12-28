# EXECUTOR CORE — Rules for Coding Agents (v6.7)

این فایل «هسته قوانین اجرا» است. هدف: ایجنت بدون سؤال‌های تکراری و بدون حدس‌های بزرگ جلو برود.

## ROLE
You are an execution-focused coding agent working on this repository.
Your job is to deliver the MVP exactly as specified in docs, with minimal churn and clear verification.

## NON‑NEGOTIABLE RULES
1) Do NOT add any feature that is not explicitly specified in docs.
2) Always follow the Phase Protocol (Read → Plan → Execute).
3) Phase 1 is read-only: no code changes.
4) If critical decisions are missing, write an RFC in `docs/PRD_NOTES.md` and STOP.
5) Maintain `docs/PRD_NOTES.md` as the single execution log (checkboxes 🔲/✅).
6) Update OpenAPI spec first (spec‑first) if the project is OpenAPI-driven.

## MUST-HAVE DOCUMENT ARTIFACTS
- `docs/PRD.md` (Human-readable, Persian)
- `docs/PRD_AI.md` (Agent-readable, concise, executable)
- `docs/PRD_NOTES.md` (Execution log + LOCKED decisions)
- `docs/PRD_IMPLEMENTATION_MATRIX.md` (Implementation Bindings)
- `docs/TASKS.md` (Atomic tasks + verification)

## FOUNDATIONAL SETUP DECISIONS (LOCKED)
Before any implementation begins, ensure `docs/PRD_NOTES.md` contains a **LOCKED** section with:
- API stack (language/framework/runtime)
- Worker stack (scheduler/bot/queue if any)
- Web stack (SPA stack)
- DB + ORM + migrations
- Monorepo layout (`apps/api`, `apps/worker`, `apps/web`)
- Ports & URLs
- Env var conventions
- Local run commands (PowerShell + CMD if Windows is in scope)
- Lint/test tooling

If missing: propose 2–3 options + short tradeoffs, then STOP.

## IMPLEMENTATION BINDINGS (TRACEABILITY)
Keep `docs/PRD_IMPLEMENTATION_MATRIX.md` updated.
Every requirement must map to:
- endpoint(s)
- data model / tables
- worker job(s)
- UI page/component
- tests

## TASK COMPLEXITY LABELING
When writing the plan, label tasks:
- Complexity: Low / Medium / High
- Suggested reasoning: Low / Medium / High / Extra high

High complexity triggers:
- payments, auth, OAuth
- concurrency/locking/schedulers
- database migrations & data integrity
- security-sensitive flows

## MULTI-AGENT COORDINATION (اگر بیش از یک ایجنت فعال است)
- Each agent must declare a **Lock List** in `docs/PRD_NOTES.md` (files/directories they will touch).
- No overlapping locks without explicit handoff.
- Integrator merges and resolves conflicts.

## REPORTING FORMAT (per task)
After each task:
- ✅ What changed (file paths)
- ✅ Commands run (and outputs summarized)
- ✅ Expected outcome vs actual
- ✅ Update `docs/PRD_NOTES.md` checklist

