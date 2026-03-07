# Product Brief: Nanny Agency CRM

> Created: 2026-03-07
> Status: Draft
> Author: Max 🚀

---

## Problem Statement

Nanny agencies operate at the intersection of two demanding relationships — families who need reliable childcare, and nannies who need stable, well-managed employment. Most agencies today run on spreadsheets, email threads, and disconnected tools. This creates friction at every stage: recruitment is manual, contracts are inconsistent, onboarding is ad-hoc, timesheets are error-prone, and there's no single view of the business.

The result: agencies spend more time on admin than on the relationships that actually matter.

## Target Users

| User Type | Description | Key Need |
|-----------|-------------|----------|
| Agency Admin | Owner/manager running the agency | Single platform to manage all operations — nannies, families, placements, compliance |
| Agency Staff | Coordinators, recruiters | Efficient workflows for recruitment, matching, and ongoing management |
| Nannies | Childcare professionals on the agency's books | Easy onboarding, clear contracts, simple timesheets, visibility into placements |
| Families | Parents seeking childcare | Transparent process, easy communication with agency, confidence in quality |

## Success Criteria

- [ ] Agency can manage full nanny lifecycle (recruit → onboard → place → manage → offboard) in one platform
- [ ] Timesheets are digital with approval workflows
- [ ] Contracts are generated and tracked within the system
- [ ] Families and nannies have self-service portals
- [ ] Agency has a clear dashboard view of their business

## Assumptions

1. **Agencies currently use fragmented tools** (spreadsheets, email, paper) — Confidence: High
2. **Nannies and families will adopt a digital platform** if it's simple enough — Confidence: Medium
3. **Australian market first** (employment law, contracts, tax implications are AU-specific) — Confidence: Medium (need to confirm with Bmac)
4. **Agencies range from solo operators to 50+ staff** — Confidence: Medium
5. **Timesheets need payroll integration eventually** but not for MVP — Confidence: Medium

## Constraints

- **Technical:** Must work well on mobile (nannies and families are on phones)
- **Timeline:** TBD
- **Budget:** Lean — Supabase + Vercel stack
- **Regulatory:** Employment contracts and timesheets have legal requirements (jurisdiction-dependent)
- **Other:** Must be white-label-able or at least agency-brandable

## Competitive Landscape

| Solution | What it does well | Where it falls short |
|----------|-------------------|---------------------|
| Generic CRMs (HubSpot, Salesforce) | Powerful, flexible | Not built for agency-specific workflows (placements, timesheets, contracts) |
| Recruitment software (JobAdder, Bullhorn) | Good at recruitment pipeline | Weak on ongoing employment management, timesheets |
| Payroll/HR tools (Employment Hero, Xero) | Timesheets, payroll | No recruitment, no family management, no placement matching |
| Nanny-specific platforms (various) | Some handle matching | Usually marketplace-focused, not agency operations |
| Spreadsheets + email | Free, flexible | No automation, no visibility, error-prone, doesn't scale |

**Gap:** No single platform handles the full nanny agency lifecycle — from recruiting a nanny, through onboarding and contracts, to ongoing placement management and timesheets, while also managing the family relationship.

## Initial Scope Thinking

**Probably in (MVP):**
- Agency dashboard (overview of nannies, families, placements)
- Nanny profiles and recruitment pipeline
- Family profiles and requirements
- Placement matching (nanny ↔ family)
- Employment contract generation (templates)
- Digital timesheets with approval workflow
- Basic onboarding checklists
- Nanny self-service portal (profile, timesheets, documents)
- Family self-service portal (placement details, communication)

**Probably out (for now):**
- Payroll integration
- Automated invoicing
- Background check integration
- Training/certification tracking
- Mobile native app (responsive web first)
- Multi-agency / marketplace features
- Advanced reporting and analytics

---

## Open Questions for Bmac

1. **Target market:** Australia-first? Or broader from day one?
2. **Agency size:** Solo operators, small teams, or enterprise agencies? (Affects complexity)
3. **Pricing model thinking:** Per-agency SaaS? Per-nanny? Free tier?
4. **Do you have domain expertise here?** Access to an agency for user research?
5. **Contract templates:** Do we need to handle legal document generation, or just tracking?
6. **Timesheet → payroll:** Is integration with Xero/MYOB a near-term need or future?
7. **White-labelling:** Important for MVP or later?
8. **Name:** "Nanny Agency CRM" is descriptive but not a product name. Any ideas?

---

## Approval

- [ ] Bmac reviewed
- [ ] Open questions answered
- [ ] Scope agreed
- [ ] Ready to proceed to PRD

> **Next step:** Bmac reviews this brief, answers open questions, then we create the PRD.
