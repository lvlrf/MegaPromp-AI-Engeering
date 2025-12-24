# Product Specification: TaskFlow

## 1. User Roles & Permissions

### Role: Guest
<!-- نقش: مهمان -->
- **Description**: Unauthenticated visitor viewing public info
- **Can**: View landing page, pricing, signup
- **Cannot**: Access any app functionality
- **Default on signup**: No

### Role: Member
<!-- نقش: عضو تیم -->
- **Description**: Regular team member who works on tasks
- **Can**: 
  - View all tasks in their teams
  - Create tasks
  - Edit own tasks
  - Complete/reopen tasks assigned to them
  - Comment on any task
  - View team members
- **Cannot**: 
  - Delete tasks created by others
  - Invite/remove team members
  - Change team settings
  - Access billing
- **Default on signup**: Yes

### Role: Admin
<!-- نقش: ادمین تیم -->
- **Description**: Team administrator with full control
- **Can**: 
  - Everything Member can do
  - Delete any task
  - Invite/remove team members
  - Change team settings
  - View team analytics
- **Cannot**: 
  - Access billing (only Owner)
- **Default on signup**: No (first user becomes Owner)

### Role: Owner
<!-- نقش: مالک -->
- **Description**: Team creator with billing access
- **Can**: 
  - Everything Admin can do
  - Access billing
  - Delete team
  - Transfer ownership
- **Cannot**: Nothing restricted
- **Default on signup**: Yes (for team creator only)

### Permission Matrix
| Action | Guest | Member | Admin | Owner |
|--------|-------|--------|-------|-------|
| View tasks | ❌ | ✅ | ✅ | ✅ |
| Create task | ❌ | ✅ | ✅ | ✅ |
| Edit own task | ❌ | ✅ | ✅ | ✅ |
| Edit any task | ❌ | ❌ | ✅ | ✅ |
| Delete own task | ❌ | ✅ | ✅ | ✅ |
| Delete any task | ❌ | ❌ | ✅ | ✅ |
| Invite member | ❌ | ❌ | ✅ | ✅ |
| Remove member | ❌ | ❌ | ✅ | ✅ |
| Team settings | ❌ | ❌ | ✅ | ✅ |
| Billing | ❌ | ❌ | ❌ | ✅ |
| Delete team | ❌ | ❌ | ❌ | ✅ |

---

## 2. Use Cases

### UC-001: Create Task
<!-- سناریو: ایجاد تسک جدید -->
- **Actor**: Member, Admin, Owner
- **Trigger**: User clicks "+" button or presses keyboard shortcut
- **Preconditions**: 
  - User is authenticated
  - User belongs to at least one team
- **Main Flow**:
  1. User clicks "+" or presses "N"
  2. System shows quick-add modal
  3. User enters task title (required)
  4. User optionally sets: assignee, due date, priority, description
  5. User clicks "Create" or presses Enter
  6. System validates input
  7. System creates task with status "todo"
  8. System shows success toast
  9. Task appears in task list
- **Postconditions**:
  - Task exists in database
  - Task visible to all team members
  - If assignee set, assignee receives notification
- **Failure Modes**:
  - Empty title → Show inline error, don't close modal
  - Network error → Save to local storage, sync when online, show "saved offline" indicator
  - Server error → Show error toast, keep modal open with data

### UC-002: Complete Task
<!-- سناریو: تکمیل تسک -->
- **Actor**: Assignee, Admin, Owner
- **Trigger**: User clicks checkbox or swipes right (mobile)
- **Preconditions**: 
  - Task status is "todo" or "in_progress"
  - User is assignee, Admin, or Owner
- **Main Flow**:
  1. User clicks checkbox
  2. System immediately shows visual completion (optimistic UI)
  3. System sends request to server
  4. Server updates task status to "done"
  5. Server records completion timestamp
  6. System moves task to "Done" column/section
- **Postconditions**:
  - Task status = "done"
  - completed_at timestamp set
  - Task creator notified (if different from completer)
- **Failure Modes**:
  - Network error → Revert checkbox, show "couldn't save" toast with retry
  - Permission denied → Revert checkbox, show "you can't complete this task"

### UC-003: Invite Team Member
<!-- سناریو: دعوت عضو جدید -->
- **Actor**: Admin, Owner
- **Trigger**: User clicks "Invite" in team settings
- **Preconditions**: 
  - User has Admin or Owner role
  - Team has available seats (if limited plan)
- **Main Flow**:
  1. User clicks "Invite Member"
  2. System shows invite modal
  3. User enters email address
  4. User selects role (Member or Admin)
  5. User clicks "Send Invite"
  6. System creates invite record with unique token
  7. System sends invite email
  8. System shows "Invite sent" toast
- **Postconditions**:
  - Invite record created with expiry (7 days)
  - Email sent to invitee
  - Pending invite visible in team settings
- **Failure Modes**:
  - Invalid email → Show inline validation error
  - User already in team → Show "already a member" error
  - No seats available → Show upgrade prompt
  - Email send fails → Create invite anyway, show "invite created but email failed, share link manually"

### UC-004: Login
<!-- سناریو: ورود به سیستم -->
- **Actor**: Guest (existing user)
- **Trigger**: User navigates to /login
- **Preconditions**: 
  - User has existing account
- **Main Flow**:
  1. User enters email
  2. User enters password
  3. User clicks "Login"
  4. System validates credentials
  5. System creates session
  6. System redirects to dashboard
- **Postconditions**:
  - Session created
  - User redirected to last visited page or dashboard
- **Failure Modes**:
  - Wrong password → Show "Invalid credentials" (don't reveal which is wrong)
  - Account locked → Show "Account locked, check email"
  - Too many attempts → Add captcha, then temporary lockout

### UC-005: Signup
<!-- سناریو: ثبت‌نام -->
- **Actor**: Guest
- **Trigger**: User clicks "Sign up" or follows invite link
- **Preconditions**: 
  - Email not already registered
- **Main Flow**:
  1. User enters email
  2. User enters password (min 8 chars)
  3. User enters name
  4. User clicks "Create Account"
  5. System validates input
  6. System creates user
  7. System sends verification email
  8. System logs user in
  9. System redirects to onboarding
- **Postconditions**:
  - User record created
  - Verification email sent
  - If from invite, user added to team
- **Failure Modes**:
  - Email exists → Show "Account exists, try login"
  - Weak password → Show password requirements
  - Invalid invite → Show "Invite expired or invalid"

---

## 3. Functional Requirements (Cross-Referenced)
<!-- نیازمندی‌های عملکردی - با ارجاع متقابل -->

### Authentication
| FR-ID | Requirement | Links to UC | Priority | Service |
|-------|-------------|-------------|----------|---------|
| FR-001 | User can signup with email/password | UC-005 | MUST | auth-service |
| FR-002 | User can login with email/password | UC-004 | MUST | auth-service |
| FR-003 | System issues JWT on successful login | UC-004 | MUST | auth-service |
| FR-004 | JWT expires after 15 minutes | UC-004 | MUST | auth-service |
| FR-005 | User can refresh token before expiry | - | MUST | auth-service |

### Task Management
| FR-ID | Requirement | Links to UC | Priority | Service |
|-------|-------------|-------------|----------|---------|
| FR-010 | User can create task with title | UC-001 | MUST | task-service |
| FR-011 | Task title is required (1-255 chars) | UC-001 | MUST | task-service |
| FR-012 | User can set optional assignee | UC-001 | SHOULD | task-service |
| FR-013 | User can set optional due date | UC-001 | SHOULD | task-service |
| FR-014 | User can complete own tasks | UC-002 | MUST | task-service |
| FR-015 | System sets completed_at on completion | UC-002 | MUST | task-service |
| FR-016 | Assignee receives notification on assignment | UC-001 | SHOULD | notification-service |

### Team Management
| FR-ID | Requirement | Links to UC | Priority | Service |
|-------|-------------|-------------|----------|---------|
| FR-020 | Admin/Owner can invite members | UC-003 | MUST | auth-service |
| FR-021 | Invite expires after 7 days | UC-003 | MUST | auth-service |
| FR-022 | Invitee receives email with link | UC-003 | MUST | notification-service |
| FR-023 | Admin/Owner can remove members | - | MUST | auth-service |
| FR-024 | Owner cannot be removed | - | MUST | auth-service |

### Traceability Matrix
<!-- ماتریس ردیابی - هر UC به کدام FR و سرویس وصل است -->
| UC-ID | Title | Related FRs | Primary Service | Secondary Services |
|-------|-------|-------------|-----------------|-------------------|
| UC-001 | Create Task | FR-010, FR-011, FR-012, FR-013, FR-016 | task-service | notification-service |
| UC-002 | Complete Task | FR-014, FR-015 | task-service | notification-service |
| UC-003 | Invite Member | FR-020, FR-021, FR-022 | auth-service | notification-service |
| UC-004 | Login | FR-002, FR-003, FR-004 | auth-service | - |
| UC-005 | Signup | FR-001 | auth-service | notification-service |

---

## 4. Success Criteria
<!-- معیار تکمیل -->

### MVP Launch Criteria
- [ ] All UC-001 to UC-005 implemented and tested
- [ ] RTL layout works on all pages
- [ ] Mobile responsive (320px to 1920px)
- [ ] Offline task creation works
- [ ] Page load < 3s on 3G
- [ ] Error rate < 1%
- [ ] Zero critical security vulnerabilities

### Post-Launch Success (Week 4)
- [ ] 10+ teams with 3+ active members each
- [ ] 100+ tasks created
- [ ] 50%+ task completion rate
- [ ] NPS > 30
- [ ] < 5 critical bugs reported
