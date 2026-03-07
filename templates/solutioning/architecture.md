# Architecture: [Project Name]

> Created: [Date]
> Status: Draft | In Review | Approved
> PRD: [Link to PRD]
> Author: Max 🚀 (Architect lens)

---

## Tech Stack

| Layer | Technology | Rationale |
|-------|-----------|-----------|
| Frontend | | |
| Backend | | |
| Database | | |
| Auth | | |
| Hosting | | |
| CI/CD | | |

---

## System Architecture

### High-Level Diagram

```
[Client] → [API Layer] → [Business Logic] → [Data Layer]
                ↓
         [External Services]
```

_[Replace with actual architecture — keep it simple]_

### Key Components

| Component | Responsibility | Technology |
|-----------|---------------|-----------|
| | | |

---

## Data Model

### Core Entities

```
Entity: [Name]
├── id (uuid, PK)
├── field_1 (type)
├── field_2 (type)
├── created_at (timestamp)
└── updated_at (timestamp)
```

### Relationships
_[Describe key relationships between entities]_

---

## API Design

### Endpoints

| Method | Path | Purpose | Auth |
|--------|------|---------|------|
| GET | /api/v1/... | | Yes/No |
| POST | /api/v1/... | | Yes/No |

---

## Security

- **Authentication:** _[Approach]_
- **Authorization:** _[Approach]_
- **Data protection:** _[Approach]_
- **Secrets management:** _[Approach]_

---

## Infrastructure

- **Environments:** Dev → Staging → Production
- **Deployment:** _[Strategy — Vercel, etc.]_
- **Monitoring:** _[Approach]_
- **Error handling:** _[Approach]_

---

## Technical Decisions

| Decision | Options Considered | Choice | Why |
|----------|-------------------|--------|-----|
| | | | |

---

## Constraints & Trade-offs

_[What technical compromises are we making and why?]_

---

## Approval

- [ ] Stack confirmed
- [ ] Architecture reviewed
- [ ] Security approach agreed
- [ ] Bmac approved
- [ ] Ready to proceed to Epics & Stories

> **Next step:** Break down into Epics and Stories for implementation.
