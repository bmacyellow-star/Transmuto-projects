# PRD: Nanny Agency CRM

> Created: 2026-03-07
> Updated: 2026-03-11
> Status: Draft
> Brief: [Product Brief](brief.md)
> Author: Max 🚀 (PM lens)

---

## Overview

### Vision
A single platform for nanny agencies to manage their entire operation — recruitment, contracts, placements, timesheets, and communication — while giving families a seamless, hands-off experience.

### Background
Nanny agencies in Australia run on fragmented tools. No platform handles the full lifecycle while keeping the family experience effortless. This product fills that gap: powerful for the agency, invisible for the family.

### Design Principles
1. **Agency-powerful, family-effortless** — The agency gets depth. The family gets simplicity.
2. **Data captured once, used everywhere** — Profile data flows into contracts, timesheets, placements automatically.
3. **Mobile-first for nannies and families** — They live on their phones.
4. **Agency-branded** — The platform feels like the agency's own tool.
5. **Nannies and families are distinct** — Separate directories for nannies and families. Each has its own page, profile structure, and workflow.
6. **Actions drive progress** — Listing stages advance when real work is completed, not when someone drags a card.


### Terminology

| Term | Definition |
|------|-----------|
| **Nanny** | A childcare professional managed by the agency. Always "nanny", never "carer" or "worker" |
| **Family** | A household receiving childcare services. Referred to by display name (e.g. "The Johnsons") |
| **Placement** | An active arrangement connecting a nanny to a family with schedule, rate, and terms |
| **Listing** | A nanny's position in the recruitment funnel. Stages: Enquiry → Application → Interview → Reference Check → Onboarding → Active |
| **Listings** | The recruitment funnel page (kanban board). Tracks nanny recruitment journey, not the Nannies directory |
| **Portal** | The self-service interface for nannies and families (separate from the agency admin interface) |
| **Contact** | Generic reference to a nanny or family record when the distinction doesn't matter (e.g. in messaging) |
| **Compliance** | Whether a nanny's required documents (WWCC, First Aid, Police Check) are current and verified |

---

## User Personas

### Sarah — Agency Owner
**Context:** Runs "Little Stars Nannies" in Melbourne with 3 coordinators and 45 active nannies. Currently manages everything across Excel, Gmail, and WhatsApp groups. Loses 10+ hours/week to admin.
**Primary goals:** Visibility across all operations from one place. Reduce admin overhead. Professional brand image when onboarding new families.
**Pain points:** Can't see which nannies have expired documents until a family complains. Contracts are Word docs emailed back and forth. No single source of truth for who's placed where.
**Uses:** Dashboard, settings, branding, team management. Checks in 2–3x daily.

### Jess — Agency Coordinator
**Context:** Works at Little Stars full-time. Manages 15 nanny relationships and 12 family accounts. Spends most of her day in the CRM.
**Primary goals:** Know exactly what needs doing today. Move nannies through recruitment efficiently. Keep families happy with minimal back-and-forth.
**Pain points:** Spends 30 min/day chasing document renewals manually. Interview notes scattered across notebooks and emails. Can't easily see which nannies are available for a new family.
**Uses:** Listings, nanny/family profiles, placements, timesheets, communication. Power user — 6+ hours/day.

### Emma — Nanny
**Context:** Casual nanny, 24, works with 2 families through Little Stars. Primarily uses her phone. Not particularly tech-savvy.
**Primary goals:** Log hours quickly. Keep her documents up to date without nagging. See her upcoming schedule.
**Pain points:** Currently texts timesheets to her coordinator and hopes they get processed. Doesn't know when her First Aid cert expires until the agency calls.
**Uses:** Portal (mobile): timesheets, documents, profile, placement details. Logs in 2–3x per week for timesheets.

### Rachel & Tom — Family
**Context:** Parents of 2 kids (ages 1 and 3) in inner Melbourne. Both work full-time. Engaged Little Stars for a permanent nanny.
**Primary goals:** Know who's looking after their kids and when. Not be bothered with admin. Trust the agency is handling compliance.
**Pain points:** Previous agency sent contracts via email attachments and it was confusing. Want to see their nanny's qualifications for peace of mind.
**Uses:** Portal (mobile/desktop): view placement, see nanny profile, FYI timesheets. Log in rarely — only when prompted.

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
| FR1.3 | Attention panel | Dashboard surfaces items needing action in three urgency groups displayed top-to-bottom: **Critical** (red — overdue docs, expired WWCC/First Aid/Police Check), **Urgent** (amber — docs expiring within 30 days, unsigned contracts >7 days, unapproved timesheets >3 days), **Attention** (blue — docs expiring 31–90 days, nannies in same listing stage >14 days, onboarding <50% complete after 7 days). Maximum 20 items shown per group with "View all" link if more exist |
| FR1.4 | Actionable items | Each attention item links directly to the relevant record/action. One click to resolve |
| FR1.5 | Urgency indicators | Items colour-coded: red (overdue/critical), amber (approaching deadline), blue (informational) |

#### Quick Actions

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.6 | Quick-action buttons | Dashboard provides quick actions: Add Nanny, Add Family, Create Placement, New Message |
| FR1.7 | Quick actions open contextual forms | Each quick action opens the relevant creation flow (wizard or modal) without leaving the dashboard context |

#### Activity Feed

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.8 | Recent activity feed | Dashboard shows the 25 most recent agency activities in reverse chronological order. Activity types: new nannies/families added, status changes, timesheet submissions, contract status changes, placements created/updated, messages received. Each entry shows: icon by type, description, actor name, relative timestamp ("2 hours ago"). Feed auto-refreshes every 60 seconds |
| FR1.9 | Activity attribution | Each activity entry shows which team member performed the action and when |
| FR1.10 | Activity click-through | Clicking an activity entry navigates to the relevant record |

#### Branding

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.11 | Agency branding | Agency logo displayed in header/sidebar. Agency name in page titles. Configurable in settings |

#### Global Search

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.12 | Global search (⌘K) | Keyboard shortcut (⌘K / Ctrl+K) opens a global search overlay accessible from any page. Searches across: nannies, families, placements, contracts. Results grouped by type with click-through to the relevant record |
| FR1.13 | Search in header | Persistent search icon in the app header that opens the same global search overlay |

---

### FR2: Families Directory
**Priority:** P0 (MVP)

**Design rationale:** Families have their own dedicated directory page. The agency manages family profiles, children, care requirements, and placement history from a single location.

#### Directory View

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR2.1 | Families directory | All families displayed in a searchable, filterable list showing family display name, status, children count, suburb, and last activity |
| FR2.2 | Status filter tabs | Tab bar at top: **All** · **Active** · **Prospect** · **Inactive**. Tabs filter the list. Counts shown on each tab |
| FR2.3 | Search | Search across: family display name, primary parent first/last name, secondary parent first/last name, email, phone. Debounce: 300ms after last keystroke. Results update in-place (no page reload). Minimum query length: 2 characters. Matching text highlighted in results. "X" button to clear search and restore full list |
| FR2.4 | Family display name | Auto-generated from primary parent surname as "The [Surname]s" (e.g. "The Johnsons"). Can be manually overridden for blended families or non-standard names (e.g. "Smith-Jones Family") |
| FR2.5 | Sort options | Sort by: name (A–Z), date added (newest first), last activity (most recent first). Default: last activity |
| FR2.6 | Bulk actions | Select multiple families for: bulk tagging, bulk status change, bulk export, bulk message (see FR10) |

#### Adding Families

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR2.7 | Add family | "Add Family" button launches creation flow. Requires: primary parent first name, last name. Everything else is optional and can be added later |

#### Tags & Organisation

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR2.8 | Tags | Families can be tagged with custom labels (e.g. "VIP", "north-side", "special-needs"). Tags are agency-defined |
| FR2.9 | Tag filtering | Directory can be filtered by one or more tags. Tag filters combine with status tabs |

---

### FR3: Nannies Directory
**Priority:** P0 (MVP)

**Design rationale:** Nannies have their own dedicated directory page. The agency manages nanny profiles, compliance status, availability, and placement history from a single location. Compliance indicators are prominent — the agency needs to see at a glance who is compliant and who needs attention.

#### Directory View

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.1 | Nannies directory | All nannies displayed in a searchable, filterable list showing name, status, compliance indicator, suburb, and last activity |
| FR3.2 | Status filter tabs | Tab bar at top: **All** · **Active** · **Onboarding** · **Prospect**. Tabs filter the list. Counts shown on each tab |
| FR3.3 | Search | Search across nanny name, email, phone. Results update as user types (debounced) |
| FR3.4 | Compliance indicator | Each nanny row shows a compliance dot: green (all docs valid), amber (docs expiring within 60 days), red (expired or missing required docs) |
| FR3.5 | Sort options | Sort by: name (A–Z), date added (newest first), last activity (most recent first), compliance status. Default: last activity |
| FR3.6 | Bulk actions | Select multiple nannies for: bulk tagging, bulk status change, bulk export, bulk message (see FR10) |

#### Adding Nannies

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.7 | Add nanny | "Add Nanny" button launches creation flow. Requires: first name, last name. Everything else is optional and can be added later. New nanny enters Listings at "Enquiry" stage |

#### Tags & Organisation

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.8 | Tags | Nannies can be tagged with custom labels (e.g. "temp-only", "north-side", "infant-specialist"). Tags are agency-defined |
| FR3.9 | Tag filtering | Directory can be filtered by one or more tags. Tag filters combine with status tabs |

---

### FR4: Nanny Profile Page
**Priority:** P0 (MVP)

**Design rationale:** The nanny profile is where the agency spends the most time. It needs to surface compliance status (documents), current placement, and listing stage position at a glance — then allow deep dives into each area.

#### Profile Header

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.1 | Profile header | Displays: photo/avatar, full name, status badge (Enquiry / Application / Interview / Reference Check / Onboarding / Active / Inactive), phone, email |
| FR4.2 | Header quick actions | Buttons: Edit Profile, Invite to Portal (if not yet invited), Send Message (see FR10), Archive, Contact (phone/email shortcuts) |
| FR4.3 | Compliance summary in header | Header area shows a compliance indicator: green (all docs valid), amber (docs expiring within 60 days), red (expired or missing required docs). Clicking navigates to Documents tab |

#### Overview Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.4 | Personal details | Section showing: date of birth, address, phone, email, emergency contact |
| FR4.5 | Qualifications summary | Chips/badges showing qualifications: e.g. "Cert III Early Childhood", "First Aid", "WWCC". Each links to the relevant document |
| FR4.6 | Availability display | Visual weekly availability grid (Mon–Sun) showing available/unavailable blocks. Agency can edit. Nanny can edit via portal |
| FR4.7 | Preferences | Nanny's work preferences: preferred age groups, location radius, permanent vs casual, min/max hours |
| FR4.8 | Hourly rate | Current hourly rate and rate history |
| FR4.9 | Current placement card | If actively placed: card showing family name, schedule, start date, rate. Click through to placement detail |
| FR4.10 | Work rights | Visa status, work rights summary, expiry date if applicable |

#### Documents Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.11 | Document list | All documents displayed with: type, name, status (Verified / Pending / Expiring / Expired), expiry date, upload date |
| FR4.12 | Required document checklist | System shows which documents are required (WWCC, First Aid, Police Check) and their status. Missing required docs shown as empty slots with upload prompt |
| FR4.13 | Document expiry warnings | Documents expiring within 90 days flagged amber. Expired docs flagged red. Visual countdown (e.g. "Expires in 23 days") |
| FR4.14 | Upload document | Agency or nanny can upload documents. Supported types: PDF, JPG, PNG. Max 10MB per file |
| FR4.15 | Document verification | Agency can mark a document as "Verified" after review. Verification recorded with who verified and when |
| FR4.16 | Document download/view | Documents can be viewed inline (images) or downloaded (PDFs) |

#### Placements Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.17 | Placement history | Chronological list of all placements: family name, dates, status, rate. Current placement highlighted at top |
| FR4.18 | Placement detail link | Each placement links to the full placement detail page (see FR6) |

#### Timesheets Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.19 | Recent timesheets | List of recent timesheet entries: date, hours, placement, status (Draft / Submitted / Approved / Rejected) |
| FR4.20 | Hours summary | Summary stats: hours this week, hours this month, hours this year |
| FR4.21 | Timesheet detail link | Each entry links to the full timesheet record |

#### Onboarding Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.22 | Onboarding checklist | Checklist of onboarding tasks with completion status. Progress bar showing overall % complete |
| FR4.23 | Checklist item actions | Each item can be marked complete by agency or nanny (depending on item type). Some items link to actions (e.g. "Upload WWCC" links to document upload) |
| FR4.24 | Tab visibility | Onboarding tab only visible when nanny is in Onboarding status. Moves to a collapsed "Completed" section once all items done |

#### Activity Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.25 | Activity log | Chronological feed of all interactions: status changes, notes added, documents uploaded, timesheets submitted, placements created/changed, portal invites sent, messages sent/received |
| FR4.26 | Add note | Agency staff can add free-text notes (e.g. "Spoke to Sarah re availability change — confirmed available Tuesdays from April") |
| FR4.27 | Activity attribution | Each entry shows who performed the action and when |

---

### FR5: Family Profile Page
**Priority:** P0 (MVP)

**Design rationale:** The family profile centres on two things: their children (the reason they need a nanny) and their care requirements (how the agency matches them). Everything else supports those core needs.

#### Profile Header

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.1 | Profile header | Displays: family display name, status badge (Prospect / Active / Inactive), primary parent name, phone, email, address |
| FR5.1a | Family display name | Auto-generated from primary parent surname as "The [Surname]s" (e.g. "The Johnsons"). Can be manually overridden for blended families or non-standard names (e.g. "Smith-Jones Family") |
| FR5.2 | Header quick actions | Buttons: Edit Profile, Invite to Portal (if not yet invited), Send Message (see FR10), Archive, Contact (phone/email shortcuts) |

#### Overview Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.3 | Parent details | Primary and secondary parent: name, phone, email, relationship. Supports single-parent and multi-household families |
| FR5.4 | Address & location | Home address, displayed on a map pin (or suburb-level). Used for nanny matching by proximity |
| FR5.5 | Communication preferences | Preferred contact method (phone/email/SMS), preferred contact times, notification frequency |
| FR5.6 | Current placement card | If actively placed: card showing nanny name, schedule, start date, rate. Click through to placement detail |

#### Children Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.7 | Children list | Each child displayed as a card: name, date of birth (with calculated age), any special needs or notes |
| FR5.8 | Add/edit children | Agency can add, edit, and remove children. Minimum fields: name, date of birth. Optional: allergies, medical conditions, special needs, personality notes |
| FR5.9 | Age auto-calculation | Ages displayed as calculated values (e.g. "2 years 4 months") and update automatically |
| FR5.10 | Children-driven matching | Children's ages and needs are used as matching criteria when finding suitable nannies |

#### Requirements Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.11 | Care requirements | Structured capture: days needed (multi-select), hours per day, start time, end time, permanent vs casual vs temp |
| FR5.12 | Special requirements | Free-text field (max 1000 chars) for specific needs. Prompted categories with free-text: dietary requirements, language preferences, pet in household (yes/no + type), driving required (yes/no), other notes. At least one field must be filled or explicitly marked "none" |
| FR5.13 | Nanny preferences | Family's preferences: experience level, age range, gender preference, qualifications required |
| FR5.14 | Schedule display | Visual weekly schedule grid (Mon–Sun rows, hours as columns) showing requested care blocks. Same component as nanny availability grid (FR4.6) with different colour to distinguish "needs care" from "is available". Blocks show start/end times on hover |
| FR5.15 | Requirements → Matching | "Find Matching Nannies" action from requirements tab filters available nannies by compatibility |

#### Placements Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.16 | Placement history | Chronological list of all placements: nanny name, dates, status. Current placement highlighted at top |
| FR5.17 | Placement detail link | Each placement links to the full placement detail page (see FR6) |

#### Timesheets Tab (FYI)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.18 | FYI timesheet view | Approved timesheets for the family's active placements. View only — for reference, not action |
| FR5.19 | Hours summary | Summary: hours this week, hours this month, by nanny if multiple placements |

#### Activity Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.20 | Activity log | Chronological feed of all interactions: notes, status changes, placements, contract activity, messages sent/received |
| FR5.21 | Add note | Agency staff can add free-text notes |
| FR5.22 | Activity attribution | Each entry shows who and when |

---

### FR6: Placement Management
**Priority:** P0 (MVP)

**Design rationale:** Placements are the core unit of the agency's business — the connection between a nanny and a family. The placement page is where schedule, contract, timesheets, and both profiles converge. Contracts and agreements are managed within placement context — not as a separate section.

#### Placement List

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.1 | Placement list view | All placements in a filterable list: nanny name, family name, status, start date, schedule summary, rate |
| FR6.2 | Status filter tabs | Filter tabs: **Active** · **Upcoming** · **Trial** · **Completed** · **All**. Default: Active |
| FR6.3 | Calendar/timeline view | Toggle to a timeline view showing all placements on a calendar. Visual blocks per nanny showing which days/times they're placed. Useful for spotting availability gaps and scheduling conflicts |

#### Creating a Placement

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.4 | Create placement | Wizard flow: Step 1: Select nanny (searchable dropdown, only Active nannies shown) + Select family (searchable dropdown, only Active/Prospect families). Step 2: Placement type (Permanent/Casual/Temporary/Trial), start date (required), end date (required for Temporary/Trial, optional for Permanent/Casual). Step 3: Weekly schedule (day-by-day: start time, end time, break). Step 4: Rate (amount, rate type). Step 5: Review + confirm. All steps reversible. Draft saved between steps |
| FR6.5 | Placement type | Types: **Permanent**, **Casual**, **Temporary**, **Trial**. Trial placements auto-flag for review at trial end date |
| FR6.6 | Rate structure | Rate types: Hourly (default), Daily flat, Tiered. Hourly: single rate in AUD (e.g. $35.00/hr). Daily: single flat rate (e.g. $280/day). Tiered: standard rate + evening rate (after 6pm) + Saturday rate + Sunday rate + public holiday rate. Each rate stored as decimal to 2 places. Minimum: $0.01. Maximum: $999.99. Rate displayed with type label (e.g. "$35.00/hr" or "$280/day" or "$35/$40/$45 tiered") |
| FR6.7 | Matching assistance | Filter available nannies by: availability, location, qualifications, preferences. Surface potential matches for a family's requirements |
| FR6.8 | Conflict detection | System warns if a nanny's proposed schedule overlaps with an existing active placement |

#### Placement Detail Page

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.9 | Placement header | Displays: nanny name + family name (both clickable to their profiles), status badge (Proposed / Confirmed / Active / Trial / Completed / Terminated), placement type badge, start date, end date |
| FR6.10 | Schedule section | Visual weekly schedule showing placement hours (Mon–Sun grid). Editable by agency. Shows: day, start time, end time, break, total hours per day, total hours per week |
| FR6.11 | Rate & terms section | Rate details: rate type, rate amount, any penalty/overtime rates configured. Terms: free-text notes on arrangement specifics |
| FR6.12 | Contract & agreements section | Contract management within the placement context. Linked contract with status badge. Quick actions: Generate Contract (if none), View Contract, Send for Signing. If no contract yet, prominent prompt to create one. Supports multiple agreement types per placement |
| FR6.13 | Timesheet summary | Recent timesheets for this placement. Hours this week / this month / total. Link to full timesheet list filtered to this placement |
| FR6.14 | Nanny card | Summary card: nanny photo, name, compliance indicator, phone, key qualifications. Click through to full nanny profile |
| FR6.15 | Family card | Summary card: family name, children summary (names + ages), address, phone. Click through to full family profile |
| FR6.16 | Placement notes | Free-text notes specific to this placement (e.g. "Family prefers pickup from school at 3pm on Wednesdays") |
| FR6.17 | Placement activity log | Chronological log: status changes, schedule modifications, contract events, timesheet submissions, notes added |

#### Placement Lifecycle

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.18 | Placement status flow | Statuses: Proposed → Confirmed → Active → Completed / Terminated. Trial placements: Proposed → Trial → Active → Completed / Terminated |
| FR6.19 | Trial review prompt | Trial placements surface a review prompt on the dashboard when trial end date is approaching (7 days before). Options: Convert to Permanent, Extend Trial, End Placement |
| FR6.20 | Placement history | Full history of all placements for both nannies and families, accessible from their respective profile pages |

#### Contract Management (within Placements)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.21 | Contract templates | Agency can create and manage contract templates with merge fields |
| FR6.22 | Contract generation | Generate contract from template, auto-populated with nanny/family/placement data |
| FR6.23 | Contract tracking | Track status: Draft → Sent → Signed → Active → Expired / Terminated |
| FR6.24 | Document storage | Generated contracts stored against the relevant placement, nanny, and family records |
| FR6.25 | AU compliance fields | Contract templates include merge fields for: Fair Work Information Statement reference, applicable Modern Award name, hourly/annual rate, ordinary hours per week, notice period (weeks), probation period, superannuation fund details, leave entitlements summary. A "Compliance checklist" sidebar in the template editor shows which AU-required fields are present and which are missing |

---

### FR7: Listings (Recruitment Pipeline)
**Priority:** P0 (MVP)

**Design rationale:** Listings tracks the nanny recruitment funnel — from enquiry to active. It's a separate page from the Nannies directory. Nannies live in the directory (FR3); Listings tracks their recruitment journey. Stages advance when real actions are completed — not by manual drag. This ensures data quality and compliance.

#### Listings View

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR7.1 | Listings board | Kanban-style board showing nannies grouped by stage: **Enquiry** → **Application** → **Interview** → **Reference Check** → **Onboarding** → **Active** |
| FR7.2 | Stage counts | Each column shows the count of nannies in that stage |
| FR7.3 | Nanny cards | Each card shows: name, photo/initials, days in current stage, completion indicator (how many stage requirements are met) |
| FR7.4 | Click to profile | Clicking a listing card opens the nanny's full profile page |
| FR7.5 | Stale indicator | Cards in a stage for longer than a configurable threshold (default: 14 days) show a visual "stale" indicator. Stale nannies also surface on the dashboard attention panel |

#### Action-Driven Stage Progression

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR7.6 | Stage requirements | Each listing stage has defined requirements that must be completed before advancing. Requirements are visible on the nanny's profile as a checklist |
| FR7.7 | Enquiry → Application | Advances when: application form is completed (either via public intake form or manually entered by agency). Required data: personal details, qualifications, availability |
| FR7.8 | Application → Interview | Advances when: interview is scheduled AND interview notes are recorded on the nanny's profile. Required: interview date, interviewer name, interview notes (structured or free-text) |
| FR7.9 | Interview → Reference Check | Advances when: at least 2 reference checks are captured. Each reference: referee name, relationship, contact details, reference notes, outcome (positive/concerns/declined) |
| FR7.10 | Reference Check → Onboarding | Advances when: all reference checks have positive outcomes AND agency staff confirms advancement. Gate: manual approval by coordinator/admin |
| FR7.11 | Onboarding → Active | Advances when: all required documents are uploaded and verified (WWCC, First Aid, Police Check at minimum), onboarding checklist is 100% complete, nanny has been invited to portal |
| FR7.12 | Advancement prompt | When all stage requirements are met, the nanny's profile shows a prominent "Ready to advance to [next stage]" prompt. Agency staff confirms to advance |
| FR7.13 | Manual override | Agency staff with Admin+ role can manually advance or revert a nanny's stage with a required reason note. Override logged in activity |
| FR7.14 | Stage history | Full history of stage transitions: from, to, date, triggered by (action or manual override), who confirmed |

#### Listings Filters & Search

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR7.15 | Listings filters | Filter listings by: assigned coordinator, tags, date range (entered listings), stale only |
| FR7.16 | Listings search | Search nannies within the listings by name |

---

### FR8: Timesheets
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR8.1 | Nanny timesheet submission | Nanny submits: date (cannot be future, max 14 days in past), start time (15-min increments), end time (must be after start, 15-min increments), break duration (0/15/30/45/60 min select), placement (auto-selected if only one active), notes (optional, max 500 chars). Total hours auto-calculated as (end - start - break). Minimum entry: 0.25 hours. Maximum entry: 16 hours per day |
| FR8.2 | Approval workflow | States: Draft → Submitted → Approved / Rejected. Nanny submits → status becomes "Submitted" → agency reviewer sees in queue → clicks Approve (one-click) or Reject (requires reason, min 10 chars). Approved timesheets are immutable. Rejected timesheets return to nanny as "Rejected" with reason displayed — nanny can edit and resubmit. Agency can bulk-approve multiple timesheets from the same nanny |
| FR8.3 | Family FYI view | Family can see approved timesheets for their placement. View only — no action required unless flagged |
| FR8.4 | Timesheet summary | Agency dashboard: weekly/monthly summary per nanny, per placement |
| FR8.5 | Overtime/penalty rate flags | System flags entries where: daily hours exceed 8 (overtime), weekly hours for a placement exceed 38 (overtime), entry falls on Saturday (penalty), entry falls on Sunday (higher penalty), entry falls on a public holiday (AU national + state-specific). Flags are visual indicators (amber badge) on the timesheet entry — informational only, not blocking. Tooltip shows: "This entry may attract [overtime/Saturday/Sunday/public holiday] rates under the relevant award" |

---

### FR9: Onboarding
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR9.1 | Default onboarding checklist | Agency has a default checklist template applied to all new nannies entering Onboarding stage. Default items: Upload WWCC, Upload First Aid Certificate, Upload Police Check, Complete profile (photo, availability, qualifications), Review agency policies (acknowledgement checkbox), Bank details for timesheets. Agency can customise the default template in Settings |
| FR9.2 | Per-nanny checklist | When a nanny enters Onboarding, the default template is copied to their profile. Agency can add/remove/reorder items for that specific nanny without affecting the template |
| FR9.3 | Checklist item types | Three item types: **Document** (links to document upload — auto-completes when doc uploaded and verified), **Task** (manual checkbox — completed by agency or nanny), **Acknowledgement** (nanny must read and confirm — e.g. agency policies) |
| FR9.4 | Onboarding progress | Progress bar on nanny profile showing X of Y items complete (percentage). Progress visible on: nanny profile header, Listings board card, dashboard attention panel (if <50% after 7 days) |
| FR9.5 | Nanny self-service | Nanny can complete applicable items from their portal: upload documents, tick tasks assigned to them, sign acknowledgements. Items marked "agency-only" are not visible to the nanny |
| FR9.6 | Completion triggers | When all required items are complete: prominent "Ready to advance to Active" prompt on nanny profile. Notification sent to assigned coordinator. Nanny remains in Onboarding until agency confirms advancement (see FR7.11) |

---

### FR10: Communication
**Priority:** P0 (MVP)

**Design rationale:** Agencies need to communicate with nannies and families directly from the platform. This replaces scattered email/SMS/WhatsApp threads with a centralised, logged communication system. Every message is recorded in the contact's activity log. The Communication page provides a unified view of all agency messaging — inbound and outbound.

#### Communication Page

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.1 | Communication hub | Dedicated Communication page with three tabs: **Inbox**, **Sent**, **Templates** |
| FR10.2 | Inbox tab | Displays all inbound messages: sender name, subject, preview, date, read/unread state. Unread messages visually distinct. Click to open full message |
| FR10.3 | Sent tab | Displays all outbound messages: recipient(s), subject, date, delivery status (sent/delivered/failed), recipient count for bulk sends |
| FR10.4 | Templates tab | Grid of reusable message templates: name, category, description, last used date. Click to preview or edit |

#### In-App Notifications

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.5 | Notification bell | Persistent notification icon in the app header showing unread count. Clicking opens a notification dropdown/panel |
| FR10.6 | Notification list | List of notifications: document expiring, timesheet submitted, contract signed, listing stage change, message received. Each notification links to the relevant record |
| FR10.7 | Read/unread state | Notifications can be marked as read individually or "mark all as read" |
| FR10.8 | Notification preferences | In Settings → Notifications, each staff member can toggle on/off by category: Document alerts (expiring/expired), Timesheet alerts (submitted/overdue), Listing alerts (stage changes/stale), Communication alerts (new inbound messages), Placement alerts (trial ending/contract unsigned). Default: all on for Owners/Admins, all except Placement alerts for Coordinators |

#### Sending Messages

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.9 | Send message to individual | From any nanny or family profile, "Send Message" button opens the composer. Message delivered via the contact's preferred channel (email default, SMS if preferred and phone available). Delivery confirmed within 30 seconds (email) or 60 seconds (SMS). Success toast: "Message sent to [name] via [channel]". Failed: error toast with retry. Message logged in contact's activity log with: timestamp, channel, status, sender (staff member), subject, body preview |
| FR10.10 | Message composer | Rich-text composer with: subject line (email only), message body, optional attachment. Templates available for common messages (e.g. "Welcome", "Document reminder", "Timesheet overdue") |
| FR10.11 | Message templates | Agency can create, edit, duplicate, and delete templates. Each template has: name (required, max 100 chars), category (select: Welcome, Reminder, Update, Contract, Custom), body with merge fields. Available merge fields: {{first_name}}, {{last_name}}, {{full_name}}, {{placement_start_date}}, {{placement_end_date}}, {{nanny_name}}, {{family_name}}, {{agency_name}}. Invalid merge fields highlighted in red in editor. Template preview shows sample data. Maximum 50 templates per agency |
| FR10.12 | Delivery channel | Messages sent via email (default) or SMS (if phone number available and SMS enabled). Channel selected automatically based on contact's communication preference, or manually by sender |

#### Receiving Messages (Inbound)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.13 | Inbound message reception | System receives inbound email replies and SMS responses. Messages appear in the Communication inbox and on the relevant contact's activity log |
| FR10.14 | Message threading | Inbound messages are threaded with the original outbound message where possible. Thread view shows full conversation history |
| FR10.15 | Unread indicators | New inbound messages trigger: notification bell count increase, unread badge on Communication nav item, unread indicator on the sender's contact profile |
| FR10.16 | Reply from inbox | Agency can reply to inbound messages directly from the Communication inbox. Reply is sent via the same channel as the original message |

#### Bulk Messaging

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.17 | Bulk send from directories | Select multiple contacts from the Nannies or Families directory → "Send Message" bulk action. Opens the message composer with recipient list. Merge fields personalise each message |
| FR10.18 | Recipient filtering | Bulk message recipients can be filtered by: type (all nannies, all families), tags, status, placement status. Preview recipient count before sending |
| FR10.19 | Bulk send confirmation | Before sending, show: recipient count, message preview (with sample merge field values), delivery channel breakdown (X via email, Y via SMS). Require explicit confirmation |
| FR10.20 | Bulk send logging | Each bulk message logged in every recipient's activity log as an individual message. Bulk send also logged in a central message history for the agency |

#### Message History

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.21 | Contact message history | Each contact's activity tab shows all messages sent to and received from them: date, subject/preview, delivery channel, status (sent/delivered/failed), direction (inbound/outbound) |
| FR10.22 | Agency message log | Central Communication page (Sent tab) showing all messages sent by the agency: date, sender (staff member), recipients, subject, status |

#### Email Notifications for Critical Items

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.23 | Critical email alerts | System sends email alerts to relevant agency staff for critical events: document expired (WWCC, First Aid, Police Check), contract unsigned after 7 days, timesheet unapproved after 3 days |
| FR10.24 | Alert routing | Alerts sent to: the coordinator assigned to the nanny/family (if assigned), or all admins/owners if no coordinator assigned |

---

### FR11: Team & Multi-user
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR11.1 | Invite team member | Owner/Admin enters email + selects role (Admin or Coordinator). System sends invitation email with magic link. Invite expires after 7 days. Pending invites shown in Settings → Team with resend/revoke options |
| FR11.2 | Role-based permissions | **Owner:** all features + billing + team management + delete agency. **Admin:** all features + team management (cannot delete agency or manage billing). **Coordinator:** nannies, families, placements, timesheets, communication, listings. Cannot access Settings, team management, or billing. Permissions enforced server-side via RLS + middleware, not just UI hiding |
| FR11.3 | Activity attribution | Every data mutation records: actor (staff member ID + name), action type, timestamp, entity affected. Displayed in activity logs throughout the app. Cannot be edited or deleted |
| FR11.4 | Team directory | Settings → Team shows all active staff: name, email, role, last active date, status (Active/Invited/Deactivated). Owner can change roles (except cannot demote themselves), deactivate members (preserves history, revokes access) |
| FR11.5 | Coordinator assignment | Nannies and families can be assigned to a coordinator. Assignment shown on profile header. Filterable in directories. Affects notification routing (see FR10.24) |

---

### FR12: Authentication & Tenant
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR12.1 | Agency registration | Sign-up flow: agency name, owner name, owner email, password (min 8 chars, complexity enforced). After sign-up: onboarding wizard (add logo, set branding colour, invite first team member — all skippable). Agency gets a unique slug (e.g. "little-stars") used for public form URLs |
| FR12.2 | Multi-tenant isolation | Every database table includes agency_id. Supabase RLS policies enforce: users can only read/write rows matching their agency_id. RLS policies tested in CI with cross-tenant access assertions. No API endpoint returns data without agency_id scoping |
| FR12.3 | Agency staff auth | Email + password via Supabase Auth. Optional MFA (TOTP). Session: 8-hour expiry, refresh token rotated on use. Password reset via email link (expires 1 hour) |
| FR12.4 | Nanny/family portal auth | Magic link only (no password). Agency sends portal invite → nanny/family receives email with magic link → link creates Supabase Auth account on first use. Subsequent logins: enter email → receive magic link. Session: 30 days with remember-me (default on). Magic links expire after 1 hour, single-use |
| FR12.5 | Role routing | After auth, user routed by role: agency staff → admin dashboard, nanny → nanny portal, family → family portal. If user has multiple roles (edge case): role selector on login |
| FR12.6 | Account deactivation | Deactivated users cannot log in. Active sessions revoked within 5 minutes (JWT expiry). Deactivated staff: data preserved, actions attributed, but no access. Deactivated nannies/families: portal inaccessible, agency can still view their records |

---

### FR13: Form UX & Data Entry
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR13.1 | Multi-step wizard pattern | All complex forms (nanny profile, family profile, placement creation) use a step-by-step wizard with progress indicator. Max 4-6 fields visible per step |
| FR13.2 | Select over input | Where a finite set of options exists, use select/dropdown/toggle/radio — not free text. Examples: qualifications, availability days, suburb, care type, certification type |
| FR13.3 | Smart defaults and presets | Common values pre-selected where sensible. Example: break = 30min, start time = 8:00am, standard availability = Mon-Fri |
| FR13.4 | Save as draft | Partially completed forms save automatically. Users can return and finish later |
| FR13.5 | Inline validation | Validation feedback appears inline as fields are completed — not on submit. Clear error messages with fix suggestions |
| FR13.6 | Minimal required fields | Only fields essential to create the record are required. Everything else is optional and can be added later |
| FR13.7 | Mobile-optimised forms | All forms work on mobile. Large touch targets (44px min). Single-column layout. Appropriate keyboard types (tel, email, date) |
| FR13.8 | Contextual help | Complex or ambiguous fields include a short help text or tooltip. Example: "WWCC number format: VIC-XXXXXXX" |

**Form UX Principles:**
1. **Prefer selection over typing** — dropdowns, toggles, chips, radio groups
2. **Progressive disclosure** — show only what is needed at each step
3. **Forgiving** — save progress, allow skipping optional sections
4. **Fast path** — common scenarios take the fewest steps

---

### FR14: Public Intake Forms (Agency-Branded)
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR14.1 | Public nanny application form | Agency has a unique URL (e.g. app.nannyCRM.com/apply/little-stars) that nannies can access without logging in. Captures: personal details, qualifications, availability, preferences. Submits directly into the CRM as a new nanny contact in "Enquiry" listing stage |
| FR14.2 | Public family registration form | Agency has a unique URL (e.g. app.nannyCRM.com/register/little-stars) for families. Captures: parent details, children, care needs, preferences. Submits into CRM as a new family contact in "Prospect" status |
| FR14.3 | Agency branding on public forms | Public forms display: agency logo, agency name, agency colour (optional). The form feels like the agency's own tool, not a generic platform |
| FR14.4 | No login required | Public forms are accessible without authentication. Email verification optional (post-MVP) |
| FR14.5 | Confirmation page | After submission, show a branded thank-you page with next steps ("We'll be in touch within 48 hours") |
| FR14.6 | Embeddable (future) | Forms can be embedded into an agency's existing website via iframe or script tag. Out of scope for MVP but architecture should not prevent it |
| FR14.7 | Form customisation (future) | Agencies can toggle fields on/off and reorder sections. Out of scope for MVP — all agencies get the same form structure |

**Key principle:** These forms are the agency's first impression. They must be beautiful, minimal, and fast to complete. Select over input. No unnecessary fields. Mobile-first.

---

## Agency Portal Navigation

The sidebar navigation for agency staff follows this structure:

```
🏠 Dashboard        → Metrics, attention items, activity feed
👨‍👩‍👧 Families         → Family directory (Prospect / Active / Inactive)
❤️ Nannies           → Nanny directory with compliance indicators
📋 Listings          → Recruitment funnel (action-driven stage progression)
🤝 Placements        → Active placements, contracts, agreements, calendar view
⏱️ Timesheets        → Submissions, approvals, summaries
💬 Communication     → Inbox, sent messages, templates, agency inbox
⚙️ Settings          → Agency branding, team, templates, notification preferences
```

**Key design decisions:**
- **Families** and **Nannies** are separate top-level directories. No unified "People" page.
- **Listings** tracks the nanny recruitment funnel. Stages advance via completed actions, not manual drag.
- **Placements** houses contracts and agreements alongside placement details. No separate Contracts page.
- **Communication** provides a unified messaging hub — inbound and outbound.
- **Global search** (⌘K) is accessible from any page via the header.
- **Other contacts** (referrers, partners) are dropped for MVP.

---

## Data Model (Conceptual)

This section defines the core entities and their relationships. Detailed schema is defined in Architecture — this captures the PRD-level data expectations.

### Core Entities

| Entity | Key Fields | Relationships |
|--------|-----------|---------------|
| **Agency** (tenant) | name, logo, colour, subscription_tier, created_at | Has many: staff, nannies, families, placements, templates, tags |
| **Staff** | first_name, last_name, email, role (Owner/Admin/Coordinator), status (Active/Invited/Deactivated), last_active_at, mfa_enabled | Belongs to: agency. Has many: activity_log entries (as actor). Assigned to: nannies, families (as coordinator) |
| **Nanny** | first_name, last_name, email, phone, dob, address, suburb, status, listing_stage, hourly_rate, availability (weekly grid), work_rights, visa_expiry, assigned_coordinator_id | Belongs to: agency. Has many: documents, placements, timesheets, tags, activity_log entries, messages, onboarding_items, reference_checks, listing_stage_requirements |
| **Family** | display_name, primary_parent (name, email, phone), secondary_parent, address, suburb, status, communication_preference, assigned_coordinator_id | Belongs to: agency. Has many: children, placements, tags, activity_log entries, messages, requirements |
| **Child** | first_name, dob, allergies, medical_conditions, special_needs, notes | Belongs to: family |
| **Placement** | type (Permanent/Casual/Temporary/Trial), status, start_date, end_date, schedule (weekly), rate_type, rate_amount, notes | Belongs to: agency, nanny, family. Has many: timesheets, contracts, activity_log entries |
| **Contract** | status (Draft/Sent/Signed/Active/Expired/Terminated), template_used, generated_content, signed_date | Belongs to: placement. References: nanny, family |
| **Timesheet Entry** | date, start_time, end_time, break_minutes, total_hours, status (Draft/Submitted/Approved/Rejected), rejection_reason, notes | Belongs to: placement, nanny. Reviewed by: staff |
| **Document** | type (WWCC/First Aid/Police Check/Qualification/Other), name, file_url, status (Pending/Verified/Expiring/Expired), expiry_date, uploaded_at, verified_by, verified_at | Belongs to: nanny |
| **Message** | direction (inbound/outbound), channel (email/SMS), subject, body, status (sent/delivered/failed), sent_at, thread_id | Belongs to: agency. References: sender (staff or contact), recipient (nanny or family) |
| **Template** (message) | name, category, body_with_merge_fields, last_used_at | Belongs to: agency |
| **Template** (contract) | name, body_with_merge_fields, au_compliance_fields | Belongs to: agency |
| **Tag** | name, colour | Belongs to: agency. Many-to-many: nannies, families |
| **Activity Log Entry** | action_type, description, actor (staff/nanny/family), timestamp, entity_type, entity_id | Belongs to: agency |
| **Notification** | type, title, body, read, entity_type, entity_id, created_at | Belongs to: staff |
| **Onboarding Item** | title, type (document/task/acknowledgement), required, completed, completed_at, assigned_to (agency/nanny/both), agency_only (boolean) | Belongs to: nanny. Template source: Onboarding Template |
| **Reference Check** | referee_name, relationship, contact, notes, outcome (positive/concerns/declined) | Belongs to: nanny |
| **Onboarding Template** | name, items (ordered list of default checklist items), is_default (boolean) | Belongs to: agency |
| **Team Invite** | email, role, invited_by, status (pending/accepted/expired/revoked), token, expires_at | Belongs to: agency |
| **Listing Stage Requirement** | stage, requirement_description, met (boolean), met_at | Belongs to: nanny |

### Key Constraints

- **Tenant isolation:** All queries scoped by agency_id. Supabase RLS enforces at database level
- **Soft deletes:** Records are archived (status = inactive), not hard-deleted. Preserves audit trail
- **Timestamps:** All entities have created_at, updated_at (auto-managed)
- **Audit:** All mutations logged in activity_log with actor, action, timestamp

---

## Edge Cases & Error Handling

This section defines system behaviour for error states, empty states, and boundary conditions that apply across features.

### Empty States

| Context | Behaviour |
|---------|-----------|
| Dashboard — no nannies/families yet | Show onboarding prompt: "Add your first nanny to get started" with quick-action button. Metric cards show 0 |
| Directory (Nannies/Families) — no records | Show illustrated empty state with "Add [Nanny/Family]" CTA. No blank table |
| Listings board — no nannies in listings | Show empty kanban with stage headers and "Add your first nanny to start recruiting" prompt |
| Placements — no placements | Empty state: "Create your first placement to connect a nanny with a family" |
| Timesheets — no submissions | Empty state: "No timesheets submitted yet. Timesheets will appear here once nannies submit hours" |
| Communication inbox — no messages | Empty state: "No messages yet. Messages from nannies and families will appear here" |
| Search results — no matches | "No results found for [query]. Try a different search term" with suggestion to broaden filters |
| Profile tabs with no data | Each tab shows contextual empty state (e.g. Documents tab: "No documents uploaded yet. Upload the first document to track compliance") |

### Error States

| Context | Behaviour |
|---------|-----------|
| Document upload fails | Inline error: "Upload failed — [reason: file too large / unsupported format / network error]. Try again." File size limit: 10MB. Supported: PDF, JPG, PNG |
| Document upload — invalid type | Reject immediately with: "Unsupported file type. Please upload PDF, JPG, or PNG" |
| Message delivery fails (email) | Mark message as "Failed" in sent log. Show retry button. Log failure reason. Surface on dashboard attention panel if critical (contract/document reminder) |
| Message delivery fails (SMS) | Mark as "Failed". Fallback: prompt sender to try email channel instead. Do not auto-retry SMS (cost) |
| Bulk message — partial failure | Show delivery summary: "48 of 50 sent successfully. 2 failed." Link to failed recipients with retry option |
| Contract generation — missing merge fields | Show warning listing missing fields before generation. Allow generation with placeholders marked as "[MISSING: field_name]" |
| Placement conflict detected | Modal warning: "This nanny already has an active placement on [days]. Overlapping hours: [details]. Create anyway?" Require explicit confirmation |
| Concurrent editing | Last-write-wins with notification: "This record was updated by [user] at [time]. Your changes have been saved but may have overwritten their edits. Review the activity log." |
| Session timeout | Redirect to login with message: "Your session has expired. Please log in again." Preserve unsaved form data in local storage where possible |
| Network error (API failure) | Toast notification: "Something went wrong. Please try again." Retry button. No data loss — pending changes preserved in local state |
| Timesheet rejection — no reason | Rejection requires a reason (text field). Cannot reject without explanation |
| Public form submission — duplicate email | Accept submission. Flag as potential duplicate in CRM. Agency decides whether to merge or keep separate |
| Nanny invited but email bounces | Surface on dashboard attention panel: "Portal invite failed for [name] — email bounced. Update email address" |
| Trial placement — end date passes without review | Auto-surface on dashboard: "Trial for [nanny] with [family] ended [N days ago] without review. Action required: Convert, Extend, or End" |

### Boundary Conditions

| Condition | Behaviour |
|-----------|-----------|
| Maximum children per family | No hard limit. UI handles 1–10+ children gracefully (scrollable list, not fixed grid) |
| Maximum placements per nanny | System supports multiple concurrent placements (common for casual nannies). Conflict detection warns but does not block |
| Maximum team members per agency | No hard limit at MVP. Pricing tiers may restrict post-MVP |
| Tag limits | Maximum 50 tags per entity. Maximum 20 characters per tag |
| Search query length | Maximum 200 characters. Queries exceeding limit are truncated with notice |
| Bulk message recipient limit | Maximum 500 recipients per bulk send. If selection exceeds 500, show: "Maximum 500 recipients per send. Please narrow your selection" |
| File storage per agency | 5GB at MVP. Approaching limit (80%): warning banner. At limit: block new uploads with upgrade prompt |
| Timesheet — future dates | Cannot submit timesheets for future dates. Date picker restricts to today or earlier |
| Timesheet — overlapping entries | Warn if a timesheet entry overlaps with an existing approved entry for the same placement and date. Allow override with confirmation |
| Rate — negative or zero values | Reject. Rate must be a positive number. Validation inline: "Rate must be greater than $0" |
| Contract — unsigned after 30 days | Auto-expire unsigned contracts. Surface on dashboard: "Contract for [placement] expired unsigned. Generate a new one?" |

---

## Non-Functional Requirements

| ID | Category | Requirement | Target |
|----|----------|-------------|--------|
| NFR-01 | Performance | Page load time | First Contentful Paint < 1.5s, Largest Contentful Paint < 2.5s on simulated 4G (1.6Mbps down, 750ms RTT). Measured via Lighthouse CI in deployment pipeline. Directory pages with 500+ records: initial render < 2s with virtual scrolling, search results < 300ms |
| NFR-02 | Security | Data isolation | Complete tenant isolation via Supabase RLS. Every table includes agency_id column. All queries filtered by agency_id at the database level (not application level). RLS policies tested with cross-tenant access attempts in CI |
| NFR-03 | Security | Authentication | Supabase Auth with RLS. Agency staff: email + password with optional MFA. Nannies/Families: magic link (email) for portal access — no password to manage. Session timeout: 8 hours (agency staff), 30 days (portal users with remember-me). JWT refresh handled client-side |
| NFR-04 | Accessibility | WCAG | 2.1 AA minimum. All form inputs have labels. Colour is never the sole indicator (icons/text accompany red/amber/green). Keyboard navigation for all actions. Screen reader tested on Dashboard, Directories, and Profile pages |
| NFR-05 | Mobile | Responsive | Fully responsive. Breakpoints: mobile (<640px), tablet (640–1024px), desktop (>1024px). Nanny/family portals designed mobile-first. Agency admin usable on tablet but optimised for desktop. Touch targets minimum 44×44px |
| NFR-06 | Compliance | AU employment law | Contract templates support Fair Work, NES, award rates. Templates include disclaimer: "This template is a starting point — agencies are responsible for ensuring legal compliance." Templates reviewed against Fair Work template library but not legally certified |
| NFR-07 | Scalability | Concurrent agencies | Support 100+ agencies. Supabase connection pooling (PgBouncer) with per-tenant query budget. Database indexes on agency_id + commonly filtered columns (status, created_at). Vercel Edge Functions for API routes. Static assets on Vercel CDN. Document storage on Supabase Storage with per-agency 5GB limit |
| NFR-08 | Data | Backup | Supabase managed backups: daily point-in-time recovery, 7-day retention (Pro plan). Document storage: redundant across Supabase Storage regions |
| NFR-10 | Real-time | Live updates | Dashboard attention panel, notification bell count, and activity feed use Supabase Realtime (WebSocket subscriptions). Directories and profiles use standard request/response (no real-time needed). Fallback: polling every 60s if WebSocket connection drops |
| NFR-11 | API | Rate limiting | API rate limits per agency: 100 requests/second (burst), 1000 requests/minute (sustained). Bulk messaging: max 10 messages/second to prevent email/SMS provider throttling. Public intake forms: 10 submissions/minute per IP (spam protection) |
| NFR-12 | Integration | Email (Resend) | Outbound: Resend API for transactional email. Inbound: Resend webhook for reply reception — webhook endpoint validates signature, parses sender, matches to contact by email address, creates Message record. Delivery status tracked via Resend webhooks (sent/delivered/bounced/complained) |
| NFR-13 | Integration | SMS (Twilio) | Outbound: Twilio Programmable SMS. Inbound: Twilio webhook for reply reception. Delivery receipts via status callback URL. SMS opt-in stored per contact. Cost: agency pays per-message (passed through or bundled in subscription). Fallback: if SMS fails, surface in UI — do not auto-retry (cost) |
| NFR-14 | Caching | Client-side | SWR (stale-while-revalidate) for directory listings and profile data. Cache TTL: 30s for directories, 60s for profiles, 0s (no cache) for timesheets and notifications. Optimistic updates for status changes and form submissions |
| NFR-09 | Availability | Uptime | 99.5% measured monthly (excludes scheduled maintenance windows announced 48h in advance). Maximum unplanned downtime: 3.6 hours/month. Health check endpoint responds within 500ms |

---

## User Flows

### Flow 1: Agency onboards a new nanny (listings-driven)
```
Nanny submits public application form (FR14.1) →
Appears in Listings at "Enquiry" stage (FR7.1) →
Agency reviews application → records interview notes (FR7.8) →
Listings advances to "Interview" →
Agency captures 2+ reference checks with outcomes (FR7.9) →
Listings advances to "Reference Check" →
References positive → agency confirms advancement (FR7.10) →
Listings advances to "Onboarding" →
Default onboarding checklist copied to nanny (FR9.1, FR9.2) →
Agency sends portal invite → magic link email (FR12.4) →
Nanny opens portal → uploads WWCC, First Aid, Police Check (FR9.5) →
Nanny completes profile, signs acknowledgements (FR9.3) →
Onboarding progress reaches 100% → "Ready to advance" prompt (FR9.6) →
Agency confirms → Listings advances to "Active" (FR7.11) →
Nanny ready for placement
```

### Flow 2: Agency places a nanny with a family
```
Family registered with requirements (via Families → Add Family) →
Agency opens family's Requirements tab → "Find Matching Nannies" →
Match proposed → Placement created (nanny + family + schedule + rate + type) →
Contract generated from template within placement → Contract sent for signing →
Placement status: Active (or Trial) → Timesheets begin
```

### Flow 3: Nanny submits a timesheet
```
Nanny logs hours in portal → Submits for review →
Agency reviews + approves → Family sees FYI summary →
Timesheet data available for reporting/export
```

### Flow 4: Family experience (minimal)
```
Agency sends portal invite → magic link email (FR12.4) →
Family clicks link → account created automatically →
Views placement details + nanny info (FR5.6) →
Receives FYI timesheet summaries (FR5.18) →
Only prompted when: contract signing (FR6.12), issue flagged, feedback requested →
Subsequent logins: enter email → magic link (no password)
```

### Flow 5: Agency coordinator daily workflow
```
Opens Dashboard → Reviews attention items (expiring docs, pending timesheets, stale listing cards) →
Clicks through to resolve → Checks activity feed for updates →
Checks Communication inbox → responds to inbound messages →
Checks Listings → advances nannies with completed requirements →
Navigates to Nannies/Families for ad-hoc lookups →
Reviews Placements → checks upcoming trial reviews →
Reviews Timesheets → approves pending → Done
```

### Flow 6: Agency sends bulk update
```
Agency navigates to Nannies → Filters by tag "active" →
Selects all → Bulk action: Send Message →
Chooses template "Holiday hours update" → previews with merge fields →
Confirms → messages sent via preferred channels →
Each message logged in recipient's activity → appears in Communication Sent tab
```

### Flow 7: Agency receives and responds to inbound message
```
Nanny replies to availability check email →
Message appears in Communication inbox (unread) →
Notification bell shows count →
Coordinator opens inbox → reads message → clicks reply →
Reply sent via same channel → threaded in conversation →
Both messages logged in nanny's activity
```

---

## Scope

### In Scope (MVP)
Everything in FR1–FR14 above.

### Out of Scope (MVP)
- Other contacts (referrers, partners, generic contacts) — dropped for MVP
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
- [ ] SMS provider preference? (Twilio is the default recommendation)

---

## Feature Prioritisation (MoSCoW within MVP)

While all FRs are in MVP scope, they are not equal priority. This MoSCoW classification guides build order and identifies what could be deferred if timeline pressure requires it.

### Must Have (Launch blockers — product does not function without these)
- **FR1** Agency Dashboard (core: FR1.1–FR1.7. Activity feed FR1.8–FR1.10 is Should Have)
- **FR2** Families Directory (all)
- **FR3** Nannies Directory (all)
- **FR4** Nanny Profile (all tabs except Onboarding tab FR4.22–FR4.24 which is Should Have)
- **FR5** Family Profile (all tabs)
- **FR6** Placement Management (core: FR6.1–FR6.20. Contract management FR6.21–FR6.25 is Should Have)
- **FR7** Listings / Recruitment Pipeline (all — core differentiator)
- **FR8** Timesheets (FR8.1–FR8.4. Overtime flags FR8.5 is Should Have)
- **FR11** Team & Multi-user (all)
- **FR12** Authentication & Tenant (all)

### Should Have (Expected at launch but could ship in fast-follow if needed)
- **FR1.8–FR1.10** Activity feed on dashboard
- **FR1.12–FR1.13** Global search (⌘K)
- **FR4.22–FR4.24** Onboarding tab (checklist)
- **FR6.21–FR6.25** Contract management within placements
- **FR8.5** Overtime/penalty rate flags
- **FR9** Onboarding (configurable checklists)
- **FR10.1–FR10.12** Communication — outbound messaging, templates
- **FR13** Form UX patterns (progressive enhancement — basic forms work without wizards)

### Could Have (Valuable but clearly deferrable to post-launch sprint)
- **FR10.13–FR10.16** Communication — inbound message reception and threading
- **FR10.17–FR10.20** Bulk messaging
- **FR10.23–FR10.24** Critical email alerts
- **FR14** Public intake forms (agency-branded)

### Won't Have (Confirmed out of scope — listed for clarity)
- Payroll integration, invoicing, background check APIs, native mobile app, analytics, international support (see Out of Scope section)

### Critical Path (Build Order)

```
Phase 1 (Foundation):  FR12 Auth → FR11 Team → FR2 Families → FR3 Nannies
Phase 2 (Core):        FR4 Nanny Profiles → FR5 Family Profiles → FR7 Listings
Phase 3 (Operations):  FR6 Placements → FR8 Timesheets → FR1 Dashboard
Phase 4 (Enhancement): FR9 Onboarding → FR10 Communication → FR13 Form UX → FR14 Public Forms
```

Each phase depends on the previous. Within a phase, features can be parallelised.

---

## Risks

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| AU employment law complexity | High | High | Start with most common contract types; flag areas needing legal review |
| Contract template legal liability | Medium | High | Templates are starting points — agencies responsible for legal compliance. Add disclaimer |
| Family adoption friction | Medium | Medium | Keep family portal ultra-simple. Minimal required actions |
| Scope creep from agency feature requests | High | Medium | Strict MVP scope. Post-MVP backlog for additional features |
| Multi-tenant security | Low | Critical | Supabase RLS from day one. Tenant isolation tested thoroughly |
| SMS cost at scale | Medium | Low | SMS opt-in per agency. Email as default. SMS as premium feature if needed |
| Inbound message volume | Medium | Medium | Threaded conversations to manage volume. Notification preferences to control noise |

---

## Success Metrics

| Metric | Target | How Measured |
|--------|--------|--------------|
| Agency activation | Agency completes setup + adds first nanny within 7 days | Onboarding funnel tracking |
| Nanny adoption | 80% of invited nannies complete onboarding within 14 days | Onboarding completion rate |
| Timesheet submission | 90% of timesheets submitted on time | Submission tracking |
| Family satisfaction | Families rate experience 4+/5 | In-app feedback |
| Agency retention | 90% month-over-month retention | Subscription data |
| Listing velocity | Average time from Enquiry to Active < 21 days | Listing stage tracking |
| Communication adoption | 70% of agency messaging happens through the platform within 30 days | Message volume tracking |

---

## Dependencies

| Dependency | Type | Status | Risk |
|------------|------|--------|------|
| Supabase (DB, Auth, Storage) | External | Available | Low |
| Vercel (Hosting) | External | Available | Low |
| Resend (Email — outbound + inbound) | External | Available | Low |
| SMS provider (Twilio or similar) | External | TBD | Low — well-established providers |
| AU Fair Work award information | Research | Needed | Medium — affects contract templates |
| Agency user research | Research | Warm list available | Low — access confirmed |

---

## Approval

- [ ] Requirements complete and comprehensive
- [ ] Scope locked for MVP
- [ ] Open questions acceptable to proceed (can be resolved during solutioning)
- [ ] Bmac approved
- [ ] Ready to proceed to Architecture

> **Next step:** Bmac reviews PRD → update Architecture (data model, routing, messaging infrastructure) → break into Epics & Stories.
