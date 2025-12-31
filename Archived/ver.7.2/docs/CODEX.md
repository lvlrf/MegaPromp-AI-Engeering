# CODEX.md — GitHub Copilot & GPT-4 Instructions

**Version**: 2.0  
**Last Updated**: 2024-12-29  
**Target**: GitHub Copilot, GPT-4, OpenAI Codex, Cursor AI

---

## Quick Reference

This is the GPT-4/Copilot equivalent of CLAUDE.md. 

**Key Differences from Claude:**
- Context Window: 128K tokens (vs Claude's 200K)
- Best for: GitHub integration, API usage, Cursor IDE
- Cost: Similar to Claude Opus (~$0.03/1K tokens)

---

## Model Selection

| Task Complexity | Model | Reason |
|----------------|-------|---------|
| L (Low) | GPT-3.5-Turbo | 75x cheaper, sufficient for simple tasks |
| M (Medium) | GPT-3.5 or GPT-4 | GPT-3.5 usually fine |
| H (High) | GPT-4 | Security, payments need best model |

---

## Usage Methods

### 1. ChatGPT Web Interface
- Paste MEGAPROMPT_V7_FINAL.md
- Follow same workflow as Claude
- See: `docs/prompts/example-codex.md`

### 2. GitHub Copilot in VS Code
```python
# Open TASKS.md in VS Code
# For each task, create file with comment:

# TASK-001: Setup Database Schema
# From TASKS.md - Create users, reservations, menu tables
# Follow ARCHITECTURE.md - PostgreSQL with proper indexing

# [Copilot suggests implementation here]
```

### 3. Cursor AI
- Best all-in-one solution
- Built-in GPT-4
- Chat with entire codebase
- $20/month unlimited

### 4. OpenAI API
```python
import openai

response = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
        {"role": "system", "content": open('docs/CODEX.md').read()},
        {"role": "user", "content": f"Implement {task_description}"}
    ]
)
```

---

## Core Principles (Same as Claude)

1. **Read First** - All docs before coding
2. **Follow Complexity Labels** - L/M/H determines model
3. **Respect DoD** - All criteria must be met
4. **UTF-8 Everywhere** - All files and DB
5. **Log Everything** - Every task in CHANGELOG
6. **English Logs** - Persian breaks terminals

---

## Logging Format

```markdown
## [2024-12-29 14:30] TASK-XXX: Title
**Model Used**: gpt-4 / gpt-3.5-turbo
**Status**: ✅ DONE
**Time**: 45m
**Tokens**: ~12,000

### Changes:
- Created login API
- Added JWT auth

### Verification:
```bash
npm test
# ✅ All passed
```
```

---

## Error Handling

1. Try fix (1st attempt)
2. Alternative approach (2nd attempt)  
3. Log to PRD_NOTES.md
4. Wait for user decision

Never loop infinitely - stop after 2 retries.

---

## Cost Tracking

Log every task in `docs/COST_LOG.md`:
```
| Time | Task | Model | Tokens | Cost | Total |
```

---

## Git Auto-Backup

Every 5 tasks:
```bash
git add .
git commit -m "Progress: 5 tasks done"
git push
```

---

## Agent Start Protocol

1. Read all docs
2. Analyze & create estimate
3. Wait for approval ("Yes"/"Go"/"Approved")
4. Execute tasks sequentially
5. Report completion

---

## Best Practices

✅ DO:
- Use GPT-3.5 for L/M tasks (save money)
- Use GPT-4 for H tasks (quality matters)
- Test as you go
- Keep it simple

❌ DON'T:
- Use GPT-4 for simple tasks (waste)
- Add features not in spec
- Skip testing
- Ignore complexity labels

---

## Final Checklist

- [ ] All tasks ✅
- [ ] Tests passing
- [ ] Code in Git
- [ ] Logs updated
- [ ] User notified

---

**For detailed examples, see:** `docs/prompts/example-codex.md`

**Full documentation:** Same principles as `CLAUDE.md` - read that for complete details.
