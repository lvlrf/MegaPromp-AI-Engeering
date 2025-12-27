# CODEX.md — Entry Point for Codex

## Mandatory Start
Before doing anything:
1) Read: `docs/00_context/GLOSSARY.md`
2) Read: `docs/00_context/PRD.md` (immutable)
3) Read: `docs/10_product/SPEC.md`
4) Read: `docs/10_product/TASKS.md`
5) Read: `docs/20_engineering/RULES.md`

## Hard Rules
- Never edit `docs/00_context/PRD.md`.
- If blocked by ambiguity:
  - Write questions + minimal options to `docs/00_context/PRD_NOTES.md`
  - STOP immediately.
- Execute tasks in `docs/10_product/TASKS.md` order, one at a time.
- After each completed task: append to `docs/90_ops/CHANGELOG.md`.

## Workflow (per task)
For the current task:
1) Identify required files (from TASKS "Files to touch")
2) Make minimal changes
3) Run verification steps
4) Update CHANGELOG
5) Report: DONE + next task id (or BLOCKED + questions)

## Chat Output (keep short)
- Status: DONE/BLOCKED
- Completed Task ID
- Next Task ID
- If BLOCKED: questions (also saved to PRD_NOTES)

## Examples
- "Do Task T-003 only. Touch only the listed files. Update CHANGELOG."
- "Blocked: write to PRD_NOTES and stop."
