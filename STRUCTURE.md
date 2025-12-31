# MegaPrompt V8 - ساختار پروژه

## 📁 ساختار فولدرها

```
megaprompt-v8/
│
├── README.md                    # مقدمه پروژه (GitHub)
├── .cursorrules                 # تنظیمات Cursor IDE
│
├── core/                        # فایل‌های اصلی
│   ├── MEGAPROMPT_V8_FINAL.md       # Framework کامل (اصلی‌ترین)
│   ├── AGENT_START_PROMPT.md        # راه‌اندازی سریع
│   └── INDEX.md                     # راهنمای فایل‌ها
│
├── agents/                      # راهنماهای هر AI Model
│   ├── CLAUDE.md                    # برای Claude
│   ├── CODEX.md                     # برای GPT
│   └── GEMINI.md                    # برای Gemini
│
├── examples/                    # مثال‌های عملی
│   ├── example-claude.md            # مثال‌های Claude
│   └── example-codex.md             # مثال‌های GPT
│
├── guides/                      # راهنماهای تکمیلی
│   └── CLOUDFLARE_INTEGRATION.md    # CloudFlare VibeSDK + Agents
│
├── changelog/                   # تاریخچه تغییرات
│   ├── V8_CHANGES_SUMMARY.md        # تغییرات اولیه V8
│   └── V8_FINAL_UPDATE_SUMMARY.md   # آپدیت نهایی
│
├── tools/                       # ابزارهای کمکی (اگه داری)
│   └── [فولدر tools قبلی‌ات]
│
└── vibecoding/                  # کدهای vibe (اگه داری)
    └── [فولدر vibecoding قبلی‌ات]
```

---

## 🎯 توضیح هر فولدر

### 📂 core/ (هسته اصلی)
**مهم‌ترین فولدر!**

**MEGAPROMPT_V8_FINAL.md**:
- Framework کامل
- تمام فازها
- ساختار فایل‌ها
- قوانین تصمیم‌گیری
- اولین چیزی که باید خونده بشه

**AGENT_START_PROMPT.md**:
- راه‌اندازی سریع (30 ثانیه)
- Quick reference
- First message template

**INDEX.md**:
- راهنمای همه فایل‌ها
- توضیح هر فایل
- نقشه کلی پروژه

---

### 📂 agents/ (راهنماهای AI)
هر AI model راهنمای خودش رو داره.

**CLAUDE.md**:
- برای Claude Sonnet, Opus, Haiku
- Persian conversation patterns
- Evidence-based recommendations
- Deep technical review

**CODEX.md**:
- برای GPT-4o, o1, o1-mini
- UI/UX excellence
- Creative problem solving
- Code generation patterns

**GEMINI.md**:
- برای Gemini 2.0 Pro, Flash, 1.5 Pro
- Speed optimization
- Multimodal processing
- Cost efficiency

---

### 📂 examples/ (مثال‌های عملی)
مثال‌های واقعی conversation

**example-claude.md**:
- مثال Task Manager (Persian)
- Override warning
- Multi-agent coordination
- Complete workflows

**example-codex.md**:
- مثال E-Commerce Page
- UI/UX suggestions
- Multi-model strategy
- Professional patterns

---

### 📂 guides/ (راهنماهای اضافی)
مستندات تکمیلی و integration guides

**CLOUDFLARE_INTEGRATION.md**:
- VibeSDK patterns
- Agents framework
- Integration ideas
- Code examples

**بعداً می‌تونی اضافه کنی**:
- DEPLOYMENT_GUIDE.md
- ADVANCED_PATTERNS.md
- TROUBLESHOOTING.md

---

### 📂 changelog/ (تاریخچه)
تغییرات و آپدیت‌ها

**V8_CHANGES_SUMMARY.md**:
- تغییرات اولیه V8
- مقایسه با V7
- فایل‌های جدید

**V8_FINAL_UPDATE_SUMMARY.md**:
- آخرین آپدیت‌ها
- 30+ نقش اضافه شده
- مدل‌های جدید
- تمام بهبودها

---

### 📂 tools/ (ابزارهای قبلی شما)
**این فولدر رو تو داری!**

محتوای احتمالی:
- Scripts
- Utilities
- Helper tools
- Custom scripts

**مکان**: همین جا کنار megaprompt-v8

---

### 📂 vibecoding/ (کدهای قبلی شما)
**این فولدر رو هم تو داری!**

محتوای احتمالی:
- Vibe coding examples
- Templates
- Sample projects
- Experimental code

**مکان**: همین جا کنار megaprompt-v8

---

## 🔧 نحوه استفاده

### Setup اولیه

```bash
# 1. Extract ZIP
unzip MEGAPROMPT_V8_COMPLETE.zip

# 2. ساختار نهایی:
your-workspace/
├── megaprompt-v8/     # این پروژه
├── tools/             # فولدر قبلی‌ات (copy کن اینجا)
└── vibecoding/        # فولدر قبلی‌ات (copy کن اینجا)
```

### برای AI Models

```bash
# 1. مسیر اصلی
cd megaprompt-v8/

# 2. اولین فایل
Read: core/AGENT_START_PROMPT.md

# 3. فایل اصلی
Read: core/MEGAPROMPT_V8_FINAL.md

# 4. راهنمای model
Read: agents/CLAUDE.md  # یا CODEX.md یا GEMINI.md

# 5. مثال‌ها
Read: examples/example-claude.md
```

### برای Developers

```bash
# 1. مطالعه اولیه
cat README.md
cat core/INDEX.md

# 2. Setup Cursor
cp .cursorrules /path/to/your/project/

# 3. مطالعه کامل
cat core/MEGAPROMPT_V8_FINAL.md

# 4. Integration guides
cat guides/CLOUDFLARE_INTEGRATION.md
```

---

## 📌 فولدرهای قبلی شما

### tools/
**محتوای احتمالی**:
```
tools/
├── scripts/
├── utilities/
├── helpers/
└── ...
```

**استفاده در MegaPrompt V8**:
- Scripts برای automation
- Utilities برای helper functions
- Integration با MegaPrompt workflow

**مکان پیشنهادی**: کنار megaprompt-v8/

### vibecoding/
**محتوای احتمالی**:
```
vibecoding/
├── templates/
├── examples/
├── experiments/
└── ...
```

**استفاده در MegaPrompt V8**:
- Templates برای UI generation
- Examples برای learning
- Experiments برای testing patterns

**مکان پیشنهادی**: کنار megaprompt-v8/

---

## 🎨 ساختار نهایی پیشنهادی

```
your-workspace/
│
├── megaprompt-v8/              # این پروژه
│   ├── README.md
│   ├── .cursorrules
│   ├── core/
│   ├── agents/
│   ├── examples/
│   ├── guides/
│   └── changelog/
│
├── tools/                      # ابزارهای قبلی‌ات
│   ├── scripts/
│   ├── utilities/
│   └── helpers/
│
├── vibecoding/                 # کدهای vibe قبلی‌ات
│   ├── templates/
│   ├── examples/
│   └── experiments/
│
└── projects/                   # (اختیاری) پروژه‌های جدید
    ├── project-1/
    ├── project-2/
    └── ...
```

---

## 🔗 ارتباط فولدرها

### MegaPrompt V8 + Tools

```python
# مثال: استفاده از tools در MegaPrompt

# در Phase 3 (BUILD):
from tools.utilities import generate_template
from tools.scripts import deploy_automation

# Generate با MegaPrompt pattern
code = megaprompt.generate_code(task)

# Deploy با tools قبلی‌ات
deploy_automation.run(code)
```

### MegaPrompt V8 + VibeCoding

```javascript
// مثال: استفاده از vibecoding templates

// در UI generation:
import { templates } from '../vibecoding/templates';

// MegaPrompt می‌تونه از templates استفاده کنه
const ui = megaprompt.generateUI({
  template: templates.dashboard,
  customization: userPrefs
});
```

---

## 📊 مقایسه ساختارها

### ❌ ساختار قبلی (Flat)
```
all-files/
├── MEGAPROMPT_V8_FINAL.md
├── CLAUDE.md
├── CODEX.md
├── example-claude.md
├── example-codex.md
├── V8_CHANGES_SUMMARY.md
├── CLOUDFLARE_INTEGRATION.md
└── ... (13 files mixed together)

مشکلات:
- پیدا کردن فایل سخت
- دسته‌بندی نداره
- منظم نیست
```

### ✅ ساختار جدید (Organized)
```
megaprompt-v8/
├── core/           (اصلی‌ترین‌ها)
├── agents/         (راهنماهای AI)
├── examples/       (مثال‌ها)
├── guides/         (راهنماهای اضافه)
└── changelog/      (تاریخچه)

مزایا:
- سازماندهی شده
- پیدا کردن آسان
- قابل توسعه
- حرفه‌ای
```

---

## 🚀 مراحل بعدی

### 1. Setup فولدرها
```bash
# Copy فولدرهای قبلی
cp -r /path/to/old/tools ./tools
cp -r /path/to/old/vibecoding ./vibecoding

# ساختار نهایی:
ls -la
# megaprompt-v8/
# tools/
# vibecoding/
```

### 2. Test Integration
```bash
# Test که همه چی کار می‌کنه
cd megaprompt-v8/
cat core/MEGAPROMPT_V8_FINAL.md

cd ../tools/
ls -la

cd ../vibecoding/
ls -la
```

### 3. Git Setup (اختیاری)
```bash
# اگه می‌خوای Git داشته باشی
git init
git add megaprompt-v8/
git add tools/
git add vibecoding/
git commit -m "Initial setup: MegaPrompt V8 + Tools + VibeCoding"
```

---

## 💡 نکات مهم

### 1. فولدر tools
```
✅ بزارش کنار megaprompt-v8/
✅ می‌تونه با MegaPrompt integrate بشه
✅ Scripts قابل استفاده در workflow
```

### 2. فولدر vibecoding
```
✅ بزارش کنار megaprompt-v8/
✅ Templates قابل استفاده در UI generation
✅ Examples برای learning patterns
```

### 3. Cursor IDE
```
.cursorrules باید در root پروژه‌ای که کار می‌کنی باشه:

my-project/
├── .cursorrules    ← اینجا
├── src/
└── ...
```

---

## 📚 مستندات مرتبط

### در core/
- **MEGAPROMPT_V8_FINAL.md**: Framework کامل
- **INDEX.md**: راهنمای فایل‌ها

### در guides/
- **CLOUDFLARE_INTEGRATION.md**: Integration با VibeSDK & Agents

### در changelog/
- تاریخچه تمام تغییرات

---

## ✅ چک‌لیست Setup

**Setup اولیه**:
- [ ] Extract کردی ZIP رو
- [ ] ساختار فولدرها رو دیدی
- [ ] README.md خوندی

**فولدرهای قبلی**:
- [ ] tools/ رو copy کردی کنار megaprompt-v8/
- [ ] vibecoding/ رو copy کردی کنار megaprompt-v8/

**تست**:
- [ ] همه فایل‌ها accessible هستن
- [ ] ساختار منطقی به نظر میاد
- [ ] .cursorrules قابل استفاده است

**آماده استفاده**:
- [ ] AI agent راه‌اندازی شد
- [ ] Documentation خونده شد
- [ ] شروع پروژه اول!

---

## 🎯 خلاصه

**ساختار بهینه**:
```
workspace/
├── megaprompt-v8/    # MegaPrompt V8 (organized)
├── tools/            # ابزارهای قبلی‌ات
└── vibecoding/       # کدهای vibe قبلی‌ات
```

**مزایا**:
✅ منظم و سازمان‌یافته
✅ قابل توسعه
✅ راحت برای navigation
✅ حرفه‌ای
✅ Integration آسان

**استفاده**:
1. Extract ZIP
2. Copy tools و vibecoding کنار megaprompt-v8
3. شروع کار با core/AGENT_START_PROMPT.md

---

**همه چیز آماده است! 🚀**

*Structure designed for scalability and clarity*
