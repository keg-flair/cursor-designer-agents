# Claude Designer Agents (Skills)

A small suite of **Claude-ready skills** for Senior Product Designers working on **UX/UI** and **design systems**.

These skills are optimized for **screenshots**, **Figma links/component names**, and **lightweight product context**, and they output artifacts that are easy to paste into **Figma pages**, **Notion**, or **design-system docs**.

## Repository

- **GitHub**: `https://github.com/keg-flair/claude-designer-agents`

## What’s in this repo

- **Skills**: `skills/` (`skills/<skill-name>/SKILL.md`)
- **Docs**: `docs/` (usage tips + prompts you can paste into Claude)

## Quick start (Claude Projects)

1. In Claude, create (or open) a **Project** you use for design work.
2. Copy a skill file from `skills/<skill-name>/SKILL.md` into your Project’s **Knowledge** (or keep it open and paste it into the chat when needed).
3. Ask for the deliverable in plain language and attach screenshots/links/context as needed.

Example prompts:
- “Write a design spec for this flow. Include states, edge cases, a11y, and open questions.”
- “Run a competitive design audit on this pattern. Compare 3–5 products and recommend what we should do.”

## Skill catalog

- **Design Specs Writer** (`skills/design-specs-writer/`)
  - Use for: “write a spec”, “handoff notes”, “document this component/flow”
  - Output: engineering-ready spec (states/behaviors/edge cases/a11y/token hooks/open questions)
- **Competitive Design Audit** (`skills/competitive-design-audit/`)
  - Use for: competitor comparison, teardown, benchmarking a feature/flow/pattern
  - Output: comparative audit (patterns/trade-offs/opportunities/recommendations + what to capture next)

## How these work

Each skill is a folder under `skills/<skill-name>/` with a `SKILL.md` containing:
- when to use it (discoverability + trigger terms)
- what inputs to request (only if missing)
- a repeatable method/checklist
- a copy/paste output template

## Docs

- **Docs index**: `docs/README.md`
- **Usage tips**: `docs/USAGE.md`
- **Copy/paste prompts**: `docs/COMMANDS.md`
- **Skill catalog**: `docs/SKILLS.md`

## Publishing / development

If you’re missing `git` on macOS, install Apple Command Line Tools:

```bash
xcode-select --install
```


