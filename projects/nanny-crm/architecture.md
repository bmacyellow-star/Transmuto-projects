# Architecture: Nanny Agency CRM

> Created: 2026-03-07
> Status: ✅ Approved
> PRD: [PRD](prd.md)
> Author: Max 🚀 (Architect lens)

---

## Tech Stack

| Layer | Technology | Rationale |
|-------|-----------|-----------|
| Frontend | **Next.js 14+ (App Router)** | React-based, SSR/SSG, file-based routing, great DX. Vercel-native. |
| UI Framework | **Tailwind CSS + shadcn/ui** | Clean, customisable components. No vendor lock-in. Accessible by default. |
| Backend | **Next.js API Routes + Supabase** | API routes for business logic. Supabase handles auth, DB, storage, realtime. |
| Database | **Supabase (PostgreSQL)** | RLS for multi-tenancy. Strong relational model for complex agency data. |
| Auth | **Supabase Auth** | OTP (SMS/email) for nannies/families. Email/password for agency staff. Role-based via custom claims. |
| File Storage | **Supabase Storage** | Documents, contracts, certifications. Per-tenant bucket isolation. |
| Hosting | **Vercel** | Zero-config Next.js deployment. Preview deployments. Edge functions. |
| Email | **Resend** | Transactional emails (invites, notifications). Simple API. |
| PDF Generation | **@react-pdf/renderer** or **Puppeteer** | Contract generation from templates. |
| State Management | **React Server Components + TanStack Query** | Server-first data. Client cache for interactive views. |
| Forms | **React Hook Form + Zod** | Type-safe validation. Good for complex multi-step forms (onboarding, profiles). |

---

## System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                        VERCEL                            │
│  ┌─────────────────────────────────────────────────┐    │
│  │              Next.js Application                  │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────┐   │    │
│  │  │  Agency   │  │  Nanny   │  │   Family     │   │    │
│  │  │  Portal   │  │  Portal  │  │   Portal     │   │    │
│  │  └────┬─────┘  └────┬─────┘  └──────┬───────┘   │    │
│  │       │              │               │            │    │
│  │  ┌────┴──────────────┴───────────────┴───────┐   │    │
│  │  │           API Routes (Business Logic)      │   │    │
│  │  │  ┌────────┐ ┌────────┐ ┌────────────────┐ │   │    │
│  │  │  │ Auth   │ │ Tenant │ │ Domain Logic   │ │   │    │
│  │  │  │Middleware│ │ Guard  │ │ (services)     │ │   │    │
│  │  │  └────────┘ └────────┘ └────────────────┘ │   │    │
│  │  └────────────────────┬──────────────────────┘   │    │
│  └───────────────────────┼──────────────────────────┘    │
└──────────────────────────┼───────────────────────────────┘
                           │
┌──────────────────────────┼───────────────────────────────┐
│                     SUPABASE                              │
│  ┌──────────┐  ┌────────┴───┐  ┌──────────────────┐     │
│  │   Auth   │  │ PostgreSQL │  │  Storage          │     │
│  │          │  │   + RLS    │  │  (documents,      │     │
│  │ Email/PW │  │            │  │   contracts,      │     │
│  │ Magic Link│  │ Multi-tenant│  │   certifications)│     │
│  └──────────┘  └────────────┘  └──────────────────┘     │
│                                                           │
│  ┌──────────────────────────────────────────────────┐    │
│  │              Row Level Security (RLS)             │    │
│  │   Every query scoped to agency_id automatically   │    │
│  └──────────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────────┘
                           │
┌──────────────────────────┼───────────────────────────────┐
│                   EXTERNAL SERVICES                       │
│  ┌──────────┐  ┌────────────┐                            │
│  │  Resend  │  │  (Future)  │                            │
│  │  Email   │  │ Employment │                            │
│  │          │  │   Hero     │                            │
│  └──────────┘  └────────────┘                            │
└──────────────────────────────────────────────────────────┘
```

### Three Portals, One App

Rather than separate apps, we use Next.js route groups to serve three distinct experiences from one codebase:

```
app/
├── (agency)/          → Agency staff portal (full features)
│   ├── dashboard/
│   ├── contacts/
│   ├── nannies/
│   ├── families/
│   ├── placements/
│   ├── contracts/
│   ├── timesheets/
│   └── settings/
├── (nanny)/           → Nanny self-service portal
│   ├── profile/
│   ├── timesheets/
│   ├── documents/
│   └── placements/
├── (family)/          → Family lightweight portal
│   ├── placement/
│   ├── timesheets/
│   └── notifications/
├── (auth)/            → Shared auth flows
│   ├── login/
│   ├── register/
│   └── invite/
└── api/               → API routes
```

**Why one app:** Shared types, shared components, single deployment. Role-based middleware routes users to their portal automatically after login.

---

## Data Model

### Core Entities

```
Agency (tenant)
├── id (uuid, PK)
├── name
├── logo_url
├── settings (jsonb)
├── subscription_tier
├── created_at
└── updated_at

AgencyUser (staff)
├── id (uuid, PK)
├── agency_id (FK → Agency)
├── user_id (FK → auth.users)
├── role (enum: owner, admin, coordinator)
├── name
├── email
├── created_at
└── updated_at

Contact
├── id (uuid, PK)
├── agency_id (FK → Agency)
├── type (enum: nanny, family, referrer, partner, other)
├── first_name
├── last_name
├── email
├── phone
├── address (jsonb)
├── tags (text[])
├── notes (text)
├── created_at
└── updated_at

Nanny (extends Contact)
├── id (uuid, PK)
├── contact_id (FK → Contact)
├── agency_id (FK → Agency)
├── user_id (FK → auth.users, nullable — set when invited to portal)
├── status (enum: enquiry, application, interview, reference_check, onboarding, active, inactive)
├── qualifications (jsonb)
├── availability (jsonb)
├── preferences (jsonb)
├── hourly_rate
├── work_rights (jsonb)
├── emergency_contact (jsonb)
├── created_at
└── updated_at

Family (extends Contact)
├── id (uuid, PK)
├── contact_id (FK → Contact)
├── agency_id (FK → Agency)
├── user_id (FK → auth.users, nullable — set when invited to portal)
├── status (enum: prospect, active, inactive)
├── children (jsonb[]) — [{name, dob, needs}]
├── care_requirements (jsonb)
├── schedule_preferences (jsonb)
├── location (jsonb)
├── created_at
└── updated_at

Placement
├── id (uuid, PK)
├── agency_id (FK → Agency)
├── nanny_id (FK → Nanny)
├── family_id (FK → Family)
├── status (enum: proposed, confirmed, active, completed, terminated)
├── start_date
├── end_date (nullable)
├── schedule (jsonb) — [{day, start_time, end_time}]
├── hourly_rate
├── terms (text)
├── created_at
└── updated_at

Contract
├── id (uuid, PK)
├── agency_id (FK → Agency)
├── placement_id (FK → Placement)
├── nanny_id (FK → Nanny)
├── family_id (FK → Family)
├── template_id (FK → ContractTemplate)
├── status (enum: draft, sent, signed, active, expired, terminated)
├── content (text) — rendered contract content
├── document_url — stored PDF
├── signed_at
├── expires_at
├── created_at
└── updated_at

ContractTemplate
├── id (uuid, PK)
├── agency_id (FK → Agency)
├── name
├── content (text) — template with merge fields {{nanny.name}}, {{placement.rate}}, etc.
├── category (enum: employment, placement, casual, permanent)
├── is_default (boolean)
├── created_at
└── updated_at

Timesheet
├── id (uuid, PK)
├── agency_id (FK → Agency)
├── nanny_id (FK → Nanny)
├── placement_id (FK → Placement)
├── date
├── start_time
├── end_time
├── break_minutes
├── total_hours (computed)
├── notes
├── status (enum: draft, submitted, approved, rejected)
├── reviewed_by (FK → AgencyUser, nullable)
├── reviewed_at
├── rejection_reason
├── created_at
└── updated_at

Document
├── id (uuid, PK)
├── agency_id (FK → Agency)
├── contact_id (FK → Contact)
├── nanny_id (FK → Nanny, nullable)
├── type (enum: wwcc, first_aid, police_check, visa, qualification, contract, other)
├── name
├── file_url
├── expires_at (nullable)
├── status (enum: pending, verified, expired)
├── created_at
└── updated_at

OnboardingChecklist
├── id (uuid, PK)
├── agency_id (FK → Agency)
├── nanny_id (FK → Nanny)
├── items (jsonb[]) — [{title, description, required, completed, completed_at}]
├── progress_pct (computed)
├── created_at
└── updated_at

ActivityLog
├── id (uuid, PK)
├── agency_id (FK → Agency)
├── contact_id (FK → Contact, nullable)
├── user_id (FK → auth.users)
├── action (text) — e.g. "created_nanny", "approved_timesheet", "generated_contract"
├── details (jsonb)
├── created_at
└── (no updated_at — immutable log)
```

### Key Relationships

```
Agency ──1:N──→ AgencyUser (staff)
Agency ──1:N──→ Contact ──1:1──→ Nanny
                         ──1:1──→ Family
Agency ──1:N──→ Placement ←── Nanny + Family
Placement ──1:N──→ Timesheet
Placement ──1:1──→ Contract
Agency ──1:N──→ ContractTemplate
Contact ──1:N──→ Document
Contact ──1:N──→ ActivityLog
Nanny ──1:1──→ OnboardingChecklist
```

---

## Multi-Tenancy Strategy

**Approach:** Shared database with Row Level Security (RLS)

Every table has an `agency_id` column. Every RLS policy enforces:
```sql
agency_id = (SELECT agency_id FROM agency_users WHERE user_id = auth.uid())
```

**For nanny/family portal users:**
```sql
-- Nannies see only their own data
user_id = auth.uid()

-- Families see only their placement data
family_id IN (SELECT id FROM families WHERE user_id = auth.uid())
```

**Why shared DB over schema-per-tenant:**
- Simpler at this scale (targeting 100s of agencies, not 10,000s)
- Easier migrations
- Lower infrastructure cost
- RLS is PostgreSQL-native and battle-tested in Supabase

---

## Authentication Flow

```
1. Agency owner signs up (email/password) → creates Agency + first AgencyUser (owner role)
2. Owner invites staff → AgencyUser created, invite email sent via Resend (email/password login)
3. Staff invites nanny → Contact + Nanny created, invite email with OTP link
4. Staff invites family → Contact + Family created, invite email with OTP link
5. Nannies/families login via OTP (email or SMS) → no password to remember
6. On login → middleware reads user role → redirects to correct portal
```

**Role resolution:**
```
auth.users.id → check AgencyUser? → Agency portal
              → check Nanny?      → Nanny portal
              → check Family?     → Family portal
```

---

## API Design

### Route Structure
```
/api/contacts          → CRUD + search + filter
/api/nannies           → CRUD + pipeline management
/api/families          → CRUD + requirements
/api/placements        → CRUD + matching + status
/api/contracts         → CRUD + generate from template
/api/contract-templates → CRUD
/api/timesheets        → CRUD + submit + approve/reject
/api/documents         → CRUD + upload + expiry check
/api/onboarding        → CRUD + progress
/api/team              → invite + roles + manage
/api/settings          → agency settings + branding
/api/activity           → read-only activity log
```

All routes enforce:
1. Authentication (Supabase Auth middleware)
2. Tenant isolation (agency_id from session)
3. Role-based access (permission check per route)

---

## Security

- **Authentication:** Supabase Auth (email/password + magic link)
- **Authorization:** Role-based permissions enforced in middleware + RLS at DB level (defense in depth)
- **Data isolation:** RLS on every table. No cross-agency data access possible.
- **File access:** Supabase Storage policies scoped to agency. Signed URLs for document access.
- **Secrets:** Environment variables via Vercel. No secrets in code.
- **HTTPS:** Enforced by Vercel.
- **Input validation:** Zod schemas on all API inputs.

---

## Infrastructure

- **Environments:** Development (local) → Preview (Vercel PR deploys) → Production
- **Database:** Supabase project (free tier to start, scale as needed)
- **Deployment:** Git push to main → Vercel auto-deploys
- **Monitoring:** Vercel analytics + Supabase dashboard. Sentry for error tracking (post-MVP).
- **Backups:** Supabase handles daily backups on Pro plan

---

## File / Folder Structure

```
nanny-crm/
├── src/
│   ├── app/
│   │   ├── (agency)/           → Agency portal pages
│   │   ├── (nanny)/            → Nanny portal pages
│   │   ├── (family)/           → Family portal pages
│   │   ├── (auth)/             → Auth pages
│   │   ├── api/                → API routes
│   │   ├── layout.tsx          → Root layout
│   │   └── globals.css
│   ├── components/
│   │   ├── ui/                 → shadcn/ui components
│   │   ├── agency/             → Agency-specific components
│   │   ├── nanny/              → Nanny-specific components
│   │   ├── family/             → Family-specific components
│   │   └── shared/             → Shared components
│   ├── lib/
│   │   ├── supabase/
│   │   │   ├── client.ts       → Browser client
│   │   │   ├── server.ts       → Server client
│   │   │   ├── admin.ts        → Service role client
│   │   │   └── middleware.ts   → Auth middleware
│   │   ├── services/           → Business logic
│   │   │   ├── contacts.ts
│   │   │   ├── nannies.ts
│   │   │   ├── families.ts
│   │   │   ├── placements.ts
│   │   │   ├── contracts.ts
│   │   │   ├── timesheets.ts
│   │   │   └── documents.ts
│   │   ├── utils/              → Helpers
│   │   └── validations/        → Zod schemas
│   ├── hooks/                  → Custom React hooks
│   └── types/                  → TypeScript types
├── supabase/
│   ├── migrations/             → SQL migrations
│   ├── seed.sql                → Dev seed data
│   └── config.toml
├── public/
├── docs/
│   ├── planning-artifacts/
│   └── implementation-artifacts/
├── .planning/                  → GSD execution state
├── tests/
├── .env.local.example
├── next.config.js
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## Mobile & App Store Strategy

### PWA-Ready from Day One
The app ships as a Progressive Web App:
- Web app manifest for "Add to Home Screen"
- Service worker for offline capability (cached pages, queued timesheet submissions)
- Push notifications via Web Push API (supported on Android, improving on iOS)
- Zero cost to implement alongside the responsive web build

### Path to App Store
When App Store presence is needed (likely for the family portal first):

| Phase | Approach | Effort | Result |
|-------|----------|--------|--------|
| MVP | PWA | Included | Home screen install, offline, push (Android) |
| V2 | Capacitor wrap | 1-2 weeks | Same codebase → native shell → App Store + Play Store |
| V3 (if needed) | React Native | 4-8 weeks | True native family app, shares TS types + API layer |

**Recommendation:** PWA now → Capacitor when agencies ask for App Store presence → React Native only if premium native UX becomes a competitive requirement.

### Mobile-First Design Priority
- **Family portal:** Mobile-first (primary device). Minimal UI, large touch targets, single-column.
- **Nanny portal:** Mobile-first (timesheets submitted on phone). Quick-entry optimised.
- **Agency portal:** Desktop-first (complex data, dashboards). Responsive but not mobile-primary.

---

## Technical Decisions

| Decision | Options Considered | Choice | Why |
|----------|-------------------|--------|-----|
| Framework | Next.js vs Remix vs Vite+React | Next.js (App Router) | Best Vercel integration, SSR, RSC, file routing |
| UI | Material UI vs Chakra vs shadcn/ui | shadcn/ui + Tailwind | Customisable, accessible, no vendor lock-in, lightweight |
| Multi-tenancy | Schema-per-tenant vs shared DB + RLS | Shared DB + RLS | Simpler at scale, lower cost, Supabase-native |
| Auth | Custom vs Clerk vs Supabase Auth | Supabase Auth | Already using Supabase, good enough, free |
| PDF generation | React-PDF vs Puppeteer vs external | @react-pdf/renderer | No headless browser needed, works serverless |
| Email | SendGrid vs Resend vs Postmark | Resend | Simple API, good DX, React Email templates |
| Portal architecture | Separate apps vs monorepo vs route groups | Route groups in one app | Shared types, single deployment, simpler |

---

## Scale & Growth Path

| Scale | Status | Infrastructure Notes |
|-------|--------|---------------------|
| 1–100 agencies | ✅ Comfortable | Supabase free/pro tier, single Vercel deployment |
| 100–500 agencies | ✅ Comfortable | Supabase Pro, consider read replicas |
| 500–2,000 agencies | ⚠️ Tune | Database indexing, query optimisation, edge caching. Supabase Team/Enterprise |
| 2,000–10,000 agencies | ⚠️ Review | Connection pooling (PgBouncer), background job queue, CDN for documents |
| 10,000+ agencies | 🔄 Evolve | Dedicated API service, managed Postgres, microservices for heavy workloads |

**First bottlenecks at scale:**
1. PDF generation → move to background queue (Bull/Redis or Supabase Edge Function)
2. Document storage → CDN + signed URLs (already planned)
3. Timesheet queries → indexes + materialised views for reporting
4. Notifications → Supabase Realtime or dedicated service

**Honest assessment:** This stack comfortably handles thousands of agencies. Product-market-fit will be the challenge long before infrastructure.

---

## Constraints & Trade-offs

1. **Shared DB + RLS over schema isolation** — Simpler but requires disciplined RLS policies. Every new table must have RLS. Tested in CI.
2. **One Next.js app for three portals** — Simpler deployment but larger bundle. Mitigated by route-based code splitting.
3. **No real-time in MVP** — Supabase supports realtime but adds complexity. Polling or page refresh for now. Realtime for timesheets/notifications in v2.
4. **PDF generation serverless** — @react-pdf works in serverless but complex templates may need Puppeteer (move to Edge Function if needed).
5. **No mobile app** — Responsive web covers MVP. Native app if adoption demands it.

---

## Approval

- [ ] Stack confirmed
- [ ] Architecture reviewed
- [ ] Security approach agreed
- [ ] Data model reviewed
- [ ] Bmac approved
- [ ] Ready to proceed to Epics & Stories

> **Next step:** Break down into Epics and Stories for implementation.
