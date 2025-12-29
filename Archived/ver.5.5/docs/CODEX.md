# Codex CLI — Project Execution Instructions (v6.5 aligned)

You are Codex executing this repository. Follow this document as the highest-priority repo instruction.


## Execution Principles (Do not violate)
- Treat `docs/00_context/PRD.md` as immutable after it is generated. Never rewrite PRD content unless explicitly instructed by the user.
- Work strictly task-by-task using `docs/10_product/TASKS.md`.
- For each task: modify ONLY the task’s “Files to Touch” unless the task explicitly expands scope.
- Always run the task’s Verification Steps and record results in `docs/90_ops/CHANGELOG.md`.
- If blocked: write a clear entry to `docs/00_context/PRD_NOTES.md` (execution-time blocker), mark the task BLOCKED, and STOP.
- No broad refactors. No “cleanup” PRs. No architectural changes unless a task explicitly requires it.
- Keep outputs concise: `DONE`/`BLOCKED`, task id(s), changed files, verify commands run, next task.


## Start Here
Read:
1) `docs/00_context/DECISIONS.md`
2) `docs/00_context/PRD.md`
3) `docs/10_product/TASKS.md`
4) `docs/20_engineering/RULES.md`
5) `docs/90_ops/CHANGELOG.md`

## Task Execution Contract
- Execute exactly ONE task at a time from `docs/10_product/TASKS.md`.
- Do not start the next task until:
  - current task is DONE and logged, or
  - current task is BLOCKED and logged.

## Blocking Conditions
If you lack required information (credentials, env vars, external service details, unclear acceptance criteria):
- Write a short, actionable note to `docs/00_context/PRD_NOTES.md` under a new heading: `BLOCKER: <TASK-ID>`
- Mark task BLOCKED in CHANGELOG
- STOP and ask the user for the missing information.

## Changelog Requirements
Every task completion must append to `docs/90_ops/CHANGELOG.md`:
- Date/time (UTC)
- Task id/title
- Summary of changes
- Files changed
- Verification commands and outputs (short)
- Status (DONE/BLOCKED)

## API Spec-first Rule
If task involves API changes:
- Update `docs/40_api/OPENAPI.yaml` first.
- Ensure implementation matches the spec.
- Validate spec + smoke test endpoints.
