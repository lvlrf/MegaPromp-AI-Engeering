# CLAUDE.md — Entry Point for Claude Code

## Prime Directive
- Canonical docs live in `/docs`.
- `docs/00_context/PRD.md` is **IMMUTABLE**. Never edit it.
- If anything is unclear or needs changes: write to `docs/00_context/PRD_NOTES.md` and **STOP**.

## Read Order (always)
1) `docs/00_context/GLOSSARY.md`
2) `docs/00_context/PRD.md`
3) `docs/10_product/SPEC.md`
4) `docs/10_product/TASKS.md`
5) `docs/20_engineering/RULES.md`
6) `docs/20_engineering/ARCHITECTURE.md`
7) `docs/30_design/UIUX.md`
8) `docs/40_api/OPENAPI.yaml`
9) `docs/90_ops/CHANGELOG.md` (append after each task)

## Execution Protocol
- Execute tasks strictly in `docs/10_product/TASKS.md`, one task at a time.
- After each task:
  - Update code
  - Run verification steps (per task)
  - Append a CHANGELOG entry
- If blocked:
  - Write questions + proposed options to `PRD_NOTES.md`
  - STOP (do not continue)

## Output Discipline
- Do not paste long file contents in chat.
- Reference file paths and section headers instead.

## Safety / Security
- Never hardcode secrets. Use environment variables.
- Follow `docs/20_engineering/RULES.md` security section strictly.

## Quick Prompts (examples)
- "Implement Task T-004 exactly as specified in docs/10_product/TASKS.md, update CHANGELOG.md."
- "I am blocked on Task T-007; write questions and options to PRD_NOTES.md and stop."
- "Validate OpenAPI.yaml for consistency with SPEC; propose minimal fixes."
