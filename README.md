# Designer Agents (Cursor Skills)

A small suite of **Cursor project skills** for Senior Product Designers working on **UX/UI** and **design systems**.

These agents are optimized for **screenshots**, **Figma links/component names**, and **lightweight analytics**, and they output artifacts that are easy to paste into **Figma pages**, **Notion**, or **design-system docs**.

## Repository

- **GitHub**: `https://github.com/keg-flair/cursor-designer-agents`

## What’s in this repo

- **Skills (agents)**: `.cursor/skills/` — Cursor project skills (`.cursor/skills/<skill-name>/SKILL.md`)
- **Rules (always-on guidance)**: `.cursor/rules/` — persistent Cursor rules for consistent outputs
- **Skills (Claude Projects)**: `skills/` — tool-agnostic skills you can paste into a Claude Project
- **Commands (copy/paste prompts)**: `docs/COMMANDS.md`
- **Templates (fillable outlines)**: `docs/templates/`
- **Golden examples (reference outputs)**: `docs/examples/`
- **Docs index**: `docs/README.md`

## Quick start (Cursor, use in any repo)

1. Copy this repo’s `.cursor/` folder into your product/design repo (includes **skills** under `.cursor/skills/` and **rules** under `.cursor/rules/`).
2. Optional: bookmark `docs/COMMANDS.md`, keep `docs/templates/` handy, and skim `docs/examples/` for output shape.
3. In Cursor, ask a task in plain language and attach screenshots/links/metrics as needed.

Example prompts:
- “Audit this onboarding flow for friction. Prioritize P0/P1 issues and propose fixes.”
- “Write a component spec for `Button` with variants, states, token hooks, and QA checklist.”
- “Synthesize these interviews into themes, insights, and opportunities.”
- “Given this funnel drop-off, propose UX hypotheses and what to measure next.”

## Quick start (Claude Projects)

1. In Claude, create (or open) a **Project** you use for design work.
2. Copy a skill file from `skills/<skill-name>/SKILL.md` into your Project’s **Knowledge** (or paste it into chat when needed).
3. Ask for the deliverable in plain language and attach screenshots/links/context as needed.

Example prompts:

- “Write a design spec for this flow. Include states, edge cases, a11y, and open questions.”
- “Run a competitive design audit on this pattern. Compare 3–5 products and recommend what we should do.”

## Skill catalog

- **UX Audit** (`.cursor/skills/ux-audit/`)
  - Use for: heuristic review, friction analysis, flow critique
  - Output: prioritized findings (P0–P2), quick wins, validation plan
- **Accessibility Review** (`.cursor/skills/accessibility-review/`)
  - Use for: WCAG-informed issues + remediations (contrast, focus, labels, motion)
  - Output: must-fix/should-fix/nice-to-have + verification checklist
- **Design System Governance** (`.cursor/skills/design-system-governance/`)
  - Use for: contribution workflow, decision records, release notes
  - Output: copy/paste governance artifacts (templates)
- **Component Spec Writer** (`.cursor/skills/component-spec-writer/`)
  - Use for: component documentation, variant matrix, states/behaviors, token hooks
  - Output: spec doc with slots, variants, a11y, theming, QA checklist
- **Research Synthesis** (`.cursor/skills/research-synthesis/`)
  - Use for: turning raw notes into themes → insights → opportunities
  - Output: evidence-backed insights + hypotheses + next steps
- **Analytics → UX Insights** (`.cursor/skills/analytics-insights/`)
  - Use for: interpreting funnels/events to propose UX mechanisms + experiments
  - Output: ranked hypotheses, follow-up analyses, instrumentation gaps
- **Design Specs Writer** (`.cursor/skills/design-specs-writer/`)
  - Use for: “write a spec”, “handoff notes”, “document this component/flow”
  - Output: engineering-ready spec (states/behaviors/edge cases/a11y/token hooks/open questions)
- **Competitive Design Audit** (`.cursor/skills/competitive-design-audit/`)
  - Use for: competitor comparison, teardown, benchmarking a feature/flow/pattern
  - Output: comparative audit (patterns/trade-offs/opportunities/recommendations + what to capture next)
- **Figma Master (router)** (`.cursor/skills/figma-master/`)
  - Use for: generating/modifying inside Figma; chooses the right workflow
  - Output: concrete next tool calls + stop conditions
- **Figma Triage** (`.cursor/skills/figma-triage/`)
  - Use for: Figma links/requests that are unclear or missing node targeting
  - Output: classification + minimal next calls (metadata/screenshot/discovery) before any writes
- **Figma Design System Discovery** (`.cursor/skills/figma-design-system-discovery/`)
  - Use for: inventorying components/variables/styles to avoid hardcoding during Figma edits
  - Output: reusable design system inventory + recommended next workflow
- **Figma Cleanup and Resume** (`.cursor/skills/figma-cleanup-and-resume/`)
  - Use for: multi-step Figma work that must be resumable/reversible
  - Output: tagging + ledger strategy to prevent duplicates and enable safe cleanup

## How these work

Each skill is a folder under `.cursor/skills/<skill-name>/` with a `SKILL.md` containing:
- when to use it (discoverability)
- what inputs to request (only if missing)
- a repeatable method/checklist
- a deliverable template

Claude Project skills follow the same `SKILL.md` pattern under `skills/<skill-name>/`.

## Docs

- Docs index: `docs/README.md`
- Usage tips and example workflows: `docs/USAGE.md`
- Command-style prompts: `docs/COMMANDS.md`
- Fillable templates: `docs/templates/`
- Golden examples: `docs/examples/`
- Full skills catalog: `docs/SKILLS.md`
- How to author a new skill: `docs/WRITING_SKILLS.md`

## Publishing / development

If you’re missing `git` on macOS, install Apple Command Line Tools:

```bash
xcode-select --install
```


