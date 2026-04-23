# Writing new skills

## Goal

A skill should produce a **repeatable design artifact** (spec, audit, synthesis, governance doc) with minimal back-and-forth.

## Folder structure

Create:

```
.cursor/skills/<skill-name>/SKILL.md
```

If a skill is tool-agnostic and useful outside Cursor, also mirror it in:

```
skills/<skill-name>/SKILL.md
```

## Source of truth

- **Primary**: `.cursor/skills/` + `.cursor/rules/` (Cursor behavior and enforcement)
- **Mirror**: `skills/` (Claude-compatible copies)

When you update a shared skill, update both copies (or intentionally document why they differ).

## `SKILL.md` checklist

Include:
- YAML frontmatter:
  - `name`: lowercase, numbers, hyphens only
  - `description`: what it does + when to use it (include trigger terms)
- “Inputs to request (only if missing)”
- A short method/checklist
- A copy/paste output template

## Style guidelines (for this repo)

- Default to **tool-agnostic** guidance.
- Keep outputs **Figma-ready**: crisp sections, variant matrices, token naming hooks, QA checklists.
- Prefer a **single recommended approach** with an escape hatch.
- Don’t over-claim: label assumptions and provide a verification plan when evidence is incomplete.

## Example frontmatter

```markdown
---
name: empty-states
description: Produces empty/loading/error state guidelines and copy recommendations. Use when the user asks for empty states, edge cases, or state design.
---
```

