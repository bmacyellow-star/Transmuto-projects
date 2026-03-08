# PRD: Nanny Agency CRM

> Created: 2026-03-07
> Status: Draft
> Brief: [Product Brief](brief.md)
> Author: Max 🚀 (PM lens)

---

## Overview

### Vision
A single platform for nanny agencies to manage their entire operation — recruitment, contracts, placements, timesheets, and contacts — while giving families a seamless, hands-off experience.

### Background
Nanny agencies in Australia run on fragmented tools. No platform handles the full lifecycle while keeping the family experience effortless. This product fills that gap: powerful for the agency, invisible for the family.

### Design Principles
1. **Agency-powerful, family-effortless** — The agency gets depth. The family gets simplicity.
2. **Data captured once, used everywhere** — Profile data flows into contracts, timesheets, placements automatically.
3. **Mobile-first for nannies and families** — They live on their phones.
4. **Agency-branded** — The platform feels like the agency's own tool.

---

## User Roles & Permissions

| Role | Access Level | Description |
|------|-------------|-------------|
| Agency Owner | Full admin | Everything — billing, settings, team management, all data |
| Agency Admin | Full operational | All operational features, no billing/subscription management |
| Coordinator | Operational | Manage nannies, families, placements, timesheets. No settings/team mgmt |
| Nanny | Self-service portal | Own profile, timesheets, documents, placement details |
| Family | Lightweight portal | Placement info, FYI timesheets, action items only when needed |

---

## Functional Requirements

### FR1: Agency Dashboard
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.1 | Overview dashboard showing key metrics | Dashboard displays: active nannies, active families, current placements, pending timesheets, recent activity |
| FR1.2 | Quick-action buttons for common tasks | Can start new nanny intake, new family registration, new placement from dashboard |
| FR1.3 | Agency branding | Agency logo displayed in header. Agency name in page titles. Configurable in settings |
| FR1.4 | Notification centre | Pending items surfaced: unsigned contracts, unapproved timesheets, expiring documents |

### FR2: Contact List / CRM
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR2.1 | Centralised contact directory | All contacts (nannies, families, referrers, partners, prospects) in one searchable list |
| FR2.2 | Contact profiles | Each contact has: name, type, phone, email, address, tags, notes, activity history |
| FR2.3 | Tags and filtering | Contacts can be tagged (e.g. "active nanny", "prospect", "VIP family") and filtered |
| FR2.4 | Activity log | All interactions with a contact logged chronologically (calls, emails, notes, status changes) |
| FR2.5 | Contact type categorisation | Contacts categorised as: Nanny, Family, Referrer, Partner, Other |

### FR3: Nanny Management
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.1 | Nanny profile | Comprehensive profile: personal details, qualifications, certifications, availability, preferences, work history, documents |
| FR3.2 | Recruitment pipeline | Kanban-style pipeline: Enquiry → Application → Interview → Reference Check → Onboarding → Active |
| FR3.3 | Document storage | Upload and track: Working With Children Check, First Aid cert, police check, visa, qualifications |
| FR3.4 | Document expiry tracking | System flags documents approaching expiry (30/60/90 day warnings) |
| FR3.5 | Availability management | Nannies can set availability. Agency can view availability across all nannies |
| FR3.6 | Nanny self-service portal | Nanny can: update profile, submit timesheets, view placements, upload documents, see contract details |

### FR4: Family Management
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.1 | Family profile | Profile: parent details, children (names, ages, needs), address, care requirements, preferences, schedule |
| FR4.2 | Requirements capture | Structured capture of: hours needed, days, special requirements, children's needs, location preferences |
| FR4.3 | Family portal (lightweight) | Family can view: current nanny details, placement info, FYI timesheets. Only prompted when action needed |
| FR4.4 | Communication preferences | Family sets preferred contact method and notification frequency |

### FR5: Placement Management
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.1 | Create placement | Link a nanny to a family with: start date, end date (if temp), schedule, rate, terms |
| FR5.2 | Placement overview | Agency can see all active placements, upcoming starts, recent endings |
| FR5.3 | Matching assistance | Filter available nannies by: availability, location, qualifications, preferences. Surface potential matches for a family's requirements |
| FR5.4 | Placement history | Full history of all placements for both nannies and families |
| FR5.5 | Placement status | Statuses: Proposed → Confirmed → Active → Completed / Terminated |

### FR6: Contract Management
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.1 | Contract templates | Agency can create and manage contract templates with merge fields |
| FR6.2 | Contract generation | Generate contract from template, auto-populated with nanny/family/placement data |
| FR6.3 | Contract tracking | Track status: Draft → Sent → Signed → Active → Expired / Terminated |
| FR6.4 | Document storage | Generated contracts stored against the relevant placement, nanny, and family records |
| FR6.5 | AU compliance fields | Templates support AU-specific fields: Fair Work info, award rates, NES entitlements, notice periods |

### FR7: Timesheets
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR7.1 | Nanny timesheet submission | Nanny submits: date, start time, end time, break, placement, notes |
| FR7.2 | Approval workflow | Submitted → Agency Review → Approved / Rejected (with reason) |
| FR7.3 | Family FYI view | Family can see approved timesheets for their placement. View only — no action required unless flagged |
| FR7.4 | Timesheet summary | Agency dashboard: weekly/monthly summary per nanny, per placement |
| FR7.5 | Overtime/penalty rate flags | System flags hours that may attract overtime or penalty rates under AU awards |

### FR8: Onboarding
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR8.1 | Onboarding checklists | Configurable checklist per nanny: documents to collect, forms to complete, training to do |
| FR8.2 | Onboarding progress | Agency can see onboarding completion % per nanny |
| FR8.3 | Nanny self-service onboarding | Nanny can complete onboarding steps from their portal (upload docs, fill forms) |

### FR9: Team & Multi-user
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR9.1 | Team management | Agency owner can invite team members, assign roles |
| FR9.2 | Role-based permissions | Access controlled by role (Owner, Admin, Coordinator) |
| FR9.3 | Activity attribution | All actions logged with which team member performed them |

### FR11-A: Public Intake Forms (Agency-Branded)
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR11A.1 | Public nanny application form | Agency has a unique URL (e.g. app.nannyCRM.com/apply/little-stars) that nannies can access without logging in. Captures: personal details, qualifications, availability, preferences. Submits directly into the CRM as a new nanny contact in "Enquiry" status. |
| FR11A.2 | Public family registration form | Agency has a unique URL (e.g. app.nannyCRM.com/register/little-stars) for families. Captures: parent details, children, care needs, preferences. Submits into CRM as a new family contact in "Prospect" status. |
| FR11A.3 | Agency branding on public forms | Public forms display: agency logo, agency name, agency colour (optional). The form feels like the agency's own tool, not a generic platform. |
| FR11A.4 | No login required | Public forms are accessible without authentication. Email verification optional (post-MVP). |
| FR11A.5 | Confirmation page | After submission, show a branded thank-you page with next steps ("We'll be in touch within 48 hours"). |
| FR11A.6 | Embeddable (future) | Forms can be embedded into an agency's existing website via iframe or script tag. Out of scope for MVP but architecture should not prevent it. |
| FR11A.7 | Form customisation (future) | Agencies can toggle fields on/off and reorder sections. Out of scope for MVP — all agencies get the same form structure. |

**Key principle:** These forms are the agency's first impression. They must be beautiful, minimal, and fast to complete. Select over input. No unnecessary fields. Mobile-first.

### FR11: Form UX & Data Entry
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR11.1 | Multi-step wizard pattern | All complex forms (nanny profile, family profile, placement creation) use a step-by-step wizard with progress indicator. Max 4-6 fields visible per step. |
| FR11.2 | Select over input | Where a finite set of options exists, use select/dropdown/toggle/radio — not free text. Examples: qualifications, availability days, suburb, care type, certification type |
| FR11.3 | Smart defaults and presets | Common values pre-selected where sensible. Example: break = 30min, start time = 8:00am, standard availability = Mon-Fri |
| FR11.4 | Save as draft | Partially completed forms save automatically. Users can return and finish later. |
| FR11.5 | Inline validation | Validation feedback appears inline as fields are completed — not on submit. Clear error messages with fix suggestions. |
| FR11.6 | Minimal required fields | Only fields essential to create the record are required. Everything else is optional and can be added later. |
| FR11.7 | Mobile-optimised forms | All forms work on mobile. Large touch targets (44px min). Single-column layout. Appropriate keyboard types (tel, email, date). |
| FR11.8 | Contextual help | Complex or ambiguous fields include a short help text or tooltip. Example: "WWCC number format: VIC-XXXXXXX" |

**Form UX Principles:**
1. **Prefer selection over typing** — dropdowns, toggles, chips, radio groups
2. **Progressive disclosure** — show only what is needed at each step
3. **Forgiving** — save progress, allow skipping optional sections
4. **Fast path** — common scenarios take the fewest steps

### FR10: Authentication & Tenant
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.1 | Agency registration | New agency can sign up, set up their account, add branding |
| FR10.2 | Multi-tenant architecture | Each agency's data is fully isolated |
| FR10.3 | Auth for all user types | Agency staff, nannies, and families all have separate login flows |
| FR10.4 | Invite-based access | Nannies and families are invited by the agency (not self-registration) |

---

## Non-Functional Requirements

| ID | Category | Requirement | Target |
|----|----------|-------------|--------|
| NFR-01 | Performance | Page load time | < 2s on 4G |
| NFR-02 | Security | Data isolation | Complete tenant isolation — no cross-agency data leakage |
| NFR-03 | Security | Authentication | Supabase Auth with RLS (Row Level Security) |
| NFR-04 | Accessibility | WCAG | 2.1 AA minimum |
| NFR-05 | Mobile | Responsive | Fully responsive — nanny/family portals mobile-optimised |
| NFR-06 | Compliance | AU employment law | Contract templates support Fair Work, NES, award rates |
| NFR-07 | Scalability | Concurrent agencies | Support 100+ agencies without degradation |
| NFR-08 | Data | Backup | Daily automated backups |
| NFR-09 | Availability | Uptime | 99.5% |

---

## User Flows

### Flow 1: Agency onboards a new nanny
```
Agency creates nanny contact → Nanny enters recruitment pipeline →
Interview + reference check → Nanny invited to portal →
Nanny completes onboarding (uploads docs, fills profile) →
Agency reviews + approves → Nanny status: Active
```

### Flow 2: Agency places a nanny with a family
```
Family registered with requirements → Agency filters available nannies →
Match proposed → Placement created (nanny + family + schedule + rate) →
Contract generated from template → Contract sent for signing →
Placement status: Active → Timesheets begin
```

### Flow 3: Nanny submits a timesheet
```
Nanny logs hours in portal → Submits for review →
Agency reviews + approves → Family sees FYI summary →
Timesheet data available for reporting/export
```

### Flow 4: Family experience (minimal)
```
Family invited by agency → Sets up profile →
Views placement details + nanny info →
Receives FYI timesheet summaries →
Only prompted when: contract signing, issue flagged, feedback requested
```

---

## Scope

### In Scope (MVP)
Everything in FR1–FR10 above.

### Out of Scope (MVP)
- Payroll integration (Employment Hero — post-MVP)
- Automated invoicing
- Background check API integration
- Training/certification tracking beyond document storage
- Mobile native app
- Advanced analytics/reporting
- International support

### Open Questions
- [ ] What award rates / employment classifications are most common for nannies in AU?
- [ ] Do agencies typically handle tax/super, or does that go through a payroll provider?
- [ ] What does the family onboarding look like in practice today? (Research needed)

---

## Risks

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| AU employment law complexity | High | High | Start with most common contract types; flag areas needing legal review |
| Contract template legal liability | Medium | High | Templates are starting points — agencies responsible for legal compliance. Add disclaimer |
| Family adoption friction | Medium | Medium | Keep family portal ultra-simple. Minimal required actions |
| Scope creep from agency feature requests | High | Medium | Strict MVP scope. Post-MVP backlog for additional features |
| Multi-tenant security | Low | Critical | Supabase RLS from day one. Tenant isolation tested thoroughly |

---

## Success Metrics

| Metric | Target | How Measured |
|--------|--------|--------------|
| Agency activation | Agency completes setup + adds first nanny within 7 days | Onboarding funnel tracking |
| Nanny adoption | 80% of invited nannies complete onboarding within 14 days | Onboarding completion rate |
| Timesheet submission | 90% of timesheets submitted on time | Submission tracking |
| Family satisfaction | Families rate experience 4+/5 | In-app feedback |
| Agency retention | 90% month-over-month retention | Subscription data |

---

## Dependencies

| Dependency | Type | Status | Risk |
|------------|------|--------|------|
| Supabase (DB, Auth, Storage) | External | Available | Low |
| Vercel (Hosting) | External | Available | Low |
| AU Fair Work award information | Research | Needed | Medium — affects contract templates |
| Agency user research | Research | Warm list available | Low — access confirmed |

---

## Approval

- [ ] Requirements complete and comprehensive
- [ ] Scope locked for MVP
- [ ] Open questions acceptable to proceed (can be resolved during solutioning)
- [ ] Bmac approved
- [ ] Ready to proceed to Architecture

> **Next step:** Bmac reviews PRD, then we move to Architecture design.
