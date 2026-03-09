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
6. **Actions drive progress** — Pipeline stages advance when real work is completed, not when someone drags a card.

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
| FR1.4 | Actionable items | Each attention item links directly to the relevant record/action. One click to resolve |
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

#### Global Search

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR1.12 | Global search (⌘K) | Keyboard shortcut (⌘K / Ctrl+K) opens a global search overlay accessible from any page. Searches across: people (nannies, families, contacts), placements, contracts. Results grouped by type with click-through to the relevant record |
| FR1.13 | Search in header | Persistent search icon in the app header that opens the same global search overlay |

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
| FR2.7 | Bulk actions | Select multiple contacts for: bulk tagging, bulk status change, bulk export, bulk message (see FR13) |

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

#### Other Contact Profiles

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR2.13 | Generic contact profile | Contacts of type Referrer, Partner, or Other open a simplified profile page: contact details (name, phone, email, address), tags, notes field, and activity log. No tabs — single scrollable page |
| FR2.14 | Contact type conversion | A contact's type can be changed (e.g. "Other" → "Nanny") which triggers the extended profile creation flow for that type |

---

### FR3: Nanny Profile Page
**Priority:** P0 (MVP)

**Design rationale:** The nanny profile is where the agency spends the most time. It needs to surface compliance status (documents), current placement, and pipeline position at a glance — then allow deep dives into each area.

#### Profile Header

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR3.1 | Profile header | Displays: photo/avatar, full name, status badge (Enquiry / Application / Interview / Reference Check / Onboarding / Active / Inactive), phone, email |
| FR3.2 | Header quick actions | Buttons: Edit Profile, Invite to Portal (if not yet invited), Send Message (see FR13), Archive, Contact (phone/email shortcuts) |
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
| FR3.18 | Placement detail link | Each placement links to the full placement detail page (see FR5) |

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
| FR3.25 | Activity log | Chronological feed of all interactions: status changes, notes added, documents uploaded, timesheets submitted, placements created/changed, portal invites sent, messages sent/received |
| FR3.26 | Add note | Agency staff can add free-text notes (e.g. "Spoke to Sarah re availability change — confirmed available Tuesdays from April") |
| FR3.27 | Activity attribution | Each entry shows who performed the action and when |

---

### FR4: Family Profile Page
**Priority:** P0 (MVP)

**Design rationale:** The family profile centres on two things: their children (the reason they need a nanny) and their care requirements (how the agency matches them). Everything else supports those core needs.

#### Profile Header

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.1 | Profile header | Displays: family display name, status badge (Prospect / Active / Inactive), primary parent name, phone, email, address |
| FR4.1a | Family display name | Auto-generated from primary parent surname as "The [Surname]s" (e.g. "The Johnsons"). Can be manually overridden for blended families or non-standard names (e.g. "Smith-Jones Family") |
| FR4.2 | Header quick actions | Buttons: Edit Profile, Invite to Portal (if not yet invited), Send Message (see FR13), Archive, Contact (phone/email shortcuts) |

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
| FR4.17 | Placement detail link | Each placement links to the full placement detail page (see FR5) |

#### Timesheets Tab (FYI)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.18 | FYI timesheet view | Approved timesheets for the family's active placements. View only — for reference, not action |
| FR4.19 | Hours summary | Summary: hours this week, hours this month, by nanny if multiple placements |

#### Activity Tab

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR4.20 | Activity log | Chronological feed of all interactions: notes, status changes, placements, contract activity, messages sent/received |
| FR4.21 | Add note | Agency staff can add free-text notes |
| FR4.22 | Activity attribution | Each entry shows who and when |

---

### FR5: Placement Management
**Priority:** P0 (MVP)

**Design rationale:** Placements are the core unit of the agency's business — the connection between a nanny and a family. The placement page is where schedule, contract, timesheets, and both profiles converge.

#### Placement List

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.1 | Placement list view | All placements in a filterable list: nanny name, family name, status, start date, schedule summary, rate |
| FR5.2 | Status filter tabs | Filter tabs: **Active** · **Upcoming** · **Trial** · **Completed** · **All**. Default: Active |
| FR5.3 | Calendar/timeline view | Toggle to a timeline view showing all placements on a calendar. Visual blocks per nanny showing which days/times they're placed. Useful for spotting availability gaps and scheduling conflicts |

#### Creating a Placement

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.4 | Create placement | Link a nanny to a family with: start date, end date (if temp/trial), schedule, rate, terms, placement type |
| FR5.5 | Placement type | Types: **Permanent**, **Casual**, **Temporary**, **Trial**. Trial placements auto-flag for review at trial end date |
| FR5.6 | Rate structure | Support multiple rate types: hourly rate (default), daily flat rate, different rates for standard/evening/weekend hours. Rate displayed with type label |
| FR5.7 | Matching assistance | Filter available nannies by: availability, location, qualifications, preferences. Surface potential matches for a family's requirements |
| FR5.8 | Conflict detection | System warns if a nanny's proposed schedule overlaps with an existing active placement |

#### Placement Detail Page

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.9 | Placement header | Displays: nanny name + family name (both clickable to their profiles), status badge (Proposed / Confirmed / Active / Trial / Completed / Terminated), placement type badge, start date, end date |
| FR5.10 | Schedule section | Visual weekly schedule showing placement hours (Mon–Sun grid). Editable by agency. Shows: day, start time, end time, break, total hours per day, total hours per week |
| FR5.11 | Rate & terms section | Rate details: rate type, rate amount, any penalty/overtime rates configured. Terms: free-text notes on arrangement specifics |
| FR5.12 | Contract card | Linked contract with status badge. Quick actions: Generate Contract (if none), View Contract, Send for Signing. If no contract yet, prominent prompt to create one |
| FR5.13 | Timesheet summary | Recent timesheets for this placement. Hours this week / this month / total. Link to full timesheet list filtered to this placement |
| FR5.14 | Nanny card | Summary card: nanny photo, name, compliance indicator, phone, key qualifications. Click through to full nanny profile |
| FR5.15 | Family card | Summary card: family name, children summary (names + ages), address, phone. Click through to full family profile |
| FR5.16 | Placement notes | Free-text notes specific to this placement (e.g. "Family prefers pickup from school at 3pm on Wednesdays") |
| FR5.17 | Placement activity log | Chronological log: status changes, schedule modifications, contract events, timesheet submissions, notes added |

#### Placement Lifecycle

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR5.18 | Placement status flow | Statuses: Proposed → Confirmed → Active → Completed / Terminated. Trial placements: Proposed → Trial → Active → Completed / Terminated |
| FR5.19 | Trial review prompt | Trial placements surface a review prompt on the dashboard when trial end date is approaching (7 days before). Options: Convert to Permanent, Extend Trial, End Placement |
| FR5.20 | Placement history | Full history of all placements for both nannies and families, accessible from their respective profile pages |

---

### FR6: Nanny Recruitment Pipeline
**Priority:** P0 (MVP)

**Design rationale:** The pipeline is a recruitment funnel, not a contact list. Nannies live in the People directory (FR2); the pipeline tracks their journey from enquiry to active. Stages advance when real actions are completed — not by manual drag. This ensures data quality and compliance.

#### Pipeline View

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.1 | Pipeline board | Kanban-style board showing nannies grouped by stage: **Enquiry** → **Application** → **Interview** → **Reference Check** → **Onboarding** → **Active** |
| FR6.2 | Stage counts | Each column shows the count of nannies in that stage |
| FR6.3 | Nanny cards | Each card shows: name, photo/initials, days in current stage, completion indicator (how many stage requirements are met) |
| FR6.4 | Click to profile | Clicking a pipeline card opens the nanny's full profile page |
| FR6.5 | Stale indicator | Cards in a stage for longer than a configurable threshold (default: 14 days) show a visual "stale" indicator. Stale nannies also surface on the dashboard attention panel |

#### Action-Driven Stage Progression

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.6 | Stage requirements | Each pipeline stage has defined requirements that must be completed before advancing. Requirements are visible on the nanny's profile as a checklist |
| FR6.7 | Enquiry → Application | Advances when: application form is completed (either via public intake form or manually entered by agency). Required data: personal details, qualifications, availability |
| FR6.8 | Application → Interview | Advances when: interview is scheduled AND interview notes are recorded on the nanny's profile. Required: interview date, interviewer name, interview notes (structured or free-text) |
| FR6.9 | Interview → Reference Check | Advances when: at least 2 reference checks are captured. Each reference: referee name, relationship, contact details, reference notes, outcome (positive/concerns/declined) |
| FR6.10 | Reference Check → Onboarding | Advances when: all reference checks have positive outcomes AND agency staff confirms advancement. Gate: manual approval by coordinator/admin |
| FR6.11 | Onboarding → Active | Advances when: all required documents are uploaded and verified (WWCC, First Aid, Police Check at minimum), onboarding checklist is 100% complete, nanny has been invited to portal |
| FR6.12 | Advancement prompt | When all stage requirements are met, the nanny's profile shows a prominent "Ready to advance to [next stage]" prompt. Agency staff confirms to advance |
| FR6.13 | Manual override | Agency staff with Admin+ role can manually advance or revert a nanny's stage with a required reason note. Override logged in activity |
| FR6.14 | Stage history | Full history of stage transitions: from, to, date, triggered by (action or manual override), who confirmed |

#### Pipeline Filters & Search

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR6.15 | Pipeline filters | Filter pipeline by: assigned coordinator, tags, date range (entered pipeline), stale only |
| FR6.16 | Pipeline search | Search nannies within the pipeline by name |

---

### FR7: Contract Management
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR7.1 | Contract templates | Agency can create and manage contract templates with merge fields |
| FR7.2 | Contract generation | Generate contract from template, auto-populated with nanny/family/placement data |
| FR7.3 | Contract tracking | Track status: Draft → Sent → Signed → Active → Expired / Terminated |
| FR7.4 | Document storage | Generated contracts stored against the relevant placement, nanny, and family records |
| FR7.5 | AU compliance fields | Templates support AU-specific fields: Fair Work info, award rates, NES entitlements, notice periods |

---

### FR8: Timesheets
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR8.1 | Nanny timesheet submission | Nanny submits: date, start time, end time, break, placement, notes |
| FR8.2 | Approval workflow | Submitted → Agency Review → Approved / Rejected (with reason) |
| FR8.3 | Family FYI view | Family can see approved timesheets for their placement. View only — no action required unless flagged |
| FR8.4 | Timesheet summary | Agency dashboard: weekly/monthly summary per nanny, per placement |
| FR8.5 | Overtime/penalty rate flags | System flags hours that may attract overtime or penalty rates under AU awards |

---

### FR9: Onboarding
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR9.1 | Onboarding checklists | Configurable checklist per nanny: documents to collect, forms to complete, training to do |
| FR9.2 | Onboarding progress | Agency can see onboarding completion % per nanny |
| FR9.3 | Nanny self-service onboarding | Nanny can complete onboarding steps from their portal (upload docs, fill forms) |

---

### FR10: Team & Multi-user
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR10.1 | Team management | Agency owner can invite team members, assign roles |
| FR10.2 | Role-based permissions | Access controlled by role (Owner, Admin, Coordinator) |
| FR10.3 | Activity attribution | All actions logged with which team member performed them |

---

### FR11: Authentication & Tenant
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR11.1 | Agency registration | New agency can sign up, set up their account, add branding |
| FR11.2 | Multi-tenant architecture | Each agency's data is fully isolated |
| FR11.3 | Auth for all user types | Agency staff, nannies, and families all have separate login flows |
| FR11.4 | Invite-based access | Nannies and families are invited by the agency (not self-registration) |

---

### FR12: Form UX & Data Entry
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR12.1 | Multi-step wizard pattern | All complex forms (nanny profile, family profile, placement creation) use a step-by-step wizard with progress indicator. Max 4-6 fields visible per step |
| FR12.2 | Select over input | Where a finite set of options exists, use select/dropdown/toggle/radio — not free text. Examples: qualifications, availability days, suburb, care type, certification type |
| FR12.3 | Smart defaults and presets | Common values pre-selected where sensible. Example: break = 30min, start time = 8:00am, standard availability = Mon-Fri |
| FR12.4 | Save as draft | Partially completed forms save automatically. Users can return and finish later |
| FR12.5 | Inline validation | Validation feedback appears inline as fields are completed — not on submit. Clear error messages with fix suggestions |
| FR12.6 | Minimal required fields | Only fields essential to create the record are required. Everything else is optional and can be added later |
| FR12.7 | Mobile-optimised forms | All forms work on mobile. Large touch targets (44px min). Single-column layout. Appropriate keyboard types (tel, email, date) |
| FR12.8 | Contextual help | Complex or ambiguous fields include a short help text or tooltip. Example: "WWCC number format: VIC-XXXXXXX" |

**Form UX Principles:**
1. **Prefer selection over typing** — dropdowns, toggles, chips, radio groups
2. **Progressive disclosure** — show only what is needed at each step
3. **Forgiving** — save progress, allow skipping optional sections
4. **Fast path** — common scenarios take the fewest steps

---

### FR13: Messaging & Notifications
**Priority:** P0 (MVP)

**Design rationale:** Agencies need to communicate with nannies and families directly from the platform. This replaces scattered email/SMS/WhatsApp threads with a centralised, logged communication system. Every message is recorded in the contact's activity log.

#### In-App Notifications

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR13.1 | Notification bell | Persistent notification icon in the app header showing unread count. Clicking opens a notification dropdown/panel |
| FR13.2 | Notification list | List of notifications: document expiring, timesheet submitted, contract signed, pipeline stage change, message received. Each notification links to the relevant record |
| FR13.3 | Read/unread state | Notifications can be marked as read individually or "mark all as read" |
| FR13.4 | Notification preferences | Agency staff can configure which notification types they receive (per user, in settings) |

#### Sending Messages

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR13.5 | Send message to individual | From any nanny or family profile, agency can compose and send a message. Message delivered via the contact's preferred channel (email or SMS). Message logged in the contact's activity log |
| FR13.6 | Message composer | Rich-text composer with: subject line (email only), message body, optional attachment. Templates available for common messages (e.g. "Welcome", "Document reminder", "Timesheet overdue") |
| FR13.7 | Message templates | Agency can create and manage reusable message templates with merge fields (e.g. {{first_name}}, {{placement_start_date}}). Templates categorised by type |
| FR13.8 | Delivery channel | Messages sent via email (default) or SMS (if phone number available and SMS enabled). Channel selected automatically based on contact's communication preference, or manually by sender |

#### Bulk Messaging

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR13.9 | Bulk send from People page | Select multiple contacts from the People directory → "Send Message" bulk action. Opens the message composer with recipient list. Merge fields personalise each message |
| FR13.10 | Recipient filtering | Bulk message recipients can be filtered by: type (all nannies, all families), tags, status, placement status. Preview recipient count before sending |
| FR13.11 | Bulk send confirmation | Before sending, show: recipient count, message preview (with sample merge field values), delivery channel breakdown (X via email, Y via SMS). Require explicit confirmation |
| FR13.12 | Bulk send logging | Each bulk message logged in every recipient's activity log as an individual message. Bulk send also logged in a central message history for the agency |

#### Message History

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR13.13 | Contact message history | Each contact's activity tab shows all messages sent to them: date, subject/preview, delivery channel, status (sent/delivered/failed) |
| FR13.14 | Agency message log | Central message log (accessible from Settings or a dedicated Messages section) showing all messages sent by the agency: date, sender (staff member), recipients, subject, status |

#### Email Notifications for Critical Items

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR13.15 | Critical email alerts | System sends email alerts to relevant agency staff for critical events: document expired (WWCC, First Aid, Police Check), contract unsigned after 7 days, timesheet unapproved after 3 days |
| FR13.16 | Alert routing | Alerts sent to: the coordinator assigned to the nanny/family (if assigned), or all admins/owners if no coordinator assigned |

---

### FR14: Public Intake Forms (Agency-Branded)
**Priority:** P0 (MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR14.1 | Public nanny application form | Agency has a unique URL (e.g. app.nannyCRM.com/apply/little-stars) that nannies can access without logging in. Captures: personal details, qualifications, availability, preferences. Submits directly into the CRM as a new nanny contact in "Enquiry" pipeline stage |
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
👥 People            → Unified directory (All / Nannies / Families / Other)
🔄 Pipeline          → Nanny recruitment funnel (action-driven stages)
📋 Placements        → Active placements, calendar view, matching, history
📄 Contracts         → Templates, generated contracts, tracking
⏱️ Timesheets        → Submissions, approvals, summaries
⚙️ Settings          → Agency branding, team, templates, notification preferences, message templates
```

**Key design decisions:**
- **People** is the directory of all contacts. Click through to profiles.
- **Pipeline** is a separate nav item tracking the nanny recruitment funnel. Pipeline stages advance via completed actions, not manual drag.
- **Placements** has both list and calendar/timeline views.
- **Global search** (⌘K) is accessible from any page via the header.

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

### Flow 1: Agency onboards a new nanny (pipeline-driven)
```
Nanny submits public application form →
Appears in Pipeline at "Enquiry" stage →
Agency reviews application → records interview notes →
Pipeline advances to "Interview" →
Agency captures reference checks (2+ with outcomes) →
Pipeline advances to "Reference Check" →
References positive → agency confirms advancement →
Pipeline advances to "Onboarding" →
Nanny invited to portal → completes onboarding (uploads docs, fills profile) →
All docs verified + checklist complete →
Pipeline advances to "Active" → Nanny ready for placement
```

### Flow 2: Agency places a nanny with a family
```
Family registered with requirements (via People → Add → Family) →
Agency opens family's Requirements tab → "Find Matching Nannies" →
Match proposed → Placement created (nanny + family + schedule + rate + type) →
Contract generated from template → Contract sent for signing →
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
Family invited by agency → Sets up profile →
Views placement details + nanny info →
Receives FYI timesheet summaries →
Only prompted when: contract signing, issue flagged, feedback requested
```

### Flow 5: Agency coordinator daily workflow
```
Opens Dashboard → Reviews attention items (expiring docs, pending timesheets, stale pipeline cards) →
Clicks through to resolve → Checks activity feed for updates →
Checks Pipeline → advances nannies with completed requirements →
Navigates to People for ad-hoc lookups →
Reviews Placements → checks upcoming trial reviews →
Reviews Timesheets → approves pending → Done
```

### Flow 6: Agency sends bulk update
```
Agency navigates to People → Filters by tag "active-nannies" →
Selects all → Bulk action: Send Message →
Chooses template "Holiday hours update" → previews with merge fields →
Confirms → messages sent via preferred channels →
Each message logged in recipient's activity
```

---

## Scope

### In Scope (MVP)
Everything in FR1–FR14 above.

### Out of Scope (MVP)
- Payroll integration (Employment Hero — post-MVP)
- Automated invoicing
- Background check API integration
- Training/certification tracking beyond document storage
- Mobile native app
- Advanced analytics/reporting
- International support
- Two-way messaging / chat (MVP is outbound only — replies come through normal email/SMS)

### Open Questions
- [ ] What award rates / employment classifications are most common for nannies in AU?
- [ ] Do agencies typically handle tax/super, or does that go through a payroll provider?
- [ ] What does the family onboarding look like in practice today? (Research needed)
- [ ] SMS provider preference? (Twilio is the default recommendation)

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

---

## Success Metrics

| Metric | Target | How Measured |
|--------|--------|--------------|
| Agency activation | Agency completes setup + adds first nanny within 7 days | Onboarding funnel tracking |
| Nanny adoption | 80% of invited nannies complete onboarding within 14 days | Onboarding completion rate |
| Timesheet submission | 90% of timesheets submitted on time | Submission tracking |
| Family satisfaction | Families rate experience 4+/5 | In-app feedback |
| Agency retention | 90% month-over-month retention | Subscription data |
| Pipeline velocity | Average time from Enquiry to Active < 21 days | Pipeline stage tracking |

---

## Dependencies

| Dependency | Type | Status | Risk |
|------------|------|--------|------|
| Supabase (DB, Auth, Storage) | External | Available | Low |
| Vercel (Hosting) | External | Available | Low |
| Resend (Email) | External | Available | Low |
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