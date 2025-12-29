# Vibe Coding V7 🚀

> **AI-Assisted Software Development Framework**  
> Transform your ideas into production-ready code with Claude AI

![Version](https://img.shields.io/badge/version-7.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-stable-success)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [What's Included](#whats-included)
- [Quick Start](#quick-start)
- [File Structure](#file-structure)
- [Usage Guide](#usage-guide)
- [Configuration](#configuration)
- [Best Practices](#best-practices)
- [Cost Estimation](#cost-estimation)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

**Vibe Coding V7** is a comprehensive framework for building software projects using AI coding agents (Claude, GPT-4, etc.). It provides a structured, advisor-driven approach that helps non-technical users manage AI-powered development efficiently.

### Why Vibe Coding?

- ✅ **Advisor-Driven**: AI guides you through decisions (database, architecture, tools)
- ✅ **Cost-Effective**: Smart model selection (L/M/H complexity) saves money
- ✅ **Non-Technical Friendly**: Clear Persian/English documentation
- ✅ **Production-Ready**: Includes testing, deployment, and monitoring
- ✅ **Real-Time Tracking**: Telegram notifications + Dashboard monitoring
- ✅ **Best Practices**: Built-in quality assurance and workflows

---

## ✨ Key Features

### 🤖 Smart AI Orchestration
- **Multi-Model Support**: Claude Sonnet (fast/cheap) + Opus (high-quality)
- **Complexity-Aware**: Automatic model selection based on task difficulty (L/M/H)
- **Cost Tracking**: Real-time token and budget monitoring
- **Auto-Backup**: Git commits every 5 tasks

### 📊 Decision Support
- **Comparison Tables**: Database, tools, execution modes (interactive HTML)
- **Complexity Guide**: Detailed L/M/H classification with examples
- **Cost Estimator**: Predict time and cost before starting

### 🔔 Real-Time Monitoring
- **Telegram Notifications**: Task completion, errors, budget warnings
- **Voice Alerts**: Audio notifications (cross-platform)
- **Live Dashboard**: Web-based progress monitoring

### 📚 Comprehensive Documentation
- **Agent Instructions**: Tailored for Claude, GPT-4, and other models
- **Workflow Templates**: PRD, TASKS, ARCHITECTURE, RULES, etc.
- **Test Checklists**: Automated and manual testing guides

---

## 📦 What's Included

### Core Framework Files

| File | Description |
|------|-------------|
| `MEGAPROMPT_V7_FINAL.md` | Main advisor-driven megaprompt |
| `CLAUDE.md` | Claude-specific agent instructions |
| `AGENT_START_PROMPT.md` | Initial agent protocol |
| `COMPLEXITY_GUIDE.md` | L/M/H task classification guide |

### Tools & Utilities

| File/Package | Description |
|--------------|-------------|
| `vibecoding/` | Telegram notification system (PHP) |
| `COMPARISON_TABLE.html` | Interactive decision tables |
| `Dashboard.html` | Real-time monitoring dashboard |
| `Voice_Notifier.py` | Audio alert system |

### Total Files: **8** | Total Size: **~2MB**

---

## 🚀 Quick Start

### Prerequisites

- AI coding agent access (Claude, GPT-4, etc.)
- Git installed
- (Optional) Telegram account for notifications
- (Optional) Web server for Dashboard

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/vibe-coding-v7.git
cd vibe-coding-v7

# (Optional) Setup Telegram notifications
cd vibecoding
# Edit config.php with your bot token and chat ID
# Upload to your web server
```

### Basic Usage

1. **Start a New Project**
   ```bash
   # Copy MEGAPROMPT_V7_FINAL.md content
   # Paste into Claude.ai or ChatGPT
   # Describe your project
   ```

2. **AI Generates Documentation**
   - PRD_AI.md (requirements)
   - TASKS.md (breakdown)
   - ARCHITECTURE.md (system design)
   - RULES.md (constraints)

3. **Agent Executes Tasks**
   ```bash
   # Agent reads AGENT_START_PROMPT.md
   # Analyzes project
   # Asks for approval
   # Executes tasks sequentially
   ```

4. **Monitor Progress**
   - Open `Dashboard.html` in browser
   - Check Telegram notifications
   - Review `docs/90_ops/COST_LOG.md`

---

## 📁 File Structure

```
vibe-coding-v7/
├── README.md                      # This file
├── MEGAPROMPT_V7_FINAL.md        # Main advisor prompt
├── CLAUDE.md                      # Claude agent instructions
├── AGENT_START_PROMPT.md         # Agent start protocol
├── COMPLEXITY_GUIDE.md           # L/M/H guide
├── COMPARISON_TABLE.html         # Decision tables
├── Dashboard.html                # Monitoring dashboard
├── Voice_Notifier.py             # Audio alerts
├── vibecoding/                   # Telegram notification package
│   ├── notify.php                # Main handler
│   ├── config.php                # Configuration
│   ├── README.md                 # Setup guide
│   ├── .htaccess                 # Security
│   └── .gitignore                # Git ignore
└── LICENSE                       # MIT License
```

---

## 📖 Usage Guide

### 1. Creating a Project

**Step 1: Describe Your Project**

Paste `MEGAPROMPT_V7_FINAL.md` into Claude and describe your project:

```
من یک سیستم رزرو آنلاین برای رستوران می‌خوام.
فیچرها:
- ثبت‌نام کاربران
- رزرو میز
- منو آنلاین
- پرداخت آنلاین
```

**Step 2: AI Advisory Phase**

AI will ask questions and provide recommendations:
- Database choice (PostgreSQL recommended)
- Architecture (REST API + React)
- Tools (Git, OpenAPI, Swagger)

**Step 3: Review Documentation**

AI generates:
- `docs/00_context/PRD_AI.md` - Full requirements
- `docs/10_product/TASKS.md` - 18 tasks with L/M/H labels
- `docs/20_engineering/ARCHITECTURE.md` - System design

**Step 4: Approve & Execute**

Agent analyzes, estimates cost/time, and asks for approval:
```
Estimated: 10h, $25
Ready to start? (Yes/No)
```

### 2. Model Selection Strategy

| Task Complexity | Model | Cost | When to Use |
|----------------|-------|------|-------------|
| **L (Low)** | Sonnet | $0.10-0.30 | CRUD, config, simple pages |
| **M (Medium)** | Sonnet | $0.30-1.50 | Business logic, validation |
| **H (High)** | Opus | $1.50-4.00 | Payments, auth, security |

**Recommended**: Mixed approach (L/M with Sonnet, H with Opus)

### 3. Monitoring Progress

**Option 1: Dashboard (Local)**
```bash
# Open Dashboard.html in browser
open Dashboard.html
```

**Option 2: Telegram Notifications**
```bash
# Setup once (see vibecoding/README.md)
# Then receive automatic notifications
```

**Option 3: Voice Alerts**
```bash
python Voice_Notifier.py task_complete "Task 5 done!"
```

---

## ⚙️ Configuration

### Telegram Notifications

1. Get bot token from [@BotFather](https://t.me/BotFather)
2. Get chat ID from [@userinfobot](https://t.me/userinfobot)
3. Edit `vibecoding/config.php`:
   ```php
   $TELEGRAM_BOT_TOKEN = 'your-bot-token';
   $TELEGRAM_CHAT_ID = 'your-chat-id';
   ```
4. Upload to server: `public_html/vibecoding/`
5. Test: `https://yoursite.com/vibecoding/notify.php?setup=true`

### Voice Notifications

**Windows**: No setup needed (uses `winsound`)

**Mac**: No setup needed (uses `afplay` and `say`)

**Linux**:
```bash
# Install audio tools (optional)
sudo apt-get install espeak
# Or
sudo apt-get install festival
```

---

## 🎯 Best Practices

### 1. Task Complexity Labeling

✅ **Always label complexity**:
- Check security sensitivity
- Consider edge cases
- Review COMPLEXITY_GUIDE.md

❌ **Avoid**:
- Guessing complexity
- Using Opus for simple tasks
- Skipping High tasks with Sonnet

### 2. Cost Management

✅ **Do**:
- Set budget before starting
- Monitor COST_LOG.md
- Use recommended model mix

❌ **Don't**:
- Use all-Opus unless necessary
- Ignore budget warnings
- Skip cost estimation

### 3. Communication

✅ **Terminal Output**: Always English (Persian breaks in terminals)

✅ **User Documentation**: Persian (README, TEST_CHECKLIST)

✅ **Technical Docs**: English (ARCHITECTURE, API specs)

---

## 💰 Cost Estimation

### Example Project: 18 Tasks

| Approach | Time | Cost | Quality | Recommended |
|----------|------|------|---------|-------------|
| All Sonnet | 12h | $18 | ★★★☆☆ | Budget-tight |
| **Mixed (Recommended)** | **10h** | **$25** | **★★★★☆** | **✅ Best** |
| All Opus | 8h | $45 | ★★★★★ | Quality-critical |
| Multi-Agent | 6h | $30 | ★★★★★ | Advanced users |

**Breakdown (Mixed Approach):**
```
Low tasks (8) with Sonnet:    $1.60
Medium tasks (7) with Sonnet: $7.00
High tasks (3) with Opus:     $9.00
Testing & Deployment:         $3-5
─────────────────────────────────
Total:                        $20-25
```

---

## 🛠️ Troubleshooting

### Common Issues

**1. Agent doesn't follow instructions**
- ✅ Make sure you're using AGENT_START_PROMPT.md
- ✅ Verify model is Claude Sonnet 4+ or equivalent

**2. Telegram notifications not working**
- ✅ Check config.php has correct token/chat ID
- ✅ Test with: `?setup=true`
- ✅ Verify server allows outgoing HTTPS

**3. Persian text broken in terminal**
- ✅ This is expected (Windows/Linux limitation)
- ✅ All logs should be in English
- ✅ Only user docs should be Persian

**4. High costs**
- ✅ Review task complexity labels
- ✅ Check if using Opus for Low tasks
- ✅ Set budget limit

---

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Areas for Contribution

- [ ] Support for other AI models (GPT-4, Gemini, etc.)
- [ ] Additional language support
- [ ] More comparison tables
- [ ] Dashboard data persistence
- [ ] CI/CD integration examples

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

**You are free to:**
- ✅ Use commercially
- ✅ Modify
- ✅ Distribute
- ✅ Sublicense

**With attribution required**

---

## 🙏 Acknowledgments

- **Anthropic** - For Claude AI
- **OpenAI** - For GPT models
- **Community Contributors** - For feedback and improvements

---

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/vibe-coding-v7/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/vibe-coding-v7/discussions)
- **Email**: your-email@example.com

---

## 🔗 Related Links

- [Claude AI Documentation](https://docs.anthropic.com)
- [OpenAPI Specification](https://swagger.io/specification/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)

---

## 📊 Project Stats

![GitHub stars](https://img.shields.io/github/stars/yourusername/vibe-coding-v7?style=social)
![GitHub forks](https://img.shields.io/github/forks/yourusername/vibe-coding-v7?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/yourusername/vibe-coding-v7?style=social)

---

<div align="center">

**Made with ❤️ by AI-Assisted Development**

[⭐ Star on GitHub](https://github.com/yourusername/vibe-coding-v7) • [🐛 Report Bug](https://github.com/yourusername/vibe-coding-v7/issues) • [✨ Request Feature](https://github.com/yourusername/vibe-coding-v7/issues)

</div>
