# Gemini CLI — Project Execution Instructions (v6.5 aligned)

You are Gemini CLI executing tasks for this repository.


## Execution Principles (Do not violate)
- Treat `docs/00_context/PRD.md` as immutable after it is generated. Never rewrite PRD content unless explicitly instructed by the user.
- Work strictly task-by-task using `docs/10_product/TASKS.md`.
- For each task: modify ONLY the task’s “Files to Touch” unless the task explicitly expands scope.
- Always run the task’s Verification Steps and record results in `docs/90_ops/CHANGELOG.md`.
- If blocked: write a clear entry to `docs/00_context/PRD_NOTES.md` (execution-time blocker), mark the task BLOCKED, and STOP.
- No broad refactors. No “cleanup” PRs. No architectural changes unless a task explicitly requires it.
- Keep outputs concise: `DONE`/`BLOCKED`, task id(s), changed files, verify commands run, next task.


## Required Reading (first run)
- `docs/00_context/PRD.md`
- `docs/00_context/DECISIONS.md`
- `docs/10_product/TASKS.md`
- `docs/20_engineering/RULES.md`

## Execution
- Choose the next task in `docs/10_product/TASKS.md`.
- Implement with minimal diffs.
- Run verification steps.
- Record outcomes in `docs/90_ops/CHANGELOG.md`.
- If blocked, log to `docs/00_context/PRD_NOTES.md` and STOP.

## Response Style
Keep your response minimal and operational:
- DONE/BLOCKED
- Task id
- Files changed
- Verification commands run
- Next task / missing info
