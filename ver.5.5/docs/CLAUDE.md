# Claude Code — Project Execution Instructions (v6.5 aligned)

You are an AI coding agent executing this repo. Follow these instructions exactly.


## Execution Principles (Do not violate)
- Treat `docs/00_context/PRD.md` as immutable after it is generated. Never rewrite PRD content unless explicitly instructed by the user.
- Work strictly task-by-task using `docs/10_product/TASKS.md`.
- For each task: modify ONLY the task’s “Files to Touch” unless the task explicitly expands scope.
- Always run the task’s Verification Steps and record results in `docs/90_ops/CHANGELOG.md`.
- If blocked: write a clear entry to `docs/00_context/PRD_NOTES.md` (execution-time blocker), mark the task BLOCKED, and STOP.
- No broad refactors. No “cleanup” PRs. No architectural changes unless a task explicitly requires it.
- Keep outputs concise: `DONE`/`BLOCKED`, task id(s), changed files, verify commands run, next task.


## Required Workflow
1) Read these files first (in order):
   - `docs/00_context/DECISIONS.md`
   - `docs/00_context/PRD.md`
   - `docs/10_product/SPEC.md`
   - `docs/10_product/TASKS.md`
   - `docs/20_engineering/RULES.md`
   - `docs/90_ops/CHANGELOG.md`

2) Pick the next incomplete task in `docs/10_product/TASKS.md`.
3) Implement it with minimal diffs.
4) Run verification commands exactly as listed.
5) Append a CHANGELOG entry with:
   - task id + title
   - files changed
   - commands executed + outcomes
   - status: DONE/BLOCKED
6) Move to next task.

## API Contract Rule (Spec-first)
If a task touches an API endpoint or schema:
- Update `docs/40_api/OPENAPI.yaml` first.
- Implement code to match the spec.
- Verify with:
  - OpenAPI validation (tooling as defined in RULES/TASKS)
  - endpoint smoke test(s)
- Record in CHANGELOG which endpoints/schemas changed.

## Output Format (every response)
- Status: DONE or BLOCKED
- Task: <TASK-ID>
- Files changed: <list>
- Verification: <commands + results>
- Next: <next TASK-ID or required user decision>
