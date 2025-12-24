# CLAUDE.md - Entry Point for Claude Code

> This file is the entry point for Claude Code CLI. It references all project documentation.

## Project: {PROJECT_NAME}

## Quick Context
<!-- خلاصه پروژه برای Claude Code -->
{One paragraph description}

## Documentation Map
Read these files in order when working on this project:

### 1. Definitions First (ALWAYS read)
- `docs/00_context/GLOSSARY.md` - Term definitions, DO NOT assume meanings

### 2. Constraints (ALWAYS read)  
- `docs/20_engineering/RULES.md` - Coding rules, forbidden patterns, security

### 3. What to Build (Read per task)
- `docs/00_context/PROJECT.md` - Vision, constraints, scaling thresholds
- `docs/10_product/SPEC.md` - Use cases, requirements, acceptance criteria

### 4. How to Build (Read per task)
- `docs/20_engineering/ARCHITECTURE.md` - Services, data model, APIs
- `docs/30_design/FRONTEND.md` - UI components, flows, accessibility

## Working Instructions for Claude Code

### Before ANY code generation:
```
1. Read GLOSSARY.md - understand exact term meanings
2. Read RULES.md - understand constraints
3. Identify which UC-xxx you're implementing
4. Check FR-xxx requirements for that UC
```

### When implementing a feature:
```
Implement UC-{ID}: {Title}
- Follow RULES.md constraints
- Use GLOSSARY.md definitions
- Match ARCHITECTURE.md service boundaries
```

### When asked to "just do it" or "figure it out":
```
STOP. Ask which UC-xxx to implement.
Do NOT assume or create new features.
```

## File Structure
```
/project-root
  CLAUDE.md              ← You are here
  /docs
    /00_context
      GLOSSARY.md
      PROJECT.md
    /10_product
      SPEC.md
    /20_engineering
      ARCHITECTURE.md
      RULES.md
    /30_design
      FRONTEND.md
  /services
    /{service-name}
      /src
      /tests
  /frontend
    /src
```

## Commands Cheatsheet
```bash
# Start Claude Code in this project
claude

# Ask Claude to implement a specific use case
> Implement UC-001 following docs/10_product/SPEC.md

# Ask Claude to review against rules
> Review src/api/tasks.py against docs/20_engineering/RULES.md

# Ask Claude to add tests
> Add tests for UC-001 based on failure modes in SPEC.md
```

## Security Reminder
- NEVER put secrets in code
- ALWAYS use environment variables
- Check `docs/20_engineering/RULES.md` section 11 for details
