# Frontend Specification: TaskFlow

## 1. Platform & Framework
<!-- پلتفرم و فریم‌ورک -->
- **Platform**: Web (PWA)
- **Framework**: React 18 + TypeScript
- **Build Tool**: Vite
- **UI Library**: Tailwind CSS + Headless UI
- **State Management**: Zustand (simple) or TanStack Query (server state)
- **RTL Support**: Yes (required)
- **Offline Support**: Service Worker + IndexedDB

---

## 2. Design Tokens
<!-- توکن‌های طراحی -->

```css
:root {
  /* Colors - Light Mode */
  --color-primary: #2563eb;        /* آبی اصلی */
  --color-primary-hover: #1d4ed8;
  --color-secondary: #64748b;      /* خاکستری */
  --color-success: #22c55e;        /* سبز */
  --color-warning: #f59e0b;        /* نارنجی */
  --color-error: #ef4444;          /* قرمز */
  
  --color-bg-primary: #ffffff;
  --color-bg-secondary: #f8fafc;
  --color-bg-tertiary: #f1f5f9;
  
  --color-text-primary: #0f172a;
  --color-text-secondary: #475569;
  --color-text-muted: #94a3b8;
  
  --color-border: #e2e8f0;
  
  /* Spacing */
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;
  --spacing-2xl: 48px;
  
  /* Border Radius */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-full: 9999px;
  
  /* Typography */
  --font-family: 'Vazirmatn', 'Inter', system-ui, sans-serif;
  --font-size-xs: 12px;
  --font-size-sm: 14px;
  --font-size-base: 16px;
  --font-size-lg: 18px;
  --font-size-xl: 20px;
  --font-size-2xl: 24px;
  
  /* Shadows */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
  
  /* Transitions */
  --transition-fast: 150ms ease;
  --transition-normal: 250ms ease;
}

/* Dark Mode */
[data-theme="dark"] {
  --color-bg-primary: #0f172a;
  --color-bg-secondary: #1e293b;
  --color-bg-tertiary: #334155;
  --color-text-primary: #f8fafc;
  --color-text-secondary: #cbd5e1;
  --color-border: #334155;
}
```

---

## 3. Component Library
<!-- کامپوننت‌های اصلی -->

### Component: Button
- **Purpose**: Primary action trigger
- **Variants**: primary, secondary, ghost, danger
- **Sizes**: sm, md, lg
- **States**: default, hover, active, disabled, loading
- **Props**: 
  - `variant`: 'primary' | 'secondary' | 'ghost' | 'danger'
  - `size`: 'sm' | 'md' | 'lg'
  - `loading`: boolean
  - `disabled`: boolean
  - `icon`: ReactNode (optional)
- **Accessibility**: 
  - Focusable with visible focus ring
  - `aria-disabled` when disabled
  - `aria-busy` when loading

### Component: Input
- **Purpose**: Text input field
- **Variants**: default, error
- **States**: default, focus, error, disabled
- **Props**: 
  - `label`: string
  - `error`: string (optional)
  - `hint`: string (optional)
  - `dir`: 'rtl' | 'ltr' | 'auto'
- **Accessibility**: 
  - Associated label via `htmlFor`
  - `aria-describedby` for error/hint
  - `aria-invalid` when error

### Component: TaskCard
<!-- کامپوننت: کارت تسک -->
- **Purpose**: Display single task in list/board
- **States**: default, hover, dragging, completed
- **Props**: 
  - `task`: Task object
  - `onComplete`: () => void
  - `onClick`: () => void
  - `draggable`: boolean
- **Accessibility**: 
  - Keyboard accessible (Enter to open, Space to complete)
  - `role="article"`
  - Announce status changes to screen readers

### Component: Modal
- **Purpose**: Overlay dialog for forms/confirmations
- **Variants**: default, fullscreen (mobile)
- **Props**: 
  - `isOpen`: boolean
  - `onClose`: () => void
  - `title`: string
  - `size`: 'sm' | 'md' | 'lg'
- **Accessibility**: 
  - Focus trap when open
  - `role="dialog"`, `aria-modal="true"`
  - Close on Escape
  - Return focus on close

### Component: Toast
- **Purpose**: Temporary notification message
- **Variants**: success, error, warning, info
- **Props**: 
  - `message`: string
  - `type`: 'success' | 'error' | 'warning' | 'info'
  - `duration`: number (ms)
- **Accessibility**: 
  - `role="alert"` for errors
  - `role="status"` for others
  - Auto-dismiss with adequate time

---

## 4. Page Structure
<!-- ساختار صفحات -->

### Page: Login
<!-- صفحه: ورود -->
- **Route**: `/login`
- **Auth Required**: No (redirect if logged in)
- **Components Used**: Input, Button, Link
- **Data Required**: None
- **Layout**: Centered card, full-screen bg

### Page: Signup
<!-- صفحه: ثبت‌نام -->
- **Route**: `/signup`
- **Auth Required**: No
- **Components Used**: Input, Button, Link
- **Data Required**: None

### Page: Dashboard
<!-- صفحه: داشبورد -->
- **Route**: `/`
- **Auth Required**: Any authenticated user
- **Components Used**: Sidebar, TeamSelector, TaskList, TaskCard, QuickAddButton
- **Data Required**: 
  - GET /auth/me (user + teams)
  - GET /teams/:id/tasks (when team selected)
- **Layout**: Sidebar + Main content

### Page: Task Detail
<!-- صفحه: جزئیات تسک -->
- **Route**: `/tasks/:id`
- **Auth Required**: Team member
- **Components Used**: Modal (or slide-over), TaskForm, CommentList, ActivityLog
- **Data Required**: 
  - GET /tasks/:id
  - GET /tasks/:id/comments

### Page: Team Settings
<!-- صفحه: تنظیمات تیم -->
- **Route**: `/teams/:id/settings`
- **Auth Required**: Admin, Owner
- **Components Used**: Tabs, MemberList, InviteForm, DangerZone
- **Data Required**: 
  - GET /teams/:id
  - GET /teams/:id/members
  - GET /teams/:id/invites

---

## 5. User Flows
<!-- فلوهای کاربری -->

### Flow: First-time User Onboarding
<!-- فلو: آنبوردینگ کاربر جدید -->
1. User signs up → `/signup`
2. Email verification sent → Show "check email" screen
3. User verifies (optional for MVP) → Auto-login
4. Create first team prompt → `/onboarding/team`
5. Team created → Redirect to dashboard with empty state
6. Empty state shows "Create your first task" CTA
- **Error States**: 
  - Email already exists → Show login link
  - Weak password → Show requirements inline

### Flow: Create Task (Quick Add)
<!-- فلو: ایجاد سریع تسک -->
1. User presses "N" or clicks "+" → Quick add modal opens
2. User types title → Title input focused
3. User presses Enter → Task created with defaults
4. Modal closes → Task appears in list with highlight animation
- **Error States**: 
  - Empty title → Shake input, show error
  - Offline → Save locally, show "saved offline" badge

### Flow: Complete Task
<!-- فلو: تکمیل تسک -->
1. User clicks checkbox → Immediate visual feedback (strikethrough)
2. API call in background
3. Task moves to "Done" section with animation
4. Success toast appears briefly
- **Error States**: 
  - API fails → Revert visual, show error toast with retry

### Flow: Invite Team Member
<!-- فلو: دعوت عضو -->
1. User goes to Team Settings → `/teams/:id/settings`
2. Clicks "Invite" button → Modal opens
3. Enters email, selects role → Validates email format
4. Clicks "Send" → API call
5. Modal closes, pending invite shows in list
- **Error States**: 
  - Invalid email → Inline error
  - Already member → Show "already in team" message
  - API error → Keep modal open, show error

---

## 6. Responsive Breakpoints
<!-- نقاط شکست ریسپانسیو -->

| Name | Min Width | Layout Changes |
|------|-----------|----------------|
| mobile | 0 | Single column, bottom nav, full-width cards, slide-over modals |
| tablet | 768px | Collapsible sidebar, 2-column task grid option |
| desktop | 1024px | Persistent sidebar, multi-column board view, side panel for task detail |
| wide | 1440px | Wider content area, more visible columns |

### Mobile-Specific Behaviors
<!-- رفتارهای خاص موبایل -->
- Swipe right on task → Complete
- Swipe left on task → Delete (with confirmation)
- Pull to refresh → Reload tasks
- Bottom sheet for task actions
- Sticky header with team selector

---

## 7. Accessibility Requirements
<!-- الزامات دسترس‌پذیری -->

### WCAG 2.1 AA Compliance
- **Contrast**: Minimum 4.5:1 for text, 3:1 for large text
- **Focus**: Visible focus indicator on all interactive elements
- **Keyboard**: Full keyboard navigation support
- **Screen Reader**: 
  - Semantic HTML
  - ARIA labels where needed
  - Live regions for dynamic content
- **Motion**: `prefers-reduced-motion` respected
- **Text Resize**: Works up to 200% zoom

### Keyboard Shortcuts
<!-- میانبرهای کیبورد -->
| Shortcut | Action |
|----------|--------|
| N | New task |
| / | Focus search |
| G + D | Go to Dashboard |
| G + S | Go to Settings |
| Esc | Close modal/panel |
| ? | Show keyboard shortcuts |

---

## 8. Offline Strategy
<!-- استراتژی آفلاین -->

### What Works Offline
- View cached tasks
- Create new tasks (queued)
- Complete tasks (queued)
- Edit tasks (queued)

### What Requires Connection
- Login/signup
- Invite members
- Real-time updates from others
- File uploads (if added later)

### Sync Behavior
- On reconnect: Push queued changes
- Conflict resolution: Last-write-wins with notification
- Offline indicator: Show banner when offline
- Queue status: Show pending sync count

---

## 9. Performance Targets
<!-- اهداف عملکرد -->

| Metric | Target | Measurement |
|--------|--------|-------------|
| First Contentful Paint | < 1.5s | Lighthouse |
| Time to Interactive | < 3s | Lighthouse |
| Largest Contentful Paint | < 2.5s | Lighthouse |
| Cumulative Layout Shift | < 0.1 | Lighthouse |
| Bundle Size (gzipped) | < 150KB | Build output |

### Optimization Strategies
- Code splitting by route
- Lazy load non-critical components
- Image optimization (WebP, lazy loading)
- Cache static assets (1 year)
- Cache API responses (stale-while-revalidate)
