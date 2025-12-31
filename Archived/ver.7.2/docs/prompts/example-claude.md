# Example: How to Use Vibe Coding with Claude

Quick guide for starting a project with Claude AI.

---

## Step 1: Initial Prompt

Open Claude.ai and paste:

```
I want to build a software project using Vibe Coding framework.

Please read this megaprompt:

[PASTE ENTIRE CONTENT OF: docs/MEGAPROMPT_V7_FINAL.md]

After reading, start advisory conversation with me in Persian.
```

---

## Step 2: Describe Your Project

Example (in Persian):

```
من می‌خوام یک سیستم رزرو آنلاین برای رستوران بسازم.

فیچرها:
- ثبت‌نام و ورود کاربران  
- مشاهده منو
- رزرو میز (تاریخ، ساعت، تعداد نفر)
- پرداخت آنلاین
- پنل ادمین

بودجه: 500,000 تومان (~$10-12)
زمان: 1-2 هفته
من کدنویسی بلد نیستم.
```

---

## Step 3: Advisory Phase

Claude will ask:

**Questions:**
- Do you have hosting and domain?
- Which payment gateway? (ZarinPal/Stripe?)
- Cancellation policy?
- Priorities?

**Then provides:**
- Database recommendation (usually PostgreSQL)
- Architecture proposal (Node.js + React)
- Cost estimate ($20-25)
- Time estimate (10-12 hours AI coding)

---

## Step 4: Review & Approve

Claude shows comparison tables:
- Database options
- Model execution modes (Sonnet/Opus mix recommended)
- Tools needed

You approve or request changes.

---

## Step 5: Docs Generated

Claude creates:
- `docs/PRD_AI.md` - Full requirements
- `docs/TASKS.md` - 18 tasks with L/M/H labels
- `docs/ARCHITECTURE.md` - System design
- `docs/RULES.md` - Constraints

---

## Step 6: Start Coding

**Option A: Same Session**
```
Now code. Read docs/AGENT_START_PROMPT.md first.
```

**Option B: New Session (Recommended)**

New Claude chat:
```
You are a coding agent. Read:

[PASTE: docs/CLAUDE.md]
[PASTE: docs/PRD_AI.md]
[PASTE: docs/TASKS.md]
[PASTE: docs/ARCHITECTURE.md]

Follow Agent Start Protocol.
```

---

## Step 7: Monitor

- Check `tools/Dashboard.html`
- Telegram notifications (if setup)
- Review logs in `docs/CHANGELOG.md`

---

## Example Conversation Flow

**Turn 1:** [User pastes MEGAPROMPT + describes restaurant system]

**Turn 2:** Claude asks 8-10 clarifying questions

**Turn 3:** User answers

**Turn 4:** Claude provides recommendations with tables

**Turn 5:** User: "Approved!"

**Turn 6:** Claude generates all docs

**Turn 7:** New chat → coding begins

---

## Tips

✅ DO:
- Be specific about requirements
- Mention budget upfront
- State technical level
- Review docs before coding

❌ DON'T:
- Skip advisory phase
- Change requirements mid-coding
- Ignore cost estimates

---

## Result

After 10-12 hours:
- ✅ Working restaurant reservation system
- ✅ All tests passing
- ✅ Ready for deployment
- ✅ Cost: $20-25

---

**See full conversation examples in the complete version of this file.**
