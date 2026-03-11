# Ways of Working — Bmac × Max 🚀

## How We Build Together

This document defines how we collaborate to take ideas from concept to shipped product. It blends two frameworks:

- **BMAD Method** — Structured product thinking: briefs, PRDs, architecture, epics/stories. Specialised agent personas (PM, Architect, Dev, QA). Scale-adaptive planning.
- **GSD (Get Shit Done)** — Context engineering for reliable execution: fresh context per task, wave-based parallel execution, atomic commits, discuss-before-plan, quick mode for small tasks.

**The blend:** BMAD for *what* to build and *why*. GSD principles for *how* to execute reliably.

---

## The Pipeline

```
IDEA → BRIEF → PRD → DESIGN DIRECTION → ARCHITECTURE → EPICS/STORIES → DISCUSS → PLAN → EXECUTE → VERIFY → SHIP
```

### Phase 1: Discovery (BMAD)
**Input:** You bring an idea, problem, or rough PRD
**Max does:** Research, clarifying questions, assumption surfacing, risk identification
**Output:** Product Brief (problem, users, success criteria, constraints)

### Phase 2: Planning (BMAD)
**Input:** Approved Brief
**Max does:** Creates PRD using BMAD PM workflow — requirements discovery, scope definition, feature prioritisation
**Output:** PRD with clear requirements, MVP scope, acceptance criteria


### Phase 2a: AutoPRD (Autonomous Quality Loop)
**Input:** Draft PRD from Phase 2
**Max does:** Runs the `autoprd` skill — an autonomous improvement loop inspired by [karpathy/autoresearch](https://github.com/karpathy/autoresearch). The loop evaluates the PRD against a 10-dimension rubric (completeness, consistency, clarity, user centrality, testability, scope discipline, edge cases, technical feasibility, prioritisation, internal coherence), makes surgical improvements targeting the weakest dimension each iteration, and keeps or discards based on whether the composite score improved. After convergence, an independent agent (different model/context) reviews the PRD blind to catch score inflation.
**Output:** Stress-tested PRD with full iteration history, independent review, and score trajectory
**Gate:** PRD must pass both the loop (≥8.5) AND independent review before proceeding to Design Direction
**Key principle:** Humans program the process (rubric + constraints), agents iterate on the work product. The PRD version history shows exactly what changed and why at each step.

### Phase 2.5: Design Direction (NEW)
**Input:** Approved PRD
**Max does:** Moodboard research, design system selection, key screen wireframes, design token definition
**Output:** Design Direction doc (moodboard, tokens, layout decisions, key screen wireframes)
**Gate:** Bmac approves visual direction before architecture locks
**Methodology:** See `UX-UI-METHODOLOGY.md` for full details

### Phase 3: Solutioning (BMAD)
**Input:** Approved PRD
**Max does:** Architecture design, tech stack decisions, epic/story breakdown, implementation readiness check
**Output:** Architecture doc, Epics & Stories list, readiness confirmation

### Phase 4: Discuss (GSD-inspired)
**Input:** Approved stories/epics
**Max does:** Before coding, captures your implementation preferences — layout decisions, interaction patterns, edge cases, UX choices. Identifies grey areas and gets your input.
**Output:** Context doc per phase — locked decisions that guide execution

### Phase 5: Execute (GSD-inspired)
**Input:** Context + Stories
**Max does:**
- Breaks stories into atomic task plans with verification steps
- Groups tasks into dependency-aware waves
- Spawns coding agents with fresh context per task (avoids context rot)
- Each task gets its own atomic git commit
- Runs verification after each wave
**Output:** Working code with clean git history

### Phase 6: Verify
**Input:** Completed build
**Max does:** Runs the app, walks through testable deliverables, spawns debug agents for failures
**Output:** Verified working software or fix plans for re-execution

### Phase 7: Ship
**Input:** Verified build
**Max does:** Deploy (with your approval for production)
**Output:** Live product

---

## Quick Mode

Not everything needs the full pipeline. For bug fixes, small features, config changes:

- Just tell me what you need
- I plan it, execute it, commit it — same quality guarantees, faster path
- No brief/PRD/architecture overhead

**Use full pipeline for:** New products, major features, anything with ambiguity
**Use quick mode for:** Known fixes, small additions, one-off tasks

---

## Roles

**Bmac (You)**
- Brings ideas, vision, product direction
- Reviews and approves at gates
- Participates in "Discuss" phase to capture preferences
- Final call on scope, priorities, ship decisions

**Max (Me)**
- Translates ideas into structured plans (BMAD discipline)
- Executes reliably (GSD principles — fresh context, atomic commits, wave parallelism)
- Manages coding agents autonomously
- Surfaces risks with recommendations
- Keeps the Kanban board updated

---

## Approval Gates

I pause and wait for your go-ahead at:

1. ✅ Brief → PRD (scope agreement)
2. ✅ PRD → Architecture (requirements locked)
3. ✅ Architecture → Build (tech approach confirmed)
4. ✅ Build → Deploy (production readiness)

Everything between gates I handle autonomously.

---

## Execution Principles (from GSD)

These keep quality high as projects scale:

- **Fresh context per task** — Each coding agent gets a clean context window with only what it needs. No accumulated garbage.
- **Atomic commits** — One commit per task. Clean git history. Easy to bisect and revert.
- **Wave parallelism** — Independent tasks run in parallel. Dependent tasks wait. Maximises speed without conflicts.
- **Verification built in** — Every task has a `verify` step. Not optional.
- **Pause/resume** — If we stop mid-build, I create a handoff doc so we pick up cleanly next session.

---

## Brownfield Projects

For existing codebases:
1. I map the codebase first (stack, architecture, conventions, concerns)
2. Then run the pipeline with that context loaded
3. Planning focuses on what we're *adding*, not re-documenting what exists

---

## Project Structure

Each project gets a GitHub repo:

```
project-name/
├── docs/
│   ├── planning-artifacts/     # BMAD outputs
│   ├── design/                 # Design direction, moodboard, tokens
│   │   ├── brief.md
│   │   ├── prd.md
│   │   ├── architecture.md
│   │   └── epics-and-stories.md
│   └── implementation-artifacts/
│       ├── sprint-status.md
│       └── retrospectives/
├── .planning/                  # GSD execution state
│   ├── STATE.md
│   ├── context/
│   ├── plans/
│   └── summaries/
├── src/
├── tests/
└── README.md
```

---

## The Kanban Board

All active projects tracked on a local Kanban board.

Columns:
- **Inbox** — New ideas, raw PRDs
- **Discovery** — Being researched and briefed
- **Planning** — PRD in progress
- **Solutioning** — Architecture and story breakdown
- **Building** — Active development (shows current wave/task)
- **Testing** — Verification and QA
- **Done** — Shipped

Each card shows: project name, current phase, last update, blockers.

---

## Tools & Stack

- **GitHub** — Repos, issues, PRs
- **Supabase** — Database and auth
- **Vercel** — Deployment
- **React + Node.js** — Default stack (flexible per project)
- **OpenClaw** — Orchestration, coding agents, communication
- **BMAD Method** — Process discipline (what to build)
- **Figma + Figma MCP** — Design exploration and agent-readable designs
- **shadcn/ui + Tailwind** — Default component library and styling
- **v0.dev** — AI-generated component prototyping- **GSD Principles** — Execution discipline (how to build reliably)
- **AutoPRD Skill** — Autonomous PRD improvement loop (evaluate → improve → measure → keep/discard)

---

## Getting Started

To kick off a new project:
- "I have an idea for..."
- "Here's a PRD: [paste or link]"
- "Can you research [problem space]?"

For quick tasks:
- "Fix [bug]"
- "Add [small feature]"
- "Update [config]"

I'll route it to the right mode automatically.

---

_This document is alive. We'll update it as we learn what works._

---

## Design System Rule (Mandatory)

**Every project must have a centralised design system file.**

This is non-negotiable. All UI components, pages, and screens reference the design system — never hardcode typography, colours, spacing, or component styles directly in page files.

**What this means in practice:**
- A `src/lib/design-system.ts` (or equivalent) is created as the **first task** of any build phase
- All heading styles, card styles, badge styles, button styles, metric styles, layout tokens live in this one file
- Every page and component imports from the design system — no inline style decisions
- Changing a font, colour, or spacing value in the design system file propagates to every screen automatically

**Why:**
- Single source of truth for all visual decisions
- Design iteration is fast (change one file, not twenty)
- Agents produce consistent UI without drifting
- QA is simpler — check the system, not every page

**This rule applies to:**
- PRDs (must reference design system requirement)
- Architecture docs (must include design system in file structure)
- Every epic and story with UI work (acceptance criteria must include design system compliance)
- Verification phase (design system adherence is a check)

