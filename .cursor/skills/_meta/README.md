These are Cursor **project skills**.

- Each folder under `.cursor/skills/` contains a `SKILL.md` with:
  - YAML frontmatter (`name`, `description`)
  - concise, repeatable instructions
  - an output template

Shared conventions:

- **House style**: `docs/HOUSE_STYLE.md` (severity, confidence, token protocol, fallbacks)
- **Cursor enforcement** (always-on): `.cursor/rules/`

To add more agents, duplicate an existing folder and keep `SKILL.md` under ~500 lines.

