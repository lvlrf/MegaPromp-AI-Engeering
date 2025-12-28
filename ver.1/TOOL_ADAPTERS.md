# Tool Adapters Guide
# راهنمای استفاده با ابزارهای مختلف

این ساختار مستندات با چند تغییر کوچک با همه ابزارهای AI Coding کار می‌کنه.

---

## 1. Cursor

**سازگاری:** ✅ کامل

**Setup:**
```bash
# Just put docs folder in your project
/your-project
  /docs
    /00_context
    /10_product
    /20_engineering
    /30_design
```

**Usage in Composer:**
```
@docs/00_context/GLOSSARY.md
@docs/20_engineering/RULES.md
@docs/10_product/SPEC.md

Implement UC-001: Create Task
```

**Pro Tips:**
- Add docs to `.cursorules` for auto-include
- Use `@docs` to include entire folder
- Pin frequently used docs

**.cursorrules file:**
```
# Project Documentation
Always read these before generating code:
- docs/00_context/GLOSSARY.md for term definitions
- docs/20_engineering/RULES.md for coding constraints

# Implementation Rules
- Every feature must map to a UC-xxx in SPEC.md
- Follow architecture boundaries in ARCHITECTURE.md
- Never hardcode secrets
```

---

## 2. Claude Code (CLI)

**سازگاری:** ✅ کامل

**Setup:**
```bash
# Add CLAUDE.md to project root
/your-project
  CLAUDE.md          ← Entry point (required)
  /docs
    ...
```

**CLAUDE.md Purpose:**
Claude Code automatically reads `CLAUDE.md` from project root. Use it to:
- Point to documentation files
- Set project-wide rules
- Define working instructions

**Usage:**
```bash
# Start Claude Code
cd your-project
claude

# In Claude Code session
> Read docs/10_product/SPEC.md and implement UC-001
> Check my code against docs/20_engineering/RULES.md
```

**Pro Tips:**
- Keep CLAUDE.md under 500 lines
- Reference docs, don't duplicate content
- Use `/read docs/GLOSSARY.md` command to load specific files

---

## 3. GitHub Copilot / Codex

**سازگاری:** ⚠️ نسبی (context window کوچکتر)

**Challenge:** 
Copilot doesn't have a built-in way to load project docs.

**Workarounds:**

**Option A: Copilot Chat**
```
@workspace /explain the project structure
```
Then paste relevant sections from docs.

**Option B: .github/copilot-instructions.md**
```markdown
# Copilot Instructions

## Coding Rules
- Language: Python 3.12
- Framework: FastAPI
- NEVER hardcode secrets
- ALWAYS use type hints

## Key Terms
- User = authenticated member only
- Admin = elevated permissions, no billing
- Owner = team creator with billing

## When implementing features
1. Check docs/10_product/SPEC.md for use cases
2. Follow docs/20_engineering/RULES.md
```

**Option C: Comments in Code**
```python
# Implementation of UC-001: Create Task
# See: docs/10_product/SPEC.md
# Constraints: docs/20_engineering/RULES.md
```

---

## 4. Aider

**سازگاری:** ✅ کامل

**Setup:**
```bash
# Create .aider.conf.yml
read:
  - docs/00_context/GLOSSARY.md
  - docs/20_engineering/RULES.md
```

**Usage:**
```bash
# Start with docs loaded
aider --read docs/

# Or specific files
aider --read docs/00_context/GLOSSARY.md --read docs/20_engineering/RULES.md

# In session
> Implement UC-001 from docs/10_product/SPEC.md
```

**Pro Tips:**
- Use `--read` for reference docs (read-only)
- Use regular add for files to edit
- Aider respects .gitignore

---

## 5. OpenSpec

**سازگاری:** ✅ طراحی شده برای همین

**Setup:**
OpenSpec expects this exact structure:
```
/docs
  /00_context
    META_PRD.md      ← OpenSpec looks for this
    GLOSSARY.md
  /10_product
    usecases.md      ← Or SPEC.md
  /20_engineering
    rules.md
    architecture.md
```

**Usage:**
```bash
openspec init
openspec validate
openspec generate --use-case UC-001
```

**Pro Tips:**
- Rename SPEC.md to usecases.md if OpenSpec expects it
- Keep strict MUST/SHOULD language
- OpenSpec validates cross-references automatically

---

## 6. Windsurf (Codeium)

**سازگاری:** ✅ کامل

**Setup:**
Same as Cursor - just add docs folder.

**Usage in Cascade:**
```
@docs implement UC-001 following the rules
```

**.windsurfrules file:**
```
Read docs/00_context/GLOSSARY.md for definitions
Follow docs/20_engineering/RULES.md strictly
Map features to UC-xxx in docs/10_product/SPEC.md
```

---

## 7. Cline (VS Code Extension)

**سازگاری:** ✅ کامل

**Setup:**
Add to Cline settings:
```json
{
  "cline.contextFiles": [
    "docs/00_context/GLOSSARY.md",
    "docs/20_engineering/RULES.md"
  ]
}
```

**Usage:**
```
Read docs/10_product/SPEC.md
Implement UC-001: Create Task
Follow constraints in docs/20_engineering/RULES.md
```

---

## 8. Gemini CLI / Google AI Studio

**سازگاری:** ⚠️ نسبی

**Challenge:**
No built-in project context loading.

**Workaround - Concatenate Docs:**
```bash
# Create a single context file
cat docs/00_context/GLOSSARY.md \
    docs/20_engineering/RULES.md \
    docs/10_product/SPEC.md > CONTEXT.md

# Use with Gemini
gemini chat --context CONTEXT.md
```

**Or use system prompt:**
```
You are implementing features for {PROJECT}.

GLOSSARY:
{paste glossary}

RULES:
{paste key rules}

Now implement UC-001...
```

---

## 9. Devin / Autonomous Agents

**سازگاری:** ✅ کامل (اگه docs رو بخونه)

**Key Insight:**
Autonomous agents need VERY explicit constraints because they make decisions without asking.

**Critical Additions for Devin:**
```markdown
## STOP CONDITIONS
STOP and ask human if:
- Feature is not in SPEC.md
- Need to modify architecture
- Security decision required
- External service integration needed

## NEVER DO (Auto-blocked)
- Add new dependencies without approval
- Change database schema without migration
- Commit secrets to git
- Skip tests
```

---

## 10. Antigravity / Custom Agents

**سازگاری:** Depends on implementation

**General Approach:**
1. Check if tool has config file → add docs reference
2. Check if tool has system prompt → include key rules
3. Check if tool reads specific files → rename accordingly

**Universal Entry Point Pattern:**
Create `AI_CONTEXT.md` in root:
```markdown
# AI Agent Context

## Read These Files
1. docs/00_context/GLOSSARY.md - Definitions
2. docs/20_engineering/RULES.md - Constraints
3. docs/10_product/SPEC.md - Requirements

## Quick Rules
- Language: {lang}
- No secrets in code
- Map to UC-xxx before implementing
```

---

## Quick Compatibility Matrix

| Feature | Cursor | Claude Code | Copilot | Aider | OpenSpec | Windsurf | Gemini |
|---------|--------|-------------|---------|-------|----------|----------|--------|
| Auto-load docs | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| Folder reference | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| Cross-reference | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ | ⚠️ |
| Config file | .cursorrules | CLAUDE.md | copilot-instructions | .aider.conf | openspec.yml | .windsurfrules | ❌ |
| Context window | Large | Large | Medium | Large | Large | Large | Large |

---

## Recommended Approach

### اگه فقط از یک ابزار استفاده می‌کنی:
از config file همون ابزار استفاده کن.

### اگه از چند ابزار استفاده می‌کنی:
```
/project
  CLAUDE.md           ← For Claude Code
  .cursorrules        ← For Cursor
  .aider.conf.yml     ← For Aider
  AI_CONTEXT.md       ← Universal fallback
  /docs
    ...               ← Main documentation (shared)
```

هر config file فقط به `/docs` اشاره می‌کنه، duplicate نمی‌کنه.
