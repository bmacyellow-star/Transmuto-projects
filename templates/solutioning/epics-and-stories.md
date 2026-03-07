# Epics & Stories: [Project Name]

> Created: [Date]
> Status: Draft | In Review | Approved
> Architecture: [Link to Architecture Doc]
> Author: Max 🚀

---

## Epic Overview

| # | Epic | Stories | Priority | Status |
|---|------|---------|----------|--------|
| E1 | | | P0 | Not Started |
| E2 | | | P0 | Not Started |
| E3 | | | P1 | Not Started |

---

## Epic 1: [Name]

_[Brief description of what this epic delivers]_

### Stories

#### S1.1: [Story Name]
**As a** [user type]
**I want to** [action]
**So that** [outcome]

**Acceptance Criteria:**
- [ ] _[Criteria 1]_
- [ ] _[Criteria 2]_

**Technical Notes:**
_[Implementation hints, dependencies, edge cases]_

**Estimate:** S / M / L
**Dependencies:** None | S1.x

---

#### S1.2: [Story Name]
**As a** [user type]
**I want to** [action]
**So that** [outcome]

**Acceptance Criteria:**
- [ ] _[Criteria 1]_
- [ ] _[Criteria 2]_

**Technical Notes:**
_[Implementation hints, dependencies, edge cases]_

**Estimate:** S / M / L
**Dependencies:** None | S1.x

---

## Epic 2: [Name]

_[Continue pattern...]_

---

## Dependency Map

```
S1.1 ──→ S1.2 ──→ S2.1
              ──→ S1.3
S2.2 (independent)
```

---

## Implementation Order

**Wave 1 (parallel):**
- S1.1, S2.2

**Wave 2 (parallel, depends on Wave 1):**
- S1.2, S1.3

**Wave 3:**
- S2.1

---

## Approval

- [ ] Stories cover all PRD requirements
- [ ] Acceptance criteria are testable
- [ ] Dependencies mapped
- [ ] Bmac approved
- [ ] Ready to proceed to Discuss → Build

> **Next step:** Discuss phase — capture implementation preferences before building.
