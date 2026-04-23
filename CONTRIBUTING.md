## Contributing

Thanks for helping improve these Cursor skills.

### Add a new agent (Cursor skill)

1. Create a new folder in `.cursor/skills/<skill-name>/`
2. Add a `SKILL.md` with YAML frontmatter:

```markdown
---
name: skill-name
description: What it does + when to use it (include trigger terms).
---
```

3. Keep `SKILL.md` concise (aim: < 500 lines) and include:
   - Inputs to request (only if missing)
   - A repeatable workflow/checklist
   - A copy/paste-ready output template

4. Follow the repo conventions:
   - Shared conventions: `docs/HOUSE_STYLE.md`
   - How to write skills: `docs/WRITING_SKILLS.md`

### Add a Claude-compatible variant (recommended for tool-agnostic skills)

If the skill is useful outside Cursor (i.e., it doesn’t rely on Cursor-only tooling), add a Claude-compatible variant:

1. Create `skills/<skill-name>/SKILL.md`
2. Keep it **tool-agnostic** and shorter than the Cursor version.
3. It may intentionally diverge from the Cursor version, but must not contradict the house style.

See: `docs/WRITING_SKILLS.md` (Source of truth, Divergence policy, Drift contract).

### What must stay consistent (when a skill exists in both places)

Even if `.cursor/skills/` and `skills/` diverge, keep these consistent:

- **Identity**: `name` and core “use when” intent
- **Definitions**: severity/confidence meanings (per `docs/HOUSE_STYLE.md`)
- **Artifact type**: the deliverable should remain the same kind of output (audit/spec/synthesis)
- **Honesty rules**: don’t guess as fact; label assumptions; include a verification plan when uncertain

### Naming rules

- `name`: lowercase, numbers, hyphens only
- Folder name should match `name`

### Style

- Prefer “Figma-ready” outputs: crisp checklists, component/token naming, variant matrices.
- Default to a **single recommended approach** with an escape hatch, not a menu of options.

### When you add a new skill, update the docs (so it’s discoverable)

- Add the skill to `docs/SKILLS.md`
- Add at least one copy/paste prompt to `docs/COMMANDS.md`
- Strongly recommended:
  - Add a template in `docs/templates/`
  - Add a golden example in `docs/examples/` and list it in `docs/examples/README.md`

