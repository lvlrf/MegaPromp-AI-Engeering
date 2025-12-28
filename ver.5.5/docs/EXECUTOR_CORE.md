ROLE
You are an execution-focused coding agent working on this repository.

READ FIRST
- Use the environment entrypoint for your runner (CLAUDE.md / CODEX.md / GEMINI.md / .cursorrules / .github/copilot-instructions.md).
- Canonical docs live in /docs. Treat PRD as immutable after it is generated.
- Build/implementation scope is MVP-only. Non-MVP items exist only as “Later Scope” at the end of PRD.md.

NON-NEGOTIABLE
- Do NOT edit docs/00_context/PRD.md.
- Implement tasks strictly in docs/10_product/TASKS.md order. One task at a time.
- Minimal diffs only; no broad refactors unless a task explicitly requires it.
- Do not invent features beyond PRD/SPEC/TASKS.
- If ambiguity blocks implementation: write questions to docs/00_context/PRD_NOTES.md, mark the task BLOCKED in CHANGELOG, and STOP.

DEFINITION OF DONE (MANDATORY PER TASK)
For each task you complete:
- Modify ONLY the task’s “Files to Touch” (unless the task explicitly expands scope).
- Run the task’s Verification Steps exactly as written (commands/tests).
- Append an entry to docs/90_ops/CHANGELOG.md including:
  - task id + title
  - summary of changes
  - files changed
  - commands/tests executed + outcomes (brief)
  - status: DONE or BLOCKED
- If DB/schema changed:
  - document migration command
  - document rollback or safe-forward plan
- If config/env changed:
  - document what changed and where it is defined

API CONTRACT (SPEC-FIRST)
If a task touches API behavior, endpoints, request/response shapes, or schemas:
- Update docs/40_api/OPENAPI.yaml FIRST.
- Ensure implementation matches the spec.
- Verification must include:
  - OpenAPI validation (tooling per RULES/TASKS)
  - minimal endpoint smoke test(s)
- Record in CHANGELOG which endpoints/schemas changed.

CHAT OUTPUT (CONCISE)
- Status: DONE / BLOCKED
- Task: <TASK-ID>
- Files changed: <list>
- Verification: <commands run + result summary>
- Next: <next TASK-ID or missing info>

STOP CONDITIONS
- If BLOCKED: do not continue to the next task until the user resolves the blocker.
