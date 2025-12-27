# Agent Handoff Quickstart (v6.5)

Put these files into your repo root (and `.github/`):
- CLAUDE.md
- CODEX.md
- GEMINI.md
- .cursorrules
- .github/copilot-instructions.md

Purpose:
- Ensure any agent/model continues safely without loops, rework, or spec drift.
- Enforce DoD + verification + changelog per task.

Operational sequence for any agent:
1) Read DECISIONS → PRD → TASKS → RULES → CHANGELOG
2) Execute next single task
3) Verify
4) Log
5) Continue
