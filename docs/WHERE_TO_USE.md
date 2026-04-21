## Where to use what (Cursor vs Claude)

This repo contains two “targets”:

- **Cursor**: project skills + rules that run inside Cursor (`.cursor/...`)
- **Claude Projects**: tool-agnostic skills you paste into a Claude Project’s Knowledge (`skills/...`)

### Quick decision guide

Use **Cursor** when you want:

- to work inside a repository and produce files
- to use Cursor-specific rules/skills
- to generate/modify **inside Figma** via MCP + `use_figma` (tool-driven workflows)

Use **Claude Projects** when you want:

- a repeatable deliverable template (specs, audits) without depending on IDE tooling
- to work from screenshots/links and produce docs you paste into Notion/Figma/etc.

### Folder map

- **Cursor skills**: `.cursor/skills/<skill-name>/SKILL.md`
- **Cursor rules**: `.cursor/rules/` (always-on guidance for Cursor’s agent)
- **Claude skills**: `skills/<skill-name>/SKILL.md`
- **Docs**: `docs/` (commands, templates, examples)

### How to install / use (Cursor)

1. Copy this repo’s `.cursor/` folder into your product/design repo.
2. In Cursor, ask for the task in plain language and attach screenshots/links as needed.
3. If the task is Figma generate/modify, start with `figma-master` (router) or `figma-triage`.

### How to install / use (Claude Projects)

1. In Claude, create (or open) a Project.
2. Copy one or more files from `skills/<skill-name>/SKILL.md` into the Project’s Knowledge.
3. Ask for the deliverable and attach screenshots/links/context.

### Figma-specific note (generate/modify)

The skills under `.cursor/skills/figma-*` are designed for **Cursor + Figma MCP + `use_figma`** workflows:

- `figma-master`: routes to the right workflow and lists the next tool calls
- `figma-triage`: clarifies scope/targeting before any writes
- `figma-design-system-discovery`: inventories components/variables/styles to avoid hardcoding
- `figma-cleanup-and-resume`: tagging + ledger patterns for multi-step/resumable work

If you paste those into Claude, they may read fine, but they reference Cursor/Figma tooling and are most effective in Cursor.

