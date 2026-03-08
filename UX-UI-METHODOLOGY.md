# UX/UI Design Methodology 🎨

> Part of the Transmuto Ways of Working
> Created: 2026-03-08
> Status: Draft — awaiting Bmac's review

---

## Philosophy

Every Transmuto product should feel **modern, minimal, and effortless**. Design isn't a phase bolted on — it's woven through the entire pipeline. The goal: products that look like they were designed by a boutique studio, built with the speed of AI-assisted execution.

**Design principles:**

1. **Minimal by default** — every element earns its place
2. **Whitespace is a feature** — let the UI breathe
3. **Consistent, not uniform** — shared design system, project-specific personality
4. **Motion with purpose** — subtle animations that guide, never distract
5. **Mobile-first, always** — responsive isn't optional

---

## Where Design Lives in the Pipeline

```
IDEA → BRIEF → PRD → DESIGN DIRECTION → ARCHITECTURE → STORIES → DISCUSS → BUILD → VERIFY → SHIP
                         ↑ NEW PHASE
```

### Design Direction Phase (between PRD and Architecture)

This is the new addition. After the PRD is approved and before architecture decisions lock:

1. **Inspiration & Moodboard** — visual research
2. **Design System Selection** — component library + tokens
3. **Key Screen Wireframes** — layout decisions for critical flows
4. **Design Review Gate** — Bmac approves the visual direction

This prevents the classic problem: architecture gets locked, stories get written, then everyone realises nobody thought about how it should actually look and feel.

---

## Step 1: Inspiration & Moodboard

### What
A curated collection of visual references that define the product's look and feel. Not pixel-perfect mockups — directional mood.

### How

**Sources to mine:**
- [Dribbble](https://dribbble.com) — UI patterns, visual style
- [Mobbin](https://mobbin.com) — real app screenshots, flow patterns
- [Godly](https://godly.website) — modern web design inspiration
- [Minimal Gallery](https://minimal.gallery) — minimal design showcase
- [Awwwards](https://awwwards.com) — cutting-edge web design
- [SaaS Interface](https://saasinterface.com) — SaaS-specific patterns
- Competitor/adjacent product screenshots

**Capture format:**
Create `docs/design/moodboard.md` in each project repo:

```markdown
# Moodboard: [Project Name]

## Visual Direction
[2-3 sentence summary of target aesthetic]

## References
| Reference | What We Like | Link/Screenshot |
|-----------|-------------|-----------------|
| Linear    | Navigation, density balance | [link] |
| Notion    | Typography, whitespace | [link] |
| ...       | ... | ... |

## Colour Mood
- Preference: [light/dark/adaptive]
- Accent energy: [bold/subtle/muted]
- Examples: [colour chips or references]

## Typography Mood
- Feel: [geometric/humanist/monospace/mixed]
- Density: [airy/moderate/compact]

## Interaction Mood
- Transitions: [snappy/smooth/playful]
- Feedback: [subtle/explicit]
```

### Agent Execution
Max can compile moodboards by:
- Searching design sites for relevant references
- Pulling screenshots from competitor products
- Generating mood descriptions based on product brief
- Presenting options for Bmac to react to

---

## Step 2: Design System Selection

### The Stack

Every Transmuto project starts from a **pre-built component library** and customises via design tokens. We don't hand-build buttons.

**Recommended component libraries (React):**

| Library | Best For | Style |
|---------|----------|-------|
| **shadcn/ui** | Most projects — our default | Minimal, composable, owns the code |
| **Radix UI** | Accessible primitives | Unstyled, maximum control |
| **NextUI** | Quick polish, modern feel | Opinionated, beautiful defaults |
| **Tremor** | Dashboards, data-heavy UIs | Clean data viz components |
| **Park UI** | shadcn alternative w/ Ark | Multiple CSS framework support |

**Default recommendation: shadcn/ui + Tailwind CSS + Radix primitives**

Why:
- You own the code (copy-paste, not dependency)
- Tailwind means tokens are just CSS variables
- Radix handles accessibility
- Massive ecosystem (themes, extensions, blocks)
- AI agents generate Tailwind fluently

### Design Tokens

Each project defines tokens in `tailwind.config.ts` (or CSS variables):

```
colours/        → brand, neutral, semantic (success/warning/error)
typography/     → font families, scale, weights, line heights
spacing/        → consistent spacing scale
radii/          → border radius scale
shadows/        → elevation scale
motion/         → transition durations, easings
```

**Token file:** `docs/design/tokens.md` — human-readable reference
**Implementation:** `tailwind.config.ts` or `globals.css`

### Pre-Built Themes & Blocks

Speed boosters:
- [shadcn/ui themes](https://ui.shadcn.com/themes) — pre-configured colour palettes
- [shadcn/ui blocks](https://ui.shadcn.com/blocks) — full page layouts (dashboard, auth, settings)
- [v0.dev](https://v0.dev) — AI-generated shadcn components from prompts
- [magicui.design](https://magicui.design) — animated components for shadcn
- [aceternity UI](https://ui.aceternity.com) — modern animated components
- [cult/ui](https://www.cult-ui.com) — experimental shadcn components

---

## Step 3: Figma Integration

### Role of Figma

Figma is used for **key decisions, not comprehensive specs**. We're not designing every screen in Figma before building — that's waterfall. Instead:

**Use Figma for:**
- Moodboards (visual, shareable)
- Key screen layouts (3-5 critical screens per project)
- Component exploration (when a pattern isn't obvious)
- Design review with Bmac

**Don't use Figma for:**
- Every screen in detail (code is the source of truth)
- Pixel-perfect handoff docs (agents build from descriptions + tokens)
- Maintaining a parallel design system (tokens live in code)

### Figma MCP Integration

The Figma MCP (Model Context Protocol) server lets agents read Figma files directly:

**What it enables:**
- Agent reads a Figma frame → understands layout, spacing, colours
- Agent translates Figma designs into code using the project's design system
- Design-to-code with awareness of your actual component library

**Setup:**
```json
// MCP server config
{
  "figma": {
    "command": "npx",
    "args": ["-y", "figma-developer-mcp", "--stdio"],
    "env": {
      "FIGMA_API_KEY": "<key>"
    }
  }
}
```

**Workflow:**
1. Bmac creates/approves key screen layouts in Figma
2. Max reads the Figma file via MCP
3. Coding agent receives: Figma context + design tokens + component library reference
4. Agent builds the screen using real shadcn/Tailwind components
5. Result: code that matches the design intent, not a pixel-push

### Figma Templates

Maintain a shared Figma file with:
- Transmuto colour palettes (matching Tailwind tokens)
- Typography scale
- Common layout patterns
- Device frames for key breakpoints

---

## Step 4: Design Direction Document

Each project gets a `docs/design/design-direction.md` that captures decisions:

```markdown
# Design Direction: [Project Name]

> Status: Draft | Approved
> Approved by: Bmac on [date]

## Visual Summary
[2-3 sentences: what does this product look and feel like?]

## Moodboard
[Link to moodboard.md or Figma board]

## Design System
- **Component library:** shadcn/ui
- **CSS framework:** Tailwind CSS
- **Theme base:** [chosen theme or custom]
- **Key tokens:** [link to tokens.md]

## Layout Decisions
- **Navigation:** [sidebar/topbar/bottom-tabs/contextual]
- **Page structure:** [single-column/two-column/dashboard grid]
- **Density:** [spacious/balanced/compact]
- **Responsive strategy:** [mobile-first breakpoints]

## Key Screens
| Screen | Description | Wireframe |
|--------|-------------|-----------|
| Dashboard | Primary landing view | [Figma link / ASCII wireframe] |
| [Screen 2] | ... | ... |

## Typography
- **Headings:** [font]
- **Body:** [font]
- **Mono:** [font, if needed]
- **Scale:** [reference]

## Colour
- **Mode:** Light / Dark / Both
- **Primary:** [colour + usage]
- **Neutral:** [palette approach]
- **Accent:** [colour + usage]
- **Semantic:** [success/warning/error approach]

## Motion & Interaction
- **Page transitions:** [approach]
- **Micro-interactions:** [approach]
- **Loading states:** [skeletons/spinners/shimmer]

## Iconography
- **Library:** [Lucide (shadcn default) / Phosphor / custom]
- **Style:** [outline/filled/duotone]
```

---

## Agent Execution: How Design Gets Built

### During Discuss Phase

Design decisions feed into the Discuss phase context doc. For each epic/story involving UI:

- Reference the Design Direction doc
- Specify which components from the design system to use
- Include Figma frame links for complex layouts
- Note any custom patterns not covered by the library

### During Execute Phase

Each coding agent receives:
1. **Task context** (from GSD plan)
2. **Design system reference** (component library + tokens)
3. **Design direction** (relevant section of design-direction.md)
4. **Figma context** (via MCP, if applicable)

**Agent prompt pattern for UI tasks:**
```
Build [feature]. 

Design system: shadcn/ui + Tailwind.
Design direction: [paste relevant section]
Tokens: [paste or reference tokens file]
Figma reference: [link, if available]
Components to use: [specific shadcn components]

Requirements:
- Mobile-first responsive
- Follow existing patterns in the codebase
- Use design tokens, don't hardcode colours/spacing
```

### Design QA in Verify Phase

Verification now includes design checks:
- [ ] Matches design direction (layout, spacing, colour)
- [ ] Responsive at mobile/tablet/desktop breakpoints
- [ ] Design tokens used (no hardcoded values)
- [ ] Consistent with existing screens
- [ ] Interactions feel smooth
- [ ] Loading/empty/error states handled
- [ ] Dark mode works (if applicable)

---

## Toolchain Summary

| Tool | Role | When |
|------|------|------|
| **Dribbble/Mobbin/Godly** | Inspiration hunting | Moodboard phase |
| **Figma** | Key screen layouts, moodboards | Design Direction phase |
| **Figma MCP** | Agent reads Figma designs | Execute phase |
| **shadcn/ui** | Component library (default) | Build time |
| **Tailwind CSS** | Styling + design tokens | Build time |
| **v0.dev** | AI component generation | Prototyping, complex components |
| **Storybook** | Component isolation/testing | Optional, for complex systems |

---

## Templates

- `docs/design/moodboard.md` — Visual inspiration board
- `docs/design/design-direction.md` — Approved design decisions
- `docs/design/tokens.md` — Design token reference
- Architecture template updated to reference design direction

---

## Approval Gate

**Design Direction** becomes a gate between PRD and Architecture:

```
BRIEF → PRD → DESIGN DIRECTION ✋ → ARCHITECTURE → STORIES → ...
```

Bmac approves the visual direction before we lock architecture and write stories. This ensures tech decisions support design intent (e.g., choosing Next.js for image optimisation, or adding animation libraries to the stack).

---

_This methodology evolves. As we ship products and learn what works, we'll refine it._
