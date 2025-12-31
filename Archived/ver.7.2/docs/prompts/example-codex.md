# Example: How to Use Vibe Coding with GPT-4/Copilot

Quick guide for GPT-4, GitHub Copilot, and Cursor AI.

---

## Method 1: ChatGPT (GPT-4)

Same as Claude:
1. Paste `docs/MEGAPROMPT_V7_FINAL.md`
2. Describe project
3. Follow advisory process
4. Get generated docs
5. Start coding

See `example-claude.md` for detailed flow.

---

## Method 2: GitHub Copilot

### Setup
```bash
mkdir my-restaurant-app
cd my-restaurant-app
git init

# Copy framework docs
cp -r /path/to/vibe-coding-v7/docs ./
```

### Workflow

1. **Generate requirements with ChatGPT**
   - Creates PRD_AI.md, TASKS.md, etc.

2. **Code with Copilot in VS Code**
   - Open `docs/TASKS.md`
   - For each task:

```python
# TASK-001: Setup Database Schema
# Requirements from TASKS.md:
# - Create users table
# - Create reservations table  
# - PostgreSQL with proper indexes

# [Copilot suggests implementation]
def create_schema():
    # Copilot will complete this
    pass
```

3. **Use Copilot Chat**
```
@workspace /new Create user auth following TASKS.md TASK-004
```

---

## Method 3: Cursor AI

**Best option for beginners!**

1. Download: https://cursor.sh/
2. Open project folder
3. Chat with AI (Cmd+L):

```
Read docs/CODEX.md and docs/TASKS.md

Implement TASK-001: Database Schema
This is Low complexity, be efficient.
```

4. Or inline generation (Cmd+K):
```python
# [Press Cmd+K here]
# Type: "Implement database schema from TASKS.md"
```

---

## Method 4: OpenAI API

```python
import openai

openai.api_key = "your-key"

def execute_task(task_id):
    codex = open('docs/CODEX.md').read()
    prd = open('docs/PRD_AI.md').read()
    tasks = open('docs/TASKS.md').read()
    
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[
            {"role": "system", "content": codex},
            {"role": "user", "content": f"""
Context: {prd}

Task: {extract_task(tasks, task_id)}

Implement following all guidelines.
"""}
        ],
        temperature=0.2
    )
    
    return response.choices[0].message.content

# Usage
result = execute_task("TASK-001")
print(result)
```

---

## Cost Comparison

| Method | Cost | Speed | Quality | Best For |
|--------|------|-------|---------|----------|
| ChatGPT (GPT-4) | $15-30 | Medium | ⭐⭐⭐⭐⭐ | Beginners |
| ChatGPT (GPT-3.5) | $2-5 | Fast | ⭐⭐⭐☆☆ | Budget |
| Copilot | $10/mo | Fast | ⭐⭐⭐⭐☆ | Developers |
| Cursor | $20/mo | Fast | ⭐⭐⭐⭐⭐ | Everyone |

**Recommendation:**
- Beginners: ChatGPT or Cursor
- Developers: GitHub Copilot
- Best value: Cursor AI ($20/month unlimited GPT-4)

---

## Example: Restaurant System

**With ChatGPT:**
- Describe project in Persian
- Get recommendations
- Approve plan
- Generate docs
- Code manually or with Copilot

**With Copilot:**
- Generate docs with ChatGPT first
- Then code in VS Code with Copilot suggestions
- Fast and efficient

**With Cursor:**
- Best of both worlds
- Chat + inline suggestions
- Unlimited GPT-4
- $20/month

---

## Quick Tips

✅ Use GPT-3.5 for Low/Medium tasks (save $$$)
✅ Use GPT-4 for High tasks (quality matters)
✅ Test as you code
✅ Follow TASKS.md order

❌ Don't use GPT-4 for everything (expensive)
❌ Don't skip the advisory phase
❌ Don't ignore complexity labels

---

**Full detailed examples in the complete version of this file.**

**Start now:** Choose your method and begin! 🚀
