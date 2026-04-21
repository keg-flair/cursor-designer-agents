---
name: figma-master
description: Route Figma generate/modify requests to the correct workflow and skills (triage, design system discovery, use_figma writes, screen generation, cleanup/resume, Code Connect). Use whenever the user asks to create/update something in Figma and you need to choose the right next steps.
---
## Goal

Ensure Figma work uses the correct workflow and avoids common failure modes (writing too early, hardcoding tokens, duplicating screens, losing state).

## Routing rules (mandatory)

Classify the request into exactly one primary path:

1. **Ambiguous / missing node-id / unclear scope** → use `figma-triage`
2. **Need design system inventory first** (components/variables/styles unknown) → use `figma-design-system-discovery`
3. **Build or update a full screen/page in Figma** → use `figma-generate-design` + `figma-use`
4. **Targeted modification of existing nodes** (layout tweaks, text, spacing, swaps) → use `figma-use`
5. **Long multi-step workflow / must be resumable or reversible** → use `figma-cleanup-and-resume` (then proceed with 3 or 4)
6. **Create/maintain Code Connect mappings** → use `figma-code-connect`

If multiple apply, choose the earliest prerequisite:

`cleanup/resume` (if needed) → `triage` (if unclear) → `discovery` (if unknown DS) → write path.

## Hard gates (do not write yet)

Do NOT write (`use_figma`) until all required prerequisites for the chosen path are satisfied:

- **Targeted modifications**: you can deterministically locate the nodes to change (IDs or robust find strategy) and have a screenshot reference for visual changes.
- **Screen/page generation**: you have a component/token/style discovery plan (inspect existing screens first; then `search_design_system`), and you will build section-by-section.
- **Cleanup/resume**: you have a `runId` and a ledger strategy (prefer `.cursor/figma/state.json`) and you will tag nodes with shared plugin data.

## Skill hand-offs (mandatory)

- For **any** `use_figma` call: load `figma-use` first.
- For **screen generation**: load `figma-generate-design` in addition to `figma-use`.
- For **multi-step edits**: load `figma-cleanup-and-resume` first to set up tags/ledger.
- For **inventory**: use `figma-design-system-discovery` before writing.

## Minimal output contract (always)

After routing, you MUST respond with:

- **Chosen path** (one of the 6 above)
- **Why** (1–2 sentences)
- **Next actions**: the exact next tool calls you will run (ordered)
- **Stop condition**: what would make you pause before writing

