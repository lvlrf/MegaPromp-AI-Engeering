# GitHub Copilot Instructions — Project Protocol

## Canonical Documentation
All authoritative documentation lives in `/docs`.

## Non-Negotiables
- `docs/00_context/PRD.md` is immutable and human-owned. Do not edit it.
- Any ambiguity/questions/suggestions must go to `docs/00_context/PRD_NOTES.md` and you must STOP.
- Implement tasks strictly in `docs/10_product/TASKS.md` order, one task at a time.
- After each task, append a change entry to `docs/90_ops/CHANGELOG.md`.

## Engineering Rules
- Follow `docs/20_engineering/RULES.md` for coding style, testing, security.
- Minimal changes only; no broad refactors unless a task explicitly requires it.
- Do not invent features beyond PRD/SPEC/TASKS.

## Chat/PR Discipline
- Keep summaries short. Do not paste whole files.
- Always include: status (DONE/BLOCKED), completed task id, next task id.
- If BLOCKED: list questions and ensure they are written to PRD_NOTES.

## OpenAPI
- Treat `docs/40_api/OPENAPI.yaml` as contract.
- If backend exists, align implementation to spec-first design.
