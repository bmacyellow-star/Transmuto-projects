# PRD: Nanny Agency CRM

> Created: 2026-03-07
> Updated: 2026-03-09
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
5. **People are people first** — Nannies, families, and contacts live in one unified directory. Type is a property, not a silo.

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

The dashboard is the agency's operational nerve centre. It answers one question: **"What needs my attention right now?"**

#### Metric Cards

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.1 | Key metric cards | Dashboard displays: active nannies count, active families count, current placements count, pending timesheets count |
| FR1.2 | Metric card drill-down | Clicking any metric card navigates to the relevant filtered view (e.g. clicking "Pending Timesheets" → Timesheets page filtered to pending) |

#### Attention Required

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.3 | Attention panel | Dashboard surfaces items needing action, grouped by urgency. Items include: expiring documents (30/60/90 day warnings), unsigned contracts, unapproved timesheets, nannies stalled in pipeline, incomplete onboarding |
| FR1.4 | Actionable items | Each attention item links directly to the relevant record/action. One click to resolve. |
| FR1.5 | Urgency indicators | Items colour-coded: red (overdue/critical), amber (approaching deadline), blue (informational) |

#### Quick Actions

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.6 | Quick-action buttons | Dashboard provides quick actions: Add Nanny, Add Family, Create Placement, Add Contact |
| FR1.7 | Quick actions open contextual forms | Each quick action opens the relevant creation flow (wizard or modal) without leaving the dashboard context |

#### Activity Feed

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.8 | Recent activity feed | Dashboard shows a chronological feed of recent agency activity: new contacts, status changes, timesheet submissions, contract updates, placements created |
| FR1.9 | Activity attribution | Each activity entry shows which team member performed the action and when |
| FR1.10 | Activity click-through | Clicking an activity entry navigates to the relevant record |

#### Branding

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.11 | Agency branding | Agency logo displayed in header/sidebar. Agency name in page titles. Configurable in settings |

---

### FR2: People (Unified Contact Directory)
**Priority:** P0 (MVP)

**Design rationale:** Agency coordinators think in terms of people, not categories. A single "People" page replaces separate Contacts, Nannies, and Families pages. Type is a filter, not a navigation destination.

#### Directory View

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR2.1 | Unified people directory | All contacts (nannies, families, referrers, partners, prospects) displayed in one searchable, filterable list |
| FR2.2 | Type filter tabs | Tab bar at top of directory: **All** · **Nannies** · **Families** · **Other**. Tabs filter the list by contact type. Counts shown on each tab |
| FR2.3 | Search | Global search across name, email, phone. Results update as user types (debounced). Search works across all types regardless of active tab |
| FR2.4 | Status filtering | Secondary filters for status: Nannies → pipeline stage (Enquiry, Application, Interview, etc.), Families → Prospect / Active / Inactive, All → tag-based filtering |
| FR2.5 | List row content | Each row displays: avatar/initials, full name, type badge (colour-coded), status badge, phone number, last activity date |
| FR2.6 | Sort options | Sort by: name (A–Z), date added (newest first), last activity (most recent first). Default: last activity |
| FR2.7 | Bulk actions | Select multiple contacts for: bulk tagging, bulk status change, bulk export |

#### Adding People

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR2.8 | Add person | "Add" button with type selector: Nanny, Family, Referrer, Partner, Other. Selection determines which profile creation flow is launched |
| FR2.9 | Minimal creation | Creating a contact requires only: first name, last name, type. Everything else is optional and can be added later |

#### Tags & Organisation

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR2.10 | Tags | Contacts can be tagged with custom labels (e.g. "VIP", "urgent", "north-side", "temp-only"). Tags are agency-defined, not system-defined |
| FR2.11 | Tag management | Agency can create, rename, and delete tags. Tags are reusable across all contact types |
| FR2.12 | Tag filtering | People directory can be filtered by one or more tags. Tag filters combine with type tabs |

---

### FR3: Nanny Profile Page
**Priority:** P0 (MVP)

**Design rationale:** The nanny profile is where the agency spends the most time. It needs to surface compliance status (documents), current placement, and pipeline position at a glance — then allow deep dives into each area.

#### Profile Header

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.1 | Profile header | Displays: photo/avatar, full name, status badge (Enquiry / Application / Interview / Reference Check / Onboarding / Active / Inactive), phone, email |
| FR3.2 | Header quick actions | Buttons: Edit Profile, Invite to Portal (if not yet invited), Archive, Contact (phone/email shortcuts) |
| FR3.3 | Compliance summary in header | Header area shows a compliance indicator: green (all docs valid), amber (docs expiring within 60 days), red (expired or missing required docs). Clicking navigates to Documents tab |

#### Overview Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.4 | Personal details | Section showing: date of birth, address, phone, email, emergency contact |
| FR3.5 | Qualifications summary | Chips/badges showing qualifications: e.g. "Cert III Early Childhood", "First Aid", "WWCC". Each links to the relevant document |
| FR3.6 | Availability display | Visual weekly availability grid (Mon–Sun) showing available/unavailable blocks. Agency can edit. Nanny can edit via portal |
| FR3.7 | Preferences | Nanny's work preferences: preferred age groups, location radius, permanent vs casual, min/max hours |
| FR3.8 | Hourly rate | Current hourly rate and rate history |
| FR3.9 | Current placement card | If actively placed: card showing family name, schedule, start date, rate. Click through to placement detail |
| FR3.10 | Work rights | Visa status, work rights summary, expiry date if applicable |

#### Documents Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.11 | Document list | All documents displayed with: type, name, status (Verified / Pending / Expiring / Expired), expiry date, upload date |
| FR3.12 | Required document checklist | System shows which documents are required (WWCC, First Aid, Police Check) and their status. Missing required docs shown as empty slots with upload prompt |
| FR3.13 | Document expiry warnings | Documents expiring within 90 days flagged amber. Expired docs flagged red. Visual countdown (e.g. "Expires in 23 days") |
| FR3.14 | Upload document | Agency or nanny can upload documents. Supported types: PDF, JPG, PNG. Max 10MB per file |
| FR3.15 | Document verification | Agency can mark a document as "Verified" after review. Verification recorded with who verified and when |
| FR3.16 | Document download/view | Documents can be viewed inline (images) or downloaded (PDFs) |

#### Placements Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.17 | Placement history | Chronological list of all placements: family name, dates, status, rate. Current placement highlighted at top |
| FR3.18 | Placement detail link | Each placement links to the full placement record |

#### Timesheets Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.19 | Recent timesheets | List of recent timesheet entries: date, hours, placement, status (Draft / Submitted / Approved / Rejected) |
| FR3.20 | Hours summary | Summary stats: hours this week, hours this month, hours this year |
| FR3.21 | Timesheet detail link | Each entry links to the full timesheet record |

#### Onboarding Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.22 | Onboarding checklist | Checklist of onboarding tasks with completion status. Progress bar showing overall % complete |
| FR3.23 | Checklist item actions | Each item can be marked complete by agency or nanny (depending on item type). Some items link to actions (e.g. "Upload WWCC" links to document upload) |
| FR3.24 | Tab visibility | Onboarding tab only visible when nanny is in Onboarding status. Moves to a collapsed "Completed" section once all items done |

#### Activity Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.25 | Activity log | Chronological feed of all interactions: status changes, notes added, documents uploaded, timesheets submitted, placements created/changed, portal invites sent |
| FR3.26 | Add note | Agency staff can add free-text notes (e.g. "Spoke to Sarah re availability change — confirmed available Tuesdays from April") |
| FR3.27 | Activity attribution | Each entry shows who performed the action and when |

---

### FR4: Family Profile Page
**Priority:** P0 (MVP)

**Design rationale:** The family profile centres on two things: their children (the reason they need a nanny) and their care requirements (how the agency matches them). Everything else supports those core needs.

#### Profile Header

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.1 | Profile header | Displays: family display name (e.g. "The Johnsons"), status badge (Prospect / Active / Inactive), primary parent name, phone, email, address |
| FR4.2 | Header quick actions | Buttons: Edit Profile, Invite to Portal (if not yet invited), Archive, Contact (phone/email shortcuts) |

#### Overview Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.3 | Parent details | Primary and secondary parent: name, phone, email, relationship. Supports single-parent and multi-household families |
| FR4.4 | Address & location | Home address, displayed on a map pin (or suburb-level). Used for nanny matching by proximity |
| FR4.5 | Communication preferences | Preferred contact method (phone/email/SMS), preferred contact times, notification frequency |
| FR4.6 | Current placement card | If actively placed: card showing nanny name, schedule, start date, rate. Click through to placement detail |

#### Children Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.7 | Children list | Each child displayed as a card: name, date of birth (with calculated age), any special needs or notes |
| FR4.8 | Add/edit children | Agency can add, edit, and remove children. Minimum fields: name, date of birth. Optional: allergies, medical conditions, special needs, personality notes |
| FR4.9 | Age auto-calculation | Ages displayed as calculated values (e.g. "2 years 4 months") and update automatically |
| FR4.10 | Children-driven matching | Children's ages and needs are used as matching criteria when finding suitable nannies |

#### Requirements Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.11 | Care requirements | Structured capture: days needed (multi-select), hours per day, start time, end time, permanent vs casual vs temp |
| FR4.12 | Special requirements | Free-text field for specific needs: dietary requirements, language needs, pet-friendly, driving required, etc. |
| FR4.13 | Nanny preferences | Family's preferences: experience level, age range, gender preference, qualifications required |
| FR4.14 | Schedule display | Visual weekly schedule showing requested care blocks (Mon–Sun grid, similar to nanny availability) |
| FR4.15 | Requirements → Matching | "Find Matching Nannies" action from requirements tab filters available nannies by compatibility |

#### Placements Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.16 | Placement history | Chronological list of all placements: nanny name, dates, status. Current placement highlighted at top |
| FR4.17 | Placement detail link | Each placement links to the full placement record |

#### Timesheets Tab (FYI)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.18 | FYI timesheet view | Approved timesheets for the family's active placements. View only — for reference, not action |
| FR4.19 | Hours summary | Summary: hours this week, hours this month, by nanny if multiple placements |

#### Activity Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.20 | Activity log | Chronological feed of all interactions: notes, status changes, placements, contract activity |
| FR4.21 | Add note | Agency staff can add free-text notes |
| FR4.22 | Activity attribution | Each entry shows who and when |

---

### FR5: Placement Management
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.1 | Create placement | Link a nanny to a family with: start date, end date (if temp), schedule, rate, terms |
| FR5.2 | Placement overview | Agency can see all active placements, upcoming starts, recent endings |
| FR5.3 | Matching assistance | Filter available nannies by: availability, location, qualifications, preferences. Surface potential matches for a family's requirements |
| FR5.4 | Placement history | Full history of all placements for both nannies and families |
| FR5.5 | Placement status | Statuses: Proposed → Confirmed → Active → Completed / Terminated |

---

### FR6: Contract Management
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.1 | Contract templates | Agency can create and manage contract templates with merge fields |
| FR6.2 | Contract generation | Generate contract from template, auto-populated with nanny/family/placement data |
| FR6.3 | Contract tracking | Track status: Draft → Sent → Signed → Active → Expired / Terminated |
| FR6.4 | Document storage | Generated contracts stored against the relevant placement, nanny, and family records |
| FR6.5 | AU compliance fields | Templates support AU-specific fields: Fair Work info, award rates, NES entitlements, notice periods |

---

### FR7: Timesheets
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR7.1 | Nanny timesheet submission | Nanny submits: date, start time, end time, break, placement, notes |
| FR7.2 | Approval workflow | Submitted → Agency Review → Approved / Rejected (with reason) |
| FR7.3 | Family FYI view | Family can see approved timesheets for their placement. View only — no action required unless flagged |
| FR7.4 | Timesheet summary | Agency dashboard: weekly/monthly summary per nanny, per placement |
| FR7.5 | Overtime/penalty rate flags | System flags hours that may attract overtime or penalty rates under AU awards |

---

### FR8: Onboarding
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR8.1 | Onboarding checklists | Configurable checklist per nanny: documents to collect, forms to complete, training to do |
| FR8.2 | Onboarding progress | Agency can see onboarding completion % per nanny |
| FR8.3 | Nanny self-service onboarding | Nanny can complete onboarding steps from their portal (upload docs, fill forms) |

---

### FR9: Team & Multi-user
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR9.1 | Team management | Agency owner can invite team members, assign roles |
| FR9.2 | Role-based permissions | Access controlled by role (Owner, Admin, Coordinator) |
| FR9.3 | Activity attribution | All actions logged with which team member performed them |

---

### FR10: Authentication & Tenant
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.1 | Agency registration | New agency can sign up, set up their account, add branding |
| FR10.2 | Multi-tenant architecture | Each agency's data is fully isolated |
| FR10.3 | Auth for all user types | Agency staff, nannies, and families all have separate login flows |
| FR10.4 | Invite-based access | Nannies and families are invited by the agency (not self-registration) |

---

### FR11: Form UX & Data Entry
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR11.1 | Multi-step wizard pattern | All complex forms (nanny profile, family profile, placement creation) use a step-by-step wizard with progress indicator. Max 4-6 fields visible per step |
| FR11.2 | Select over input | Where a finite set of options exists, use select/dropdown/toggle/radio — not free text. Examples: qualifications, availability days, suburb, care type, certification type |
| FR11.3 | Smart defaults and presets | Common values pre-selected where sensible. Example: break = 30min, start time = 8:00am, standard availability = Mon-Fri |
| FR11.4 | Save as draft | Partially completed forms save automatically. Users can return and finish later |
| FR11.5 | Inline validation | Validation feedback appears inline as fields are completed — not on submit. Clear error messages with fix suggestions |
| FR11.6 | Minimal required fields | Only fields essential to create the record are required. Everything else is optional and can be added later |
| FR11.7 | Mobile-optimised forms | All forms work on mobile. Large touch targets (44px min). Single-column layout. Appropriate keyboard types (tel, email, date) |
| FR11.8 | Contextual help | Complex or ambiguous fields include a short help text or tooltip. Example: "WWCC number format: VIC-XXXXXXX" |

**Form UX Principles:**
1. **Prefer selection over typing** — dropdowns, toggles, chips, radio groups
2. **Progressive disclosure** — show only what is needed at each step
3. **Forgiving** — save progress, allow skipping optional sections
4. **Fast path** — common scenarios take the fewest steps

---

### FR11-A: Public Intake Forms (Agency-Branded)
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR11A.1 | Public nanny application form | Agency has a unique URL (e.g. app.nannyCRM.com/apply/little-stars) that nannies can access without logging in. Captures: personal details, qualifications, availability, preferences. Submits directly into the CRM as a new nanny contact in "Enquiry" status |
| FR11A.2 | Public family registration form | Agency has a unique URL (e.g. app.nannyCRM.com/register/little-stars) for families. Captures: parent details, children, care needs, preferences. Submits into CRM as a new family contact in "Prospect" status |
| FR11A.3 | Agency branding on public forms | Public forms display: agency logo, agency name, agency colour (optional). The form feels like the agency's own tool, not a generic platform |
| FR11A.4 | No login required | Public forms are accessible without authentication. Email verification optional (post-MVP) |
| FR11A.5 | Confirmation page | After submission, show a branded thank-you page with next steps ("We'll be in touch within 48 hours") |
| FR11A.6 | Embeddable (future) | Forms can be embedded into an agency's existing website via iframe or script tag. Out of scope for MVP but architecture should not prevent it |
| FR11A.7 | Form customisation (future) | Agencies can toggle fields on/off and reorder sections. Out of scope for MVP — all agencies get the same form structure |

**Key principle:** These forms are the agency's first impression. They must be beautiful, minimal, and fast to complete. Select over input. No unnecessary fields. Mobile-first.

---

## Agency Portal Navigation

The sidebar navigation for agency staff follows this structure:

```
🏠 Dashboard
👥 People          → Unified directory (All / Nannies / Families / Other)
📋 Placements      → Active placements, matching, history
📄 Contracts       → Templates, generated contracts, tracking
⏱️ Timesheets      → Submissions, approvals, summaries
⚙️ Settings        → Agency branding, team, templates, preferences
```

**Key change from original structure:** Contacts, Nannies, and Families pages are consolidated into a single **People** page. Clicking a person in the directory opens their full profile (Nanny Profile or Family Profile, depending on type).

**Pipeline view:** The nanny recruitment pipeline (Kanban board) is accessed via the People page when the Nannies tab is active — toggle between list view and pipeline view.

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
Agency creates nanny contact (via People → Add → Nanny) →
Nanny enters recruitment pipeline →
Interview + reference check →
Nanny invited to portal →
Nanny completes onboarding (uploads docs, fills profile) →
Agency reviews + approves → Nanny status: Active
```

### Flow 2: Agency places a nanny with a family
```
Family registered with requirements (via People → Add → Family) →
Agency opens family's Requirements tab → "Find Matching Nannies" →
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

### Flow 5: Agency coordinator daily workflow
```
Opens Dashboard → Reviews attention items (expiring docs, pending timesheets) →
Clicks through to resolve → Checks activity feed for updates →
Navigates to People → Filters nannies in pipeline → Updates statuses →
Checks placements → Reviews timesheets → Done
```

---

## Scope

### In Scope (MVP)
Everything in FR1–FR11-A above.

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

> **Next step:** Bmac reviews PRD, then we proceed to update Architecture (data model + routing changes for unified People page).