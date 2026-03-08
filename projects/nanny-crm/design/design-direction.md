# Design Direction: Nanny Agency CRM

> Created: 2026-03-08
> Status: Draft — awaiting Bmac's approval
> PRD: [PRD](../prd.md)
> Moodboard: [Moodboard](moodboard.md)
> Author: Max 🎨

---

## Visual Summary

Warm minimal SaaS. Light, airy screens on a soft off-white canvas. Rounded cards with subtle shadows. One confident accent colour against warm neutrals. Professional enough for agency owners, approachable enough that nannies and families feel at ease. The UI should feel calm, organised, and invisible — the focus is always on the content, never the chrome.

---

## Design System

- **Component library:** shadcn/ui (customised tokens)
- **CSS framework:** Tailwind CSS
- **Theme base:** Custom — warm neutral palette built on shadcn primitives
- **Icon library:** Lucide (shadcn default) — outline style, 1.5px stroke
- **Animation:** CSS transitions + Tailwind animate. Framer Motion only where needed (page transitions, complex choreography)
- **Charts:** Recharts (shadcn charts wrapper) with muted colour palette

---

## Colour

**Mode:** Light only (MVP)

### Palette

| Token | Value | Usage |
|-------|-------|-------|
| `--background` | `#FAFAF8` | Page canvas — warm off-white |
| `--card` | `#FFFFFF` | Card/surface backgrounds |
| `--card-foreground` | `#1A1A1A` | Primary text on cards |
| `--foreground` | `#1A1A1A` | Primary text |
| `--muted` | `#F5F3EF` | Muted backgrounds, hover states |
| `--muted-foreground` | `#737067` | Secondary text, placeholders |
| `--border` | `#E8E5DF` | Borders, dividers — warm grey |
| `--primary` | `#2A7A6E` | Primary accent — warm teal. Main actions, active states, links |
| `--primary-foreground` | `#FFFFFF` | Text on primary |
| `--secondary` | `#F0EDE7` | Secondary backgrounds, subtle emphasis |
| `--secondary-foreground` | `#4A4740` | Text on secondary |
| `--accent` | `#F0EDE7` | Accent backgrounds (same family as secondary) |
| `--destructive` | `#D4483B` | Errors, delete actions — warm red |
| `--warning` | `#D4943B` | Warnings, expiring documents — warm amber |
| `--success` | `#3B8A5E` | Success states, completed — sage green |
| `--ring` | `#2A7A6E` | Focus rings — matches primary |

### Colour Principles
- Background is never pure `#FFFFFF` — always warm
- Accent colours are muted/earthy, not saturated
- Status colours (pipeline stages, document states) use the same muted family
- Charts use a palette of muted warm tones, no neon

### Pipeline / Status Colours

| Status | Colour | Used For |
|--------|--------|----------|
| New/Enquiry | `#A8A29E` (warm grey) | New leads, draft items |
| In Progress | `#2A7A6E` (primary teal) | Active states, confirmed |
| Needs Attention | `#D4943B` (warm amber) | Pending review, expiring |
| Complete/Success | `#3B8A5E` (sage green) | Approved, signed, active |
| Rejected/Terminated | `#D4483B` (warm red) | Rejected, expired, terminated |

---

## Typography

| Role | Font | Weight | Size (base) |
|------|------|--------|-------------|
| **Headings** (h1-h3) | Plus Jakarta Sans | 600 (semibold) | 30/24/20px |
| **Subheadings** (h4-h6) | Plus Jakarta Sans | 500 (medium) | 18/16/14px |
| **Body** | Inter | 400 (regular) | 14px |
| **Body emphasis** | Inter | 500 (medium) | 14px |
| **Labels/UI** | Inter | 500 (medium) | 13px |
| **Small/Caption** | Inter | 400 (regular) | 12px |
| **Mono** (data, IDs) | JetBrains Mono | 400 | 13px |

**Scale:** 1.25 modular scale from 14px base
**Line height:** 1.5 for body, 1.3 for headings
**Letter spacing:** -0.01em for headings (slightly tight), 0 for body

### Font Loading
- Plus Jakarta Sans: Google Fonts (weights 500, 600)
- Inter: Google Fonts or `next/font` (weights 400, 500)
- JetBrains Mono: Google Fonts (weight 400) — only loaded where needed

---

## Layout

### Agency Portal (Desktop-First)

```
┌──────────────────────────────────────────────────┐
│  Logo   Agency Name              🔔  👤  Settings │  ← Top bar (minimal)
├────────────┬─────────────────────────────────────┤
│            │                                      │
│  Dashboard │   Page Content                       │
│  Contacts  │                                      │
│  Nannies   │   ┌─────────┐  ┌─────────┐          │
│  Families  │   │  Card    │  │  Card   │          │
│  Placements│   │         │  │         │          │
│  Contracts │   └─────────┘  └─────────┘          │
│  Timesheets│                                      │
│  Settings  │   ┌──────────────────────┐          │
│            │   │  Table / List View   │          │
│            │   │                      │          │
│            │   └──────────────────────┘          │
│            │                                      │
└────────────┴─────────────────────────────────────┘
```

- **Navigation:** Left sidebar — collapsible, icon + label
- **Page structure:** Sidebar + main content area
- **Max content width:** 1280px (centred on wide screens)
- **Density:** Balanced — 24px section gaps, 16px card padding, 12px between list items

### Nanny Portal (Mobile-First)

```
┌──────────────────┐
│  Logo    🔔  👤   │  ← Simple top bar
├──────────────────┤
│                  │
│  ┌────────────┐  │
│  │ Quick      │  │  ← Primary action card
│  │ Actions    │  │
│  └────────────┘  │
│                  │
│  ┌────────────┐  │
│  │ Content    │  │  ← Stacked cards
│  │ Cards      │  │
│  └────────────┘  │
│                  │
├──────────────────┤
│ 🏠  📋  ➕  📄  👤 │  ← Bottom tab bar
└──────────────────┘
```

- **Navigation:** Bottom tab bar (5 items max)
- **Page structure:** Single column, stacked cards
- **Primary action:** Floating or prominent "Submit Timesheet" button
- **Touch targets:** Minimum 44px

### Family Portal (Mobile-First, Ultra-Minimal)

```
┌──────────────────┐
│  Logo            │  ← Minimal header
├──────────────────┤
│                  │
│  Welcome, [Name] │
│                  │
│  ┌────────────┐  │
│  │ Placement  │  │  ← One main card
│  │ Summary    │  │
│  └────────────┘  │
│                  │
│  ┌────────────┐  │
│  │ Recent     │  │  ← Activity feed
│  │ Activity   │  │
│  └────────────┘  │
│                  │
└──────────────────┘
```

- **Navigation:** Almost none — single page with sections
- **Interaction:** Mostly read-only. Action items are pushed to them.
- **Feel:** Like a notification summary, not an app

### Responsive Breakpoints

| Breakpoint | Target | Layout |
|------------|--------|--------|
| `< 640px` | Mobile | Single column, bottom nav (nanny/family) |
| `640-1024px` | Tablet | Collapsed sidebar (agency), stacked cards |
| `> 1024px` | Desktop | Full sidebar + content (agency) |

---

## Component Patterns

### Cards
- Background: `#FFFFFF` on `#FAFAF8` canvas
- Border: 1px `--border` OR no border + subtle shadow (`shadow-sm`)
- Radius: `12px` (rounded-xl)
- Padding: 16-24px

### Buttons
- Primary: `--primary` bg, white text, rounded-lg (8px)
- Secondary: `--secondary` bg, dark text, rounded-lg
- Ghost: transparent, hover `--muted`
- Destructive: `--destructive` bg, white text
- Size: 36px height default, 44px for mobile touch targets

### Tables (Agency Portal)
- Clean, minimal borders — bottom border only between rows
- Header: `--muted` background, `--muted-foreground` text, uppercase 12px
- Row hover: `--muted` background
- No zebra striping — hover is enough

### Status Badges
- Pill-shaped (full radius)
- Muted background tint of status colour + darker text
- Example: "Active" → light sage bg + dark sage text

### Forms
- Input height: 40px
- Border: 1px `--border`, radius 8px
- Focus: 2px ring `--ring` (primary teal)
- Labels: above input, `--muted-foreground`, 13px medium
- Validation: inline below field, `--destructive` for errors

### Empty States
- Centred illustration or icon (muted)
- Short headline + description
- CTA button to create first item
- Tone: helpful, not sad

### Modals / Sheets
- Agency: Slide-over sheet from right (preserves page context)
- Mobile: Bottom sheet (natural thumb reach)
- Overlay: subtle dark scrim

---

## Motion & Interaction

| Element | Transition | Duration | Easing |
|---------|-----------|----------|--------|
| Hover states | Background colour | 150ms | ease |
| Button press | Scale 0.98 | 100ms | ease-out |
| Page transitions | Fade | 200ms | ease |
| Sidebar collapse | Width | 200ms | ease-in-out |
| Sheet/Modal open | Slide + fade | 250ms | ease-out |
| Sheet/Modal close | Slide + fade | 200ms | ease-in |
| Skeleton shimmer | Opacity pulse | 1.5s | linear (loop) |
| Toast notifications | Slide in from top-right | 200ms | ease-out |

**Rule:** If you can't tell whether something animated, it's doing its job.

---

## Agency Branding

The platform supports per-agency branding (FR1.3):

- **Logo:** Displayed in sidebar header. Max height 32px.
- **Agency name:** In sidebar and page titles
- **Brand colour:** Optional — agencies can set a primary accent that overrides `--primary` for their instance. Falls back to default teal.
- **Implementation:** CSS custom property override at agency level, stored in `agency.settings.brand_color`

---

## Key Screens (Wireframe Notes)

### 1. Agency Dashboard
- Top row: 4 metric cards (active nannies, families, placements, pending timesheets)
- Quick actions row: "New Nanny", "New Family", "New Placement" buttons
- Recent activity feed (left 60%) + Notifications panel (right 40%)
- Upcoming: document expiries, unsigned contracts

### 2. Contact List
- Search bar + filter pills (type, tags, status)
- Table view with avatar, name, type badge, email, phone, last activity
- Click → slide-over sheet with full profile

### 3. Nanny Pipeline (Kanban)
- Horizontal kanban columns: Enquiry → Application → Interview → Reference Check → Onboarding → Active
- Cards show: avatar, name, stage duration, key flag (missing docs, etc.)
- Drag to advance (desktop) or tap-to-move (mobile)

### 4. Nanny Timesheet Submission (Mobile)
- Date picker (default: today)
- Placement selector (if multiple — most nannies have one)
- Start time / End time (large, easy tap)
- Break duration (quick presets: 0, 15, 30, 60 min)
- Notes (optional)
- Submit button (full width, primary)
- Total hours calculated and displayed live

### 5. Family Portal Home
- Welcome header with family name
- Current placement card: nanny name + photo, schedule summary, next session
- Recent timesheets accordion (last 4 weeks)
- Action items (if any) — contract to review, feedback requested

---

## Design Tokens (Tailwind Config)

```typescript
// tailwind.config.ts — design token overrides

const config = {
  theme: {
    extend: {
      colors: {
        background: '#FAFAF8',
        foreground: '#1A1A1A',
        card: { DEFAULT: '#FFFFFF', foreground: '#1A1A1A' },
        primary: { DEFAULT: '#2A7A6E', foreground: '#FFFFFF' },
        secondary: { DEFAULT: '#F0EDE7', foreground: '#4A4740' },
        muted: { DEFAULT: '#F5F3EF', foreground: '#737067' },
        accent: { DEFAULT: '#F0EDE7', foreground: '#4A4740' },
        destructive: { DEFAULT: '#D4483B', foreground: '#FFFFFF' },
        warning: { DEFAULT: '#D4943B', foreground: '#FFFFFF' },
        success: { DEFAULT: '#3B8A5E', foreground: '#FFFFFF' },
        border: '#E8E5DF',
        ring: '#2A7A6E',
      },
      fontFamily: {
        heading: ['Plus Jakarta Sans', 'sans-serif'],
        sans: ['Inter', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      borderRadius: {
        lg: '8px',
        xl: '12px',
        '2xl': '16px',
        pill: '9999px',
      },
      boxShadow: {
        card: '0 1px 3px rgba(0,0,0,0.04), 0 1px 2px rgba(0,0,0,0.02)',
      },
    },
  },
}
```

---

## Approval

- [x] Moodboard reviewed
- [ ] Colour palette confirmed
- [ ] Typography confirmed
- [ ] Layout approach confirmed
- [ ] Key screen wireframes reviewed
- [ ] Bmac approved
- [ ] Ready to proceed to Architecture review (design-aware)

> **Next step:** Bmac reviews and approves. Then we update architecture if needed and proceed to stories.
