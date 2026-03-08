# New Project Checklist

Use this when kicking off a new project through the pipeline.

---

## Setup
- [ ] Create GitHub repo for the project
- [ ] Add project card to Kanban board (Inbox column)
- [ ] Create `docs/planning-artifacts/`, `docs/design/` and `docs/implementation-artifacts/` directories
- [ ] Create `.planning/` directory for execution state

## Phase 1: Discovery
- [ ] Complete [Product Brief](templates/discovery/product-brief.md)
- [ ] Bmac reviewed and approved brief
- [ ] Move card to Discovery column

## Phase 2: Planning
- [ ] Complete [PRD](templates/planning/prd.md)
- [ ] Requirements locked
- [ ] Bmac approved PRD
- [ ] Move card to Planning column

## Phase 2.5: Design Direction
- [ ] Complete [Moodboard](templates/design/moodboard.md)
- [ ] Select design system and component library
- [ ] Complete [Design Direction](templates/design/design-direction.md)
- [ ] Key screen wireframes created (Figma or inline)
- [ ] Design tokens defined
- [ ] Bmac approved design direction
## Phase 3: Solutioning
- [ ] Complete [Architecture](templates/solutioning/architecture.md)
- [ ] Complete [Epics & Stories](templates/solutioning/epics-and-stories.md)
- [ ] Implementation readiness confirmed
- [ ] Bmac approved architecture and stories
- [ ] Move card to Solutioning column

## Phase 4: Discuss
- [ ] Complete [Discuss Context](templates/implementation/discuss-context.md) for each epic/phase
- [ ] All grey areas resolved with Bmac
- [ ] Decisions locked

## Phase 5: Execute
- [ ] [Task Plans](templates/implementation/task-plan.md) created
- [ ] Waves defined and dependencies mapped
- [ ] Coding agents spawned
- [ ] All tasks complete with atomic commits
- [ ] Move card to Building column

## Phase 6: Verify
- [ ] Complete [Verification](templates/review/verification.md)
- [ ] All deliverables pass
- [ ] Bmac accepted
- [ ] Move card to Testing column

## Phase 7: Ship
- [ ] Deploy to production (Bmac approved)
- [ ] Complete [Retrospective](templates/review/retrospective.md)
- [ ] Move card to Done column
- [ ] Update WAYS-OF-WORKING.md with any process learnings
