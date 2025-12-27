# GEMINI.md — Entry Point for Gemini CLI

## Read First (explicit)
Gemini does not auto-load context reliably. You MUST read:
1) `docs/00_context/GLOSSARY.md`
2) `docs/00_context/PRD.md` (immutable)
3) `docs/10_product/SPEC.md`
4) `docs/10_product/TASKS.md`
5) `docs/20_engineering/RULES.md`
Then proceed task-by-task.

## Non-Negotiables
- Do not modify PRD.md.
- If ambiguity exists, write it into `docs/00_context/PRD_NOTES.md` and STOP.
- Execute tasks in order, one at a time.
- Update `docs/90_ops/CHANGELOG.md` after each task.

## Minimalism Policy (execution)
- Do not re-summarize docs.
- Do not paste large code blocks in chat unless asked.
- Reference file paths + sections instead.

## Execution Loop
For each task:
- Implement minimal change
- Run verification steps
- Update CHANGELOG
- Report DONE/BLOCKED
