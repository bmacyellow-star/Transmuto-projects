# Product Brief: Nanny Agency CRM

> Created: 2026-03-07
> Status: Draft — Awaiting remaining answers
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
| Families | Parents seeking childcare | Transparent process, easy communication with agency, confidence in quality |

## Success Criteria

- [ ] Agency can manage full nanny lifecycle (recruit → onboard → place → manage → offboard) in one platform
- [ ] Timesheets are digital with approval workflows
- [ ] Contracts are generated and tracked within the system
- [ ] Families and nannies have self-service portals
- [ ] Agency has a clear dashboard view of their business
- [ ] Contact list / CRM functionality for managing all agency relationships

## Assumptions

1. **Agencies currently use fragmented tools** (spreadsheets, email, paper) — Confidence: High
2. **Nannies and families will adopt a digital platform** if it's simple enough — Confidence: Medium
3. **Australia-first** — AU employment law, contracts, tax, Fair Work compliance — Confidence: ✅ Confirmed
4. **Agencies typically have 2+ staff** — multi-user/team support is a default requirement — Confidence: ✅ Confirmed
5. **Timesheets need payroll integration eventually** but not for MVP — Confidence: Medium
6. **Warm list of agencies available** for user research and early adoption — Confidence: ✅ Confirmed

## Constraints

- **Technical:** Must work well on mobile (nannies and families are on phones)
- **Market:** Australia-first (AU-specific employment law, awards, contracts)
- **Timeline:** TBD
- **Budget:** Lean — Supabase + Vercel stack
- **Regulatory:** Employment contracts and timesheets have legal requirements under AU Fair Work
- **Other:** Must be white-label-able or at least agency-brandable

## Competitive Landscape

| Solution | What it does well | Where it falls short |
|----------|-------------------|---------------------|
| Generic CRMs (HubSpot, Salesforce) | Powerful, flexible | Not built for agency-specific workflows (placements, timesheets, contracts) |
| Recruitment software (JobAdder, Bullhorn) | Good at recruitment pipeline | Weak on ongoing employment management, timesheets |
| Payroll/HR tools (Employment Hero, Xero) | Timesheets, payroll | No recruitment, no family management, no placement matching |
| Nanny-specific platforms (various) | Some handle matching | Usually marketplace-focused, not agency operations |
| Spreadsheets + email | Free, flexible | No automation, no visibility, error-prone, doesn't scale |

**Gap:** No single platform handles the full nanny agency lifecycle — from recruiting a nanny, through onboarding and contracts, to ongoing placement management and timesheets, while also managing the family relationship and acting as a central contact hub.

## Initial Scope Thinking

**Probably in (MVP):**
- Agency dashboard (overview of nannies, families, placements)
- **Contact list / CRM** — centralised directory of all agency contacts (nannies, families, referrers, partners) with notes, tags, activity history
- Nanny profiles and recruitment pipeline
- Family profiles and requirements
- Placement matching (nanny ↔ family)
- Employment contract generation (templates)
- Digital timesheets with approval workflow
- Basic onboarding checklists
- Nanny self-service portal (profile, timesheets, documents)
- Family self-service portal (placement details, communication)
- **Team support** — multi-user with roles/permissions (admin, coordinator, etc.)

**Probably out (for now):**
- Payroll integration (Xero/MYOB — future)
- Automated invoicing
- Background check integration
- Training/certification tracking
- Mobile native app (responsive web first)
- Multi-agency / marketplace features
- Advanced reporting and analytics
- International expansion (different employment laws)

---

## Open Questions for Bmac

1. ~~**Target market:** Australia-first?~~ ✅ **Australia-first confirmed**
2. ~~**Agency size:**~~ ✅ **2+ staff typical, team support by default**
3. **Pricing model thinking:** Per-agency SaaS? Per-nanny? Free tier?
4. ~~**Domain expertise / access:**~~ ✅ **Warm list of agencies available for research**
5. **Contract templates:** Do we need to handle legal document generation, or just tracking?
6. **Timesheet → payroll:** Is integration with Xero/MYOB a near-term need or future?
7. **White-labelling:** Important for MVP or later?
8. ~~**Name:**~~ 🔄 **Open — see name suggestions below**

## Product Name Ideas 💡

The name should feel trustworthy, warm, and professional. Nanny agencies care about relationships — the name should reflect care + organisation.

| Name | Vibe | Notes |
|------|------|-------|
| **Kinder** | Warm, childcare-adjacent | German for "children" — simple, clean |
| **Tend** | Caring, active | "To tend to" — captures the caregiving + management angle |
| **Hive** | Organised, buzzing, community | Agency as the hive, nannies and families as the network |
| **Nestled** | Safe, home, belonging | Families nest, nannies help create that |
| **Cradl** | Nurturing, foundational | Evokes care from the start |
| **Placed** | Direct, functional | It's about placements — says what it does |
| **Mindi** | Friendly, approachable | Play on "minding" children — AU/UK term |
| **Kith** | Close relationships, community | "Kith and kin" — about connection |

Let me know if any resonate or if you want a different direction entirely.

---

## Approval

- [ ] Bmac reviewed
- [x] Key questions answered (market, agency size, access)
- [ ] Remaining questions answered (pricing, contracts, payroll, white-label, name)
- [ ] Scope agreed
- [ ] Ready to proceed to PRD

> **Next step:** Bmac answers remaining questions + picks a name direction, then we create the PRD.
