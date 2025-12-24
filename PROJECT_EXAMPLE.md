# Project: TaskFlow

## 1. Vision
<!-- چشم‌انداز کلی -->
TaskFlow is a lightweight task management system designed for small teams (2-10 people) who need simple project tracking without the complexity of enterprise tools like Jira. It focuses on clarity, speed, and Persian RTL support.

## 2. Problem Statement
<!-- مسئله‌ای که حل می‌کنیم -->
- **Problem**: Small teams waste time switching between WhatsApp, spreadsheets, and notes to track tasks
- **Who has it**: Freelancers and small teams in Iran
- **Current solutions**: Trello (slow, no RTL), Jira (too complex), WhatsApp groups (chaotic)
- **Why they fail**: Either too complex, too slow, or lack proper Persian support

## 3. Constraints (ABSOLUTE)
<!-- محدودیت‌های مطلق - این‌ها قابل نقض نیستند -->
- MUST NOT: Store user data outside Iran-accessible servers
- MUST NOT: Require credit card for signup
- MUST: Work offline with sync capability
- MUST: Full RTL support
- MUST: Load under 3 seconds on 3G connection
- LEGAL: Comply with Iranian data residency preferences
- BUDGET: Infrastructure cost < $50/month for MVP
- TIME: MVP ready in 6 weeks

## 4. Non-Goals (Explicit Exclusions)
<!-- چیزهایی که عمداً نمی‌سازیم -->
- Time tracking - Reason: Adds complexity, not core to task management
- Gantt charts - Reason: Enterprise feature, not needed for small teams
- Video calls - Reason: Use existing tools (Google Meet, etc.)
- File storage - Reason: Use links to Google Drive, Dropbox, etc.
- Mobile app - Reason: PWA is sufficient for MVP

## 5. Assumptions
<!-- فرضیات پروژه -->
- Users have stable internet most of the time (offline is edge case)
- Teams are already using some form of communication tool (WhatsApp, Telegram)
- Users prefer Persian UI but can read English technical terms
- Most users access from mobile devices (70%+)

## 6. Scaling Thresholds
<!-- آستانه‌های مقیاس - کی باید چی رو ارتقا بدیم -->
| Metric | Current Target | Warning At | Action Required |
|--------|---------------|------------|-----------------|
| Concurrent Users | 100 | 70 | Add Redis caching |
| Total Users | 1,000 | 700 | Upgrade DB instance |
| Database Size | 5 GB | 3.5 GB | Add archival strategy |
| API Requests/sec | 50 | 35 | Add load balancer |
| Teams | 100 | 70 | Shard by team_id |

## 7. Success Criteria (MVP)
<!-- معیار موفقیت -->
- [ ] 10 teams actively using the product weekly
- [ ] Average task completion time trackable
- [ ] User can create, assign, complete task in < 30 seconds
- [ ] Page load < 3s on 3G
- [ ] Zero data loss incidents
- [ ] RTL works correctly on all pages
