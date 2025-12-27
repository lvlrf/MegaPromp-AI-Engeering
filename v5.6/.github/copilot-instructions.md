# GitHub Copilot Instructions (v6.5 aligned)

These instructions apply to Copilot Chat and inline suggestions for this repository.


## Execution Principles (Do not violate)
- Treat `docs/00_context/PRD.md` as immutable after it is generated. Never rewrite PRD content unless explicitly instructed by the user.
- Work strictly task-by-task using `docs/10_product/TASKS.md`.
- For each task: modify ONLY the task’s “Files to Touch” unless the task explicitly expands scope.
- Always run the task’s Verification Steps and record results in `docs/90_ops/CHANGELOG.md`.
- If blocked: write a clear entry to `docs/00_context/PRD_NOTES.md` (execution-time blocker), mark the task BLOCKED, and STOP.
- No broad refactors. No “cleanup” PRs. No architectural changes unless a task explicitly requires it.
- Keep outputs concise: `DONE`/`BLOCKED`, task id(s), changed files, verify commands run, next task.


## Minimal Change Policy
- Keep changes scoped and minimal.
- Avoid sweeping refactors, renames, or formatting-only changes.
- Prefer explicit, readable code over clever abstractions.

## Documentation Sync
- If a task changes API behavior, keep `docs/40_api/OPENAPI.yaml` consistent.
- If a task changes runtime/config requirements, update the relevant doc section and CHANGELOG.
