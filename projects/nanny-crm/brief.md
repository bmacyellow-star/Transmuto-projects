# Product Brief: Nanny Agency CRM

> Created: 2026-03-07
> Status: ✅ Approved
> Author: Max 🚀

---

## Problem Statement

Nanny agencies operate at the intersection of two demanding relationships — families who need reliable childcare, and nannies who need stable, well-managed employment. Most agencies today run on spreadsheets, email threads, and disconnected tools. This creates friction at every stage: recruitment is manual, contracts are inconsistent, onboarding is ad-hoc, timesheets are error-prone, and there's no single view of the business.

The result: agencies spend more time on admin than on the relationships that actually matter.

## Target Users

| User Type | Description | Key Need |
|-----------|-------------|----------|
| Agency Admin | Owner/manager running the agency | Single platform to manage all operations — nannies, families, placements, compliance |
| Agency Staff | Coordinators, recruiters (2+ staff typical) | Efficient workflows for recruitment, matching, and ongoing management |
| Nannies | Childcare professionals on the agency's books | Easy onboarding, clear contracts, simple timesheets, visibility into placements |
| Families | Parents seeking childcare | **Minimal friction** — most things handled for them, only surfaced when action needed |

## Product Philosophy

**For the agency:** A powerful operations platform — recruitment, contracts, placements, timesheets, contacts.

**For the family:** An invisible system. Timesheets are FYI only. Contracts are handled. The agency manages everything behind the scenes. Families only engage when something needs their attention. The goal is an autonomous system that sits behind the nanny agency and employment element.

**Key differentiator:** The family experience is seamless by design. Less is more.

## Success Criteria

- [ ] Agency can manage full nanny lifecycle (recruit → onboard → place → manage → offboard) in one platform
- [ ] Timesheets are digital with approval workflows (agency/nanny side); FYI view for families
- [ ] Contracts generated from templates using data captured in the system
- [ ] Families have a lightweight, minimal-friction experience
- [ ] Agency has a clear dashboard view of their business
- [ ] Contact list / CRM for managing all agency relationships
- [ ] Agency branding (logo, name) visible throughout the platform

## Assumptions

1. **Agencies currently use fragmented tools** (spreadsheets, email, paper) — Confidence: High
2. **Nannies and families will adopt a digital platform** if it's simple enough — Confidence: Medium
3. **Australia-first** — AU employment law, contracts, tax, Fair Work compliance — Confidence: ✅ Confirmed
4. **Agencies typically have 2+ staff** — multi-user/team support is a default requirement — Confidence: ✅ Confirmed
5. **Warm list of agencies available** for user research and early adoption — Confidence: ✅ Confirmed

## Constraints

- **Technical:** Must work well on mobile (nannies and families are on phones)
- **Market:** Australia-first (AU-specific employment law, awards, contracts)
- **Timeline:** TBD
- **Budget:** Lean — Supabase + Vercel stack
- **Regulatory:** Employment contracts and timesheets have legal requirements under AU Fair Work

## Business Model

- **Pricing:** Per-agency per month (SaaS)
- **Tiers:** Likely 2-3 tiers based on scale (details TBC)
- **Revenue model:** Subscription — agency pays, nannies and families use for free

## Competitive Landscape

| Solution | What it does well | Where it falls short |
|----------|-------------------|---------------------|
| Generic CRMs (HubSpot, Salesforce) | Powerful, flexible | Not built for agency-specific workflows (placements, timesheets, contracts) |
| Recruitment software (JobAdder, Bullhorn) | Good at recruitment pipeline | Weak on ongoing employment management, timesheets |
| Payroll/HR tools (Employment Hero, Xero) | Timesheets, payroll | No recruitment, no family management, no placement matching |
| Nanny-specific platforms (various) | Some handle matching | Usually marketplace-focused, not agency operations |
| Spreadsheets + email | Free, flexible | No automation, no visibility, error-prone, doesn't scale |

**Gap:** No single platform handles the full nanny agency lifecycle while keeping the family experience effortless.

## Scope

**MVP:**
- Agency dashboard (overview of nannies, families, placements)
- **Contact list / CRM** — centralised directory of all contacts with notes, tags, activity history
- Nanny profiles and recruitment pipeline
- Family profiles and requirements
- Placement matching (nanny ↔ family)
- **Contract generation from templates** (using data captured in system)
- Digital timesheets with approval workflow (agency/nanny); FYI view for families
- Basic onboarding checklists
- Nanny portal (profile, timesheets, documents)
- Family portal (lightweight — placement info, FYI timesheets, only action items when needed)
- **Team support** — multi-user with roles/permissions
- **Agency branding** — logo at top of UI, agency name in family-facing touchpoints

**Post-MVP:**
- Employment Hero integration (payroll)
- Automated invoicing
- Background check integration
- Training/certification tracking
- Advanced reporting and analytics
- Deeper white-labelling / customisation

**Out of scope:**
- Mobile native app (responsive web first)
- Multi-agency / marketplace features
- International expansion

## Product Name

🔄 TBD — see suggestions in discussion. Bmac to decide.

---

## Approval

- [x] Bmac reviewed
- [x] All questions answered
- [x] Scope agreed
- [x] Ready to proceed to PRD ✅

> **Next step:** PRD creation
