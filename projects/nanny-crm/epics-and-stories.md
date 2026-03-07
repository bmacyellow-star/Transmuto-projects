# Epics & Stories: Nanny Agency CRM

> Created: 2026-03-07
> Status: Draft
> Architecture: [Architecture](architecture.md)
> Author: Max 🚀

---

## Epic Overview

| # | Epic | Stories | Priority | Status |
|---|------|---------|----------|--------|
| E1 | Foundation & Auth | 6 | P0 | Not Started |
| E2 | Contact List / CRM | 4 | P0 | Not Started |
| E3 | Nanny Management | 6 | P0 | Not Started |
| E4 | Family Management | 4 | P0 | Not Started |
| E5 | Placement Management | 5 | P0 | Not Started |
| E6 | Contract Management | 4 | P0 | Not Started |
| E7 | Timesheets | 5 | P0 | Not Started |
| E8 | Onboarding | 3 | P0 | Not Started |
| E9 | Agency Dashboard | 3 | P0 | Not Started |
| E10 | PWA & Mobile Optimisation | 3 | P1 | Not Started |

**Total: 43 stories**

---

## E1: Foundation & Auth

_Core infrastructure: database, auth, multi-tenancy, role routing, agency branding._

#### S1.1: Project Scaffolding
**As a** developer
**I want** the Next.js project set up with all dependencies and folder structure
**So that** development can begin on a solid foundation

**Acceptance Criteria:**
- [ ] Next.js 14+ (App Router) initialised
- [ ] Tailwind CSS + shadcn/ui configured
- [ ] Supabase client libraries installed and configured
- [ ] Route groups created: (agency), (nanny), (family), (auth)
- [ ] TypeScript strict mode enabled
- [ ] ESLint + Prettier configured
- [ ] Environment variables structure (.env.local.example)

**Estimate:** S
**Dependencies:** None

---

#### S1.2: Database Schema & RLS
**As a** developer
**I want** the complete database schema deployed with RLS policies
**So that** all data is tenant-isolated from day one

**Acceptance Criteria:**
- [ ] All 12 core tables created via Supabase migrations
- [ ] RLS enabled on every table
- [ ] RLS policies enforce agency_id scoping for agency staff
- [ ] RLS policies enforce user_id scoping for nanny/family portals
- [ ] Seed data script for development
- [ ] Indexes on foreign keys and common query patterns

**Estimate:** M
**Dependencies:** S1.1

---

#### S1.3: Agency Registration
**As an** agency owner
**I want to** sign up and create my agency account
**So that** I can start using the platform

**Acceptance Criteria:**
- [ ] Registration form: name, email, password, agency name
- [ ] Creates auth user + Agency record + AgencyUser (owner role)
- [ ] Redirects to agency dashboard after registration
- [ ] Email verification sent

**Estimate:** M
**Dependencies:** S1.2

---

#### S1.4: Auth System & Role Routing
**As a** user (agency staff, nanny, or family)
**I want to** log in and be routed to the correct portal
**So that** I see the right experience for my role

**Acceptance Criteria:**
- [ ] Email/password login for agency staff
- [ ] OTP login (email) for nannies and families
- [ ] SMS OTP login option for nannies and families (Twilio via Supabase)
- [ ] Middleware detects user role and redirects to correct portal
- [ ] Protected routes — unauthenticated users redirected to login
- [ ] Session management with Supabase Auth

**Estimate:** L
**Dependencies:** S1.2, S1.3

---

#### S1.5: Team Management
**As an** agency owner
**I want to** invite staff and assign roles
**So that** my team can use the platform

**Acceptance Criteria:**
- [ ] Invite team member by email (sends invite via Resend)
- [ ] Assign role: admin or coordinator
- [ ] Invited user creates account and is linked to agency
- [ ] Owner can change roles or deactivate team members
- [ ] Team members list with role badges

**Estimate:** M
**Dependencies:** S1.4

---

#### S1.6: Agency Branding & Settings
**As an** agency owner
**I want to** add my logo and configure basic settings
**So that** the platform feels like my own tool

**Acceptance Criteria:**
- [ ] Upload agency logo (stored in Supabase Storage)
- [ ] Logo displayed in header across all portals
- [ ] Agency name in page titles and family/nanny-facing touchpoints
- [ ] Settings page: agency details, branding, notification preferences

**Estimate:** S
**Dependencies:** S1.3

---

## E2: Contact List / CRM

_Centralised contact directory — the backbone of the agency's relationships._

#### S2.1: Contact CRUD & Directory
**As an** agency user
**I want** a centralised contact directory
**So that** I can find and manage all agency relationships in one place

**Acceptance Criteria:**
- [ ] Create contact: name, type, phone, email, address, tags, notes
- [ ] Contact types: Nanny, Family, Referrer, Partner, Other
- [ ] List view with search (name, email, phone)
- [ ] Filter by type, tags, status
- [ ] Edit and archive contacts
- [ ] Pagination / infinite scroll

**Estimate:** M
**Dependencies:** S1.2, S1.4

---

#### S2.2: Contact Profiles & Detail View
**As an** agency user
**I want** a detailed contact profile page
**So that** I can see everything about a contact in one place

**Acceptance Criteria:**
- [ ] Contact detail page with all fields
- [ ] Linked records shown: if nanny → nanny profile; if family → family profile
- [ ] Editable inline or via edit mode
- [ ] Address displayed (with map link if possible)

**Estimate:** S
**Dependencies:** S2.1

---

#### S2.3: Tags & Categorisation
**As an** agency user
**I want to** tag and categorise contacts
**So that** I can segment and filter my contact list

**Acceptance Criteria:**
- [ ] Add/remove tags on contacts (free-form + suggested)
- [ ] Filter contact list by one or more tags
- [ ] Bulk tag operations (select multiple → add tag)
- [ ] Tag management (view all tags, merge, delete)

**Estimate:** S
**Dependencies:** S2.1

---

#### S2.4: Activity Log
**As an** agency user
**I want** an activity history on each contact
**So that** I can see all interactions and changes over time

**Acceptance Criteria:**
- [ ] Automatic logging: status changes, profile updates, placement changes, documents uploaded
- [ ] Manual notes: add timestamped notes to any contact
- [ ] Activity displayed chronologically on contact profile
- [ ] Activity attributed to the team member who performed it

**Estimate:** M
**Dependencies:** S2.2

---

## E3: Nanny Management

_Nanny profiles, recruitment pipeline, documents, availability, and self-service portal._

#### S3.1: Nanny Profiles
**As an** agency user
**I want** comprehensive nanny profiles
**So that** I have all information needed for placements and compliance

**Acceptance Criteria:**
- [ ] Create nanny (linked to Contact record)
- [ ] Fields: qualifications, certifications, availability, preferences, hourly rate, work rights, emergency contact
- [ ] Profile page with all info + linked placements, documents, timesheets
- [ ] Edit nanny details

**Estimate:** M
**Dependencies:** S2.1

---

#### S3.2: Recruitment Pipeline
**As an** agency user
**I want** a visual recruitment pipeline
**So that** I can track nannies through the hiring process

**Acceptance Criteria:**
- [ ] Kanban board view: Enquiry → Application → Interview → Reference Check → Onboarding → Active
- [ ] Drag-and-drop to move nannies between stages
- [ ] Status change logged in activity log
- [ ] Filter pipeline by date, source, stage
- [ ] Count per stage visible

**Estimate:** M
**Dependencies:** S3.1

---

#### S3.3: Document Management
**As an** agency user
**I want to** track nanny documents and certifications
**So that** I can ensure compliance and catch expiring documents

**Acceptance Criteria:**
- [ ] Upload documents: WWCC, First Aid, police check, visa, qualifications, other
- [ ] Document metadata: type, name, expiry date, status (pending/verified/expired)
- [ ] Expiry warnings: flagged at 90/60/30 days before expiry
- [ ] Document list on nanny profile
- [ ] Agency-wide view of expiring documents (notification centre)

**Estimate:** M
**Dependencies:** S3.1

---

#### S3.4: Availability Management
**As a** nanny
**I want to** set my availability
**So that** the agency can find me when families need care

**Acceptance Criteria:**
- [ ] Nanny sets weekly availability (day + time blocks)
- [ ] Agency can view availability per nanny
- [ ] Agency can view availability across all nannies (who's free Tuesday afternoon?)
- [ ] Availability factored into placement matching

**Estimate:** M
**Dependencies:** S3.1

---

#### S3.5: Nanny Portal (Self-Service)
**As a** nanny
**I want** my own portal to manage my profile and work
**So that** I can handle my admin without calling the agency

**Acceptance Criteria:**
- [ ] Login via OTP (email or SMS)
- [ ] View and edit own profile
- [ ] Upload documents
- [ ] View current and past placements
- [ ] View contract details
- [ ] Submit timesheets (see E7)
- [ ] Mobile-optimised layout

**Estimate:** L
**Dependencies:** S1.4, S3.1

---

#### S3.6: Nanny Invite Flow
**As an** agency user
**I want to** invite a nanny to the portal
**So that** they can self-serve their profile, docs, and timesheets

**Acceptance Criteria:**
- [ ] Invite button on nanny profile
- [ ] Sends OTP invite email via Resend
- [ ] Nanny clicks link → sets up account → lands in nanny portal
- [ ] Nanny user_id linked to Nanny record
- [ ] Re-send invite option

**Estimate:** S
**Dependencies:** S3.5, S1.4

---

## E4: Family Management

_Family profiles, requirements, lightweight portal, invite flow._

#### S4.1: Family Profiles
**As an** agency user
**I want** family profiles with care requirements
**So that** I can match them with the right nanny

**Acceptance Criteria:**
- [ ] Create family (linked to Contact record)
- [ ] Fields: parent details, children (name, DOB, needs), address, care requirements, schedule preferences, location
- [ ] Profile page with linked placements, contracts
- [ ] Edit family details

**Estimate:** M
**Dependencies:** S2.1

---

#### S4.2: Requirements Capture
**As an** agency user
**I want** structured capture of family requirements
**So that** matching is efficient and accurate

**Acceptance Criteria:**
- [ ] Structured form: hours needed, days, special requirements, children's needs, location preferences
- [ ] Requirements displayed on family profile
- [ ] Requirements used in placement matching filters

**Estimate:** S
**Dependencies:** S4.1

---

#### S4.3: Family Portal (Lightweight)
**As a** family member
**I want** a simple portal to see my placement details
**So that** I'm informed without having to call the agency

**Acceptance Criteria:**
- [ ] Login via OTP (email or SMS)
- [ ] View current nanny details and placement info
- [ ] View FYI timesheet summaries (approved timesheets, view only)
- [ ] Notification when action is needed (contract signing, issue flagged)
- [ ] Mobile-first, minimal UI — single column, large touch targets
- [ ] No actions required unless explicitly flagged by agency

**Estimate:** M
**Dependencies:** S1.4, S4.1

---

#### S4.4: Family Invite Flow
**As an** agency user
**I want to** invite a family to the portal
**So that** they can view their placement details

**Acceptance Criteria:**
- [ ] Invite button on family profile
- [ ] Sends OTP invite email via Resend
- [ ] Family clicks link → sets up account → lands in family portal
- [ ] Family user_id linked to Family record
- [ ] Re-send invite option

**Estimate:** S
**Dependencies:** S4.3, S1.4

---

## E5: Placement Management

_Matching nannies to families, managing placements end-to-end._

#### S5.1: Create & Manage Placements
**As an** agency user
**I want to** create and manage placements
**So that** I can formally link nannies with families

**Acceptance Criteria:**
- [ ] Create placement: select nanny + family, set start date, end date (optional), schedule, rate, terms
- [ ] Placement statuses: Proposed → Confirmed → Active → Completed / Terminated
- [ ] Edit placement details
- [ ] View placement history per nanny and per family

**Estimate:** M
**Dependencies:** S3.1, S4.1

---

#### S5.2: Placement Overview
**As an** agency user
**I want** an overview of all placements
**So that** I can see the state of my business at a glance

**Acceptance Criteria:**
- [ ] List view of all placements with filters (status, nanny, family, date range)
- [ ] Summary: active count, upcoming starts, recent endings
- [ ] Click through to placement detail

**Estimate:** S
**Dependencies:** S5.1

---

#### S5.3: Matching Assistance
**As an** agency user
**I want** help finding the right nanny for a family
**So that** placements are well-matched

**Acceptance Criteria:**
- [ ] From a family profile, click "Find Nannies"
- [ ] Filter available nannies by: availability (matching family schedule), location (proximity), qualifications
- [ ] Show match indicators (availability overlap %, distance)
- [ ] Quick-create placement from match result

**Estimate:** L
**Dependencies:** S3.4, S4.2, S5.1

---

#### S5.4: Placement Detail View
**As an** agency user
**I want** a comprehensive placement detail page
**So that** I can see everything about a placement in one place

**Acceptance Criteria:**
- [ ] Shows: nanny info, family info, schedule, rate, status, contract, timesheets
- [ ] Links to nanny profile, family profile, contract, timesheets
- [ ] Status change actions (confirm, activate, complete, terminate)
- [ ] Activity log for the placement

**Estimate:** M
**Dependencies:** S5.1

---

#### S5.5: Placement Notifications
**As an** agency user
**I want** notifications about placement changes
**So that** nothing falls through the cracks

**Acceptance Criteria:**
- [ ] Notification when placement is approaching start date (7 days, 1 day)
- [ ] Notification when placement is approaching end date
- [ ] Notification when placement status changes
- [ ] Surfaced in agency dashboard notification centre

**Estimate:** S
**Dependencies:** S5.1, S9.1

---

## E6: Contract Management

_Template-based contract generation with AU compliance._

#### S6.1: Contract Templates
**As an** agency owner
**I want** to create and manage contract templates
**So that** I can generate consistent contracts quickly

**Acceptance Criteria:**
- [ ] Create template with rich text editor
- [ ] Merge fields: {{nanny.name}}, {{family.name}}, {{placement.rate}}, {{placement.schedule}}, etc.
- [ ] Template categories: employment, placement, casual, permanent
- [ ] Default template per category
- [ ] Edit and duplicate templates
- [ ] AU compliance fields available: Fair Work info, award rates, NES entitlements, notice periods

**Estimate:** L
**Dependencies:** S1.2

---

#### S6.2: Contract Generation
**As an** agency user
**I want to** generate a contract from a template
**So that** contracts are auto-populated with the right data

**Acceptance Criteria:**
- [ ] Select template → auto-populate with nanny/family/placement data
- [ ] Preview generated contract before finalising
- [ ] Edit generated content if needed
- [ ] Save as draft
- [ ] Generate PDF version

**Estimate:** L
**Dependencies:** S6.1, S5.1

---

#### S6.3: Contract Tracking
**As an** agency user
**I want to** track contract status
**So that** I know which contracts are signed and which need attention

**Acceptance Criteria:**
- [ ] Contract statuses: Draft → Sent → Signed → Active → Expired / Terminated
- [ ] Send contract (email with PDF attachment or link)
- [ ] Mark as signed (manual for MVP — e-signatures post-MVP)
- [ ] Expiry tracking with notifications
- [ ] Contract linked to placement, nanny, and family records

**Estimate:** M
**Dependencies:** S6.2

---

#### S6.4: Contract Storage
**As an** agency user
**I want** contracts stored and accessible
**So that** I can find any contract when needed

**Acceptance Criteria:**
- [ ] Generated PDF stored in Supabase Storage
- [ ] Contract accessible from: placement detail, nanny profile, family profile
- [ ] Download PDF
- [ ] Contract list view with filters (status, nanny, family, date)

**Estimate:** S
**Dependencies:** S6.2

---

## E7: Timesheets

_Nanny submission, agency approval, family FYI view._

#### S7.1: Timesheet Submission
**As a** nanny
**I want to** submit my timesheets digitally
**So that** I don't have to use paper or email

**Acceptance Criteria:**
- [ ] Submit timesheet: date, start time, end time, break (minutes), placement (pre-selected if only one active), notes
- [ ] Save as draft before submitting
- [ ] View submitted timesheets and their status
- [ ] Edit draft timesheets (not submitted/approved ones)
- [ ] Mobile-optimised quick-entry form

**Estimate:** M
**Dependencies:** S3.5, S5.1

---

#### S7.2: Approval Workflow
**As an** agency user
**I want to** review and approve timesheets
**So that** hours are verified before any downstream processing

**Acceptance Criteria:**
- [ ] List of pending timesheets for review
- [ ] Approve or reject (with reason)
- [ ] Bulk approve option
- [ ] Nanny notified of approval/rejection
- [ ] Approved timesheets become read-only

**Estimate:** M
**Dependencies:** S7.1

---

#### S7.3: Family FYI View
**As a** family member
**I want to** see timesheet summaries
**So that** I'm informed about hours without having to do anything

**Acceptance Criteria:**
- [ ] Family portal shows approved timesheets for their placement
- [ ] Summary view: weekly total hours, dates worked
- [ ] View only — no approval action needed
- [ ] Only approved timesheets visible (not draft/pending)

**Estimate:** S
**Dependencies:** S7.2, S4.3

---

#### S7.4: Timesheet Summary & Reporting
**As an** agency user
**I want** timesheet summaries
**So that** I can see hours worked across my agency

**Acceptance Criteria:**
- [ ] Weekly/monthly summary per nanny
- [ ] Weekly/monthly summary per placement
- [ ] Export to CSV
- [ ] Dashboard widget showing pending/approved this week

**Estimate:** M
**Dependencies:** S7.2

---

#### S7.5: Award Rate Flags
**As an** agency user
**I want** the system to flag potential overtime or penalty rates
**So that** I'm aware of cost implications

**Acceptance Criteria:**
- [ ] Flag timesheets where hours exceed standard weekly threshold (38hrs)
- [ ] Flag weekend or public holiday hours
- [ ] Visual indicator on timesheet review
- [ ] Note: informational only for MVP — no rate calculation

**Estimate:** S
**Dependencies:** S7.2

---

## E8: Onboarding

_Checklists and self-service onboarding for new nannies._

#### S8.1: Onboarding Checklists
**As an** agency user
**I want** configurable onboarding checklists
**So that** every nanny completes all required steps

**Acceptance Criteria:**
- [ ] Create checklist template (agency-wide default)
- [ ] Assign checklist to nanny
- [ ] Checklist items: title, description, required (yes/no), type (document upload, form, manual tick)
- [ ] Track completion per item
- [ ] Progress percentage displayed

**Estimate:** M
**Dependencies:** S3.1

---

#### S8.2: Nanny Self-Service Onboarding
**As a** nanny
**I want to** complete my onboarding from my portal
**So that** I can get started without back-and-forth emails

**Acceptance Criteria:**
- [ ] Nanny sees their checklist in portal
- [ ] Can upload documents against checklist items
- [ ] Can fill in profile fields prompted by checklist
- [ ] Progress bar showing completion
- [ ] Agency notified when items are completed

**Estimate:** M
**Dependencies:** S8.1, S3.5

---

#### S8.3: Onboarding Overview (Agency)
**As an** agency user
**I want** an overview of all nannies in onboarding
**So that** I can see who needs follow-up

**Acceptance Criteria:**
- [ ] List of nannies currently onboarding with progress %
- [ ] Click through to individual checklist
- [ ] Filter by completion status
- [ ] Flag nannies with stalled onboarding (no progress in X days)

**Estimate:** S
**Dependencies:** S8.1

---

## E9: Agency Dashboard

_The home screen — overview of the entire agency operation._

#### S9.1: Dashboard Overview
**As an** agency user
**I want** a dashboard showing key metrics
**So that** I can see the state of my business at a glance

**Acceptance Criteria:**
- [ ] Metrics: active nannies, active families, current placements, pending timesheets
- [ ] Recent activity feed
- [ ] Quick-action buttons: new nanny, new family, new placement

**Estimate:** M
**Dependencies:** S3.1, S4.1, S5.1, S7.1

---

#### S9.2: Notification Centre
**As an** agency user
**I want** a notification centre for pending items
**So that** nothing falls through the cracks

**Acceptance Criteria:**
- [ ] Pending items: unsigned contracts, unapproved timesheets, expiring documents, stalled onboarding
- [ ] Displayed as notification badges + expandable list
- [ ] Click through to relevant item
- [ ] Mark as read/dismissed

**Estimate:** M
**Dependencies:** S3.3, S6.3, S7.2, S8.1

---

#### S9.3: Agency-wide Search
**As an** agency user
**I want** to search across all records
**So that** I can find anything quickly

**Acceptance Criteria:**
- [ ] Global search bar in header
- [ ] Searches across: contacts, nannies, families, placements
- [ ] Results grouped by type
- [ ] Click through to record

**Estimate:** M
**Dependencies:** S2.1, S3.1, S4.1, S5.1

---

## E10: PWA & Mobile Optimisation

_Progressive Web App setup and mobile polish._

#### S10.1: PWA Configuration
**As a** nanny or family member
**I want to** install the app on my phone
**So that** it feels like a native app

**Acceptance Criteria:**
- [ ] Web app manifest configured (name, icons, theme colour, display: standalone)
- [ ] Service worker for basic offline caching (app shell, recent pages)
- [ ] "Add to Home Screen" prompt on mobile browsers
- [ ] Splash screen on launch

**Estimate:** S
**Dependencies:** S1.1

---

#### S10.2: Mobile UX Polish (Nanny Portal)
**As a** nanny
**I want** the portal to feel great on my phone
**So that** submitting timesheets and checking placements is quick

**Acceptance Criteria:**
- [ ] All nanny portal pages pass mobile usability audit
- [ ] Timesheet entry optimised for thumb input (large buttons, minimal typing)
- [ ] Touch-friendly navigation (bottom nav or hamburger)
- [ ] Fast load on 4G (< 2s)

**Estimate:** M
**Dependencies:** S3.5, S7.1

---

#### S10.3: Mobile UX Polish (Family Portal)
**As a** family member
**I want** the portal to be ultra-simple on my phone
**So that** I can check things in seconds

**Acceptance Criteria:**
- [ ] Single-column layout, large text, minimal UI
- [ ] Placement info visible immediately on login
- [ ] Timesheet summary scannable in < 5 seconds
- [ ] No unnecessary navigation — everything on one or two screens

**Estimate:** S
**Dependencies:** S4.3

---

## Dependency Map

```
S1.1 ──→ S1.2 ──→ S1.3 ──→ S1.4 ──→ S1.5
                    │         │        S1.6
                    │         │
                    ▼         ▼
                  S2.1 ──→ S2.2 ──→ S2.3
                    │       │        S2.4
                    │       │
              ┌─────┼───────┘
              ▼     ▼
            S3.1  S4.1 ──→ S4.2
              │     │        S4.3 ──→ S4.4
              │     │
              ├──→ S5.1 ──→ S5.2, S5.3, S5.4, S5.5
              │     │
              │     ├──→ S6.1 ──→ S6.2 ──→ S6.3 ──→ S6.4
              │     │
              │     └──→ S7.1 ──→ S7.2 ──→ S7.3, S7.4, S7.5
              │
              ├──→ S3.2, S3.3, S3.4
              ├──→ S3.5 ──→ S3.6
              │
              └──→ S8.1 ──→ S8.2, S8.3

S9.1, S9.2, S9.3 depend on most above epics (built last)
S10.1 can start early (depends only on S1.1)
S10.2, S10.3 are polish passes (built last)
```

---

## Implementation Waves

### Wave 1: Foundation (parallel)
- **S1.1** Project scaffolding
- **S10.1** PWA configuration (can start alongside)

### Wave 2: Data Layer (sequential on S1.1)
- **S1.2** Database schema & RLS

### Wave 3: Auth & Core (parallel, depends on S1.2)
- **S1.3** Agency registration
- **S6.1** Contract templates (no auth dependency, just DB)

### Wave 4: Auth Complete + Contacts (parallel, depends on S1.3)
- **S1.4** Auth system & role routing
- **S1.6** Agency branding & settings
- **S2.1** Contact CRUD & directory

### Wave 5: Profiles (parallel, depends on S1.4 + S2.1)
- **S1.5** Team management
- **S2.2** Contact profiles
- **S2.3** Tags & categorisation
- **S3.1** Nanny profiles
- **S4.1** Family profiles

### Wave 6: Features (parallel, depends on Wave 5)
- **S2.4** Activity log
- **S3.2** Recruitment pipeline
- **S3.3** Document management
- **S3.4** Availability management
- **S4.2** Requirements capture
- **S5.1** Create & manage placements

### Wave 7: Portals + Advanced (parallel, depends on Wave 6)
- **S3.5** Nanny portal
- **S4.3** Family portal
- **S5.2** Placement overview
- **S5.3** Matching assistance
- **S5.4** Placement detail view
- **S5.5** Placement notifications
- **S6.2** Contract generation
- **S7.1** Timesheet submission
- **S8.1** Onboarding checklists

### Wave 8: Workflows & Integration (depends on Wave 7)
- **S3.6** Nanny invite flow
- **S4.4** Family invite flow
- **S6.3** Contract tracking
- **S6.4** Contract storage
- **S7.2** Approval workflow
- **S8.2** Nanny self-service onboarding
- **S8.3** Onboarding overview

### Wave 9: Dashboard & Polish (depends on most above)
- **S7.3** Family FYI view
- **S7.4** Timesheet summary & reporting
- **S7.5** Award rate flags
- **S9.1** Dashboard overview
- **S9.2** Notification centre
- **S9.3** Agency-wide search
- **S10.2** Mobile UX polish (nanny)
- **S10.3** Mobile UX polish (family)

---

## Approval

- [ ] Stories cover all PRD requirements
- [ ] Acceptance criteria are testable
- [ ] Dependencies mapped
- [ ] Waves are logical and parallelisable
- [ ] Bmac approved
- [ ] Ready to proceed to Discuss → Build

> **Next step:** Discuss phase — capture implementation preferences before building.
