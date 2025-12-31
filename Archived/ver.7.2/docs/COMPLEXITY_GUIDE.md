# COMPLEXITY_GUIDE.md — Task Complexity & Model Selection

**Version**: 1.0  
**Date**: 2024-12-29  
**Purpose**: Guide for labeling task complexity and selecting appropriate AI models

---

## 🎯 Overview

Every task in `TASKS.md` must be labeled with complexity: **L** (Low), **M** (Medium), or **H** (High)

This helps:
- Select the right model for the job
- Estimate time and cost accurately
- Prevent using expensive models for simple tasks
- Ensure quality for complex tasks

---

## 📊 Complexity Levels

### 🟢 Low (L) - Simple & Straightforward

**Characteristics:**
- Well-defined with clear requirements
- No edge cases or complex logic
- Standard patterns (CRUD, basic validation)
- Minimal decision-making needed
- Low risk of bugs

**Examples:**
- Create a simple database table
- Add a basic API endpoint (GET/POST)
- Simple form validation
- Static page creation
- Basic CSS styling
- Add logging to existing code
- Simple configuration changes
- Text updates in documentation

**Recommended Model:**
- ✅ Claude Sonnet (fast & cost-effective)
- ⚠️ Avoid Opus (overkill, waste of money)

**Typical Time:** 15-45 minutes  
**Typical Cost:** $0.10-0.30

---

### 🟡 Medium (M) - Moderate Complexity

**Characteristics:**
- Multiple interconnected parts
- Business logic with some edge cases
- Requires careful validation
- Integration between components
- Moderate risk of bugs

**Examples:**
- User authentication flow
- API endpoint with multiple validations
- Database queries with joins
- Form with complex validation rules
- Frontend component with state management
- File upload with validation
- Email sending with templates
- Pagination implementation
- Search functionality
- Basic admin dashboard

**Recommended Model:**
- ✅ Claude Sonnet (capable of handling)
- ⚠️ Consider Opus if critical business logic

**Typical Time:** 45 minutes - 2 hours  
**Typical Cost:** $0.30-1.50

---

### 🔴 High (H) - Complex & Critical

**Characteristics:**
- Security-sensitive operations
- Financial transactions
- Complex algorithms
- Race conditions / concurrency
- Data integrity critical
- Multiple edge cases
- High risk if done wrong

**Examples:**
- Payment gateway integration
- OAuth/SSO implementation
- Password reset flow (secure)
- Real-time collaboration features
- Complex data migrations
- Webhook handling with retry logic
- Rate limiting implementation
- Encryption/decryption
- File permissions system
- API versioning strategy
- Database schema changes (production)
- Caching strategy with invalidation
- Complex state machines

**Recommended Model:**
- ✅ Claude Opus (best quality, worth the cost)
- ❌ Don't use Sonnet (higher risk of bugs)

**Typical Time:** 2-4 hours  
**Typical Cost:** $1.50-4.00

---

## 🤖 Model Comparison

### Claude Sonnet 4

**Best for:** Low & Medium tasks

**Strengths:**
- Fast execution
- Cost-effective
- Good at standard patterns
- Reliable for common tasks

**Weaknesses:**
- May miss edge cases in complex logic
- Less careful with security considerations
- Might need guidance on tricky bugs

**Cost:** ~$0.015 per 1K tokens (input)  
**Speed:** ⚡⚡⚡

---

### Claude Opus 4

**Best for:** High complexity tasks

**Strengths:**
- Exceptional reasoning
- Catches edge cases
- Security-conscious
- Handles complexity well
- Better debugging

**Weaknesses:**
- Slower than Sonnet
- More expensive
- Overkill for simple tasks

**Cost:** ~$0.075 per 1K tokens (input)  
**Speed:** ⚡⚡

---

## 📋 How to Label Tasks

### Decision Tree

```
Is it security-sensitive OR financial OR has race conditions?
├─ YES → High (H)
└─ NO ↓

Does it involve multiple systems OR complex business logic?
├─ YES → Medium (M)
└─ NO ↓

Is it standard CRUD OR simple logic OR configuration?
├─ YES → Low (L)
└─ NO → Medium (M) (default when unsure)
```

### Examples with Reasoning

#### Example 1: User Registration
```markdown
## TASK-003: User Registration Endpoint
**Complexity**: M (Medium)

Why Medium?
- Multiple validations needed
- Database interaction
- Email validation logic
- Password hashing (though library handles it)
- Not security-critical (login is more critical)
```

#### Example 2: Login with JWT
```markdown
## TASK-004: Login with JWT
**Complexity**: H (High)

Why High?
- Security-sensitive (authentication)
- JWT token generation
- Session management
- Brute force protection needed
- Rate limiting required
```

#### Example 3: Display User Profile
```markdown
## TASK-010: Display User Profile Page
**Complexity**: L (Low)

Why Low?
- Simple data fetch
- Basic rendering
- No complex logic
- Standard pattern
```

#### Example 4: Payment Processing
```markdown
## TASK-015: Stripe Payment Integration
**Complexity**: H (High)

Why High?
- Financial transaction
- External API integration
- Webhook handling
- Idempotency required
- Error handling critical
- Refund logic
```

---

## 💰 Cost-Benefit Analysis

### Scenario: 18 Tasks Project

**Option 1: All Sonnet**
```
- Low (8 tasks): 8 × $0.20 = $1.60
- Medium (7 tasks): 7 × $1.00 = $7.00
- High (3 tasks): 3 × $2.00 = $6.00
Total: $14.60
Time: ~12 hours
Risk: Medium (High tasks may have bugs)
```

**Option 2: Mixed (Recommended)**
```
- Low (8 tasks, Sonnet): 8 × $0.20 = $1.60
- Medium (7 tasks, Sonnet): 7 × $1.00 = $7.00
- High (3 tasks, Opus): 3 × $3.00 = $9.00
Total: $17.60
Time: ~10 hours
Risk: Low (High quality on critical tasks)
```

**Option 3: All Opus**
```
- Low (8 tasks): 8 × $0.40 = $3.20
- Medium (7 tasks): 7 × $2.00 = $14.00
- High (3 tasks): 3 × $3.00 = $9.00
Total: $26.20
Time: ~8 hours
Risk: Very Low (best quality)
```

**Recommendation:** Option 2 (Mixed)
- Best balance of cost, time, and quality
- Save money on simple tasks
- Invest in quality for critical tasks
- +$3 vs all-Sonnet, -$8.60 vs all-Opus

---

## 🎓 Learning from Experience

### When You Might Reclassify

**Upgrade from L to M:**
- Task took longer than expected
- Multiple bugs found in testing
- More edge cases than anticipated
- Example: "Simple API endpoint" became complex with many validations

**Upgrade from M to H:**
- Security concerns emerged
- Data integrity issues discovered
- More critical than initially thought
- Example: "User settings update" affects billing

**Downgrade from M to L:**
- Simpler than expected
- Library handles most complexity
- No edge cases found
- Example: "Complex validation" was just a regex check

**Note:** Update complexity in TASKS.md as you learn!

---

## 🚨 Red Flags (Automatic High Complexity)

If ANY of these apply → Complexity = High (H)

- [ ] Involves money/payments
- [ ] Handles passwords/authentication
- [ ] Accesses external APIs with side effects
- [ ] Modifies production database schema
- [ ] Implements security features
- [ ] Deals with user permissions
- [ ] Handles file uploads (security risk)
- [ ] Processes sensitive data (PII, health, financial)
- [ ] Implements encryption/decryption
- [ ] Involves concurrency/race conditions
- [ ] Critical for system stability
- [ ] Cannot be easily rolled back

---

## 📝 Template for TASKS.md

```markdown
## TASK-XXX: [Title]
**Complexity**: L / M / H
**Recommended Model**: sonnet / opus
**Estimated Time**: [based on complexity]
**Dependencies**: [prerequisite tasks]

**Why this complexity?**
[Brief explanation of reasoning]

**Description**:
[What needs to be done]

**Files to Touch**:
- `path/to/file.py`

**Acceptance Criteria**:
- [ ] [Criterion 1]
- [ ] [Criterion 2]

**Verification Commands**:
```bash
npm test
```

**Definition of Done**:
- [ ] Code implemented
- [ ] Tests passing
- [ ] Logged in CHANGELOG
- [ ] Task status → ✅
```

---

## 🎯 Quick Reference Card

| Complexity | Time | Cost | Model | Risk | Example |
|------------|------|------|-------|------|---------|
| **L** | 15-45m | $0.10-0.30 | Sonnet | Low | CRUD, static pages |
| **M** | 45m-2h | $0.30-1.50 | Sonnet | Med | Business logic, validation |
| **H** | 2-4h | $1.50-4.00 | Opus | Low | Payments, auth, security |

---

## 💡 Tips for Estimators

### For Chatbot (Creating TASKS.md)

When analyzing requirements:
1. Identify security-sensitive tasks → Mark High
2. Identify financial operations → Mark High
3. Group related simple tasks → Can be Low
4. Business logic with edge cases → Medium
5. Standard CRUD → Low
6. Integration points → Medium minimum

### For Agent (Executing Tasks)

When starting a task:
1. Read complexity label
2. If High + you're Sonnet → Suggest Opus to user
3. If Low + you're Opus → Note it's overkill (but proceed)
4. If complexity seems wrong → Log in PRD_NOTES.md

---

## 📚 Additional Resources

**Security Checklist** (for High tasks):
- [ ] Input validation on all user data
- [ ] SQL injection prevention
- [ ] XSS prevention
- [ ] CSRF tokens (if applicable)
- [ ] Rate limiting
- [ ] Error messages don't leak info
- [ ] Logs don't contain sensitive data
- [ ] Encryption at rest (if sensitive data)

**Testing Checklist** (for all tasks):
- [ ] Happy path works
- [ ] Edge cases handled
- [ ] Error cases handled
- [ ] Unit tests passing
- [ ] Integration tests passing (if applicable)
- [ ] Manual testing done

---

## 🔄 Continuous Improvement

After each project:
1. Review actual time vs estimated time
2. Review actual cost vs estimated cost
3. Identify tasks that should have been different complexity
4. Update this guide with learnings
5. Adjust future estimates

---

**Version**: 1.0  
**Last Updated**: 2024-12-29

**Remember**: When in doubt, go one level higher. Better to over-invest in quality than fix bugs later! ✅
