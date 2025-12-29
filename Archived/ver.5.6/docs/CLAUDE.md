# Claude Code — Project Execution Instructions (v6.7 aligned)

این فایل برای هماهنگ‌سازی رفتار Claude Code با ساختار Vibe Coding شماست.

## Hard Rules
- No new features beyond docs.
- Phase 1 read-only.
- LOCKED decisions are mandatory; if missing, write RFC in `docs/PRD_NOTES.md` and STOP.
- Keep `docs/PRD_NOTES.md` as execution log (🔲/✅).

## Required Docs
- `docs/PRD.md` (Persian, for humans)
- `docs/PRD_AI.md` (concise, executable)
- `docs/PRD_NOTES.md` (LOCKED decisions + progress)
- `docs/PRD_IMPLEMENTATION_MATRIX.md` (Implementation Bindings)
- `docs/TASKS.md`

## Workflow
1) Read & Understand (no code)
2) Plan (atomic tasks + verify)
3) Execute (task-by-task + verify + log)

## Foundational Setup Decisions (LOCKED)
Must include stack + monorepo layout + ports + env + run commands.
If not present, propose options and stop.

## Implementation Bindings
Maintain traceability in `docs/PRD_IMPLEMENTATION_MATRIX.md`.

