---
name: figma-triage
description: Triage a Figma request (generate/modify in Figma) into the minimal, correct next steps. Use when the user provides a Figma URL, node-id, or asks to update/create something in a Figma file and you need to decide which Figma workflow/tools to run next.
---
## Goal

Turn an ambiguous “do something in Figma” request into a concrete plan and the exact next tool calls needed (metadata, screenshot, design system search, or `use_figma` scripts).

## When to use

- User provides a Figma URL and asks to “update this”, “make it match”, “create a screen”, “modify layout”, “change tokens”, etc.
- You are about to write to Figma but you don’t yet know:
  - what node(s) to target
  - whether it’s a screen build vs component/library work
  - whether the design system tokens/components exist in the file or libraries

## When NOT to use

- The user’s deliverable is **code**, not Figma edits.
- You already have the exact node IDs + intended edits and are ready to write a `use_figma` script.

## Required outputs from triage (always)

In your response, you MUST produce:

- **What you think the user wants** (1–2 sentences)
- **Target**: fileKey and nodeId (or “selection-based” if using desktop selection)
- **Classification** (pick one):
  - **Screen/page generation** (compose frames from design system components) → `figma-generate-design` + `figma-use`
  - **Modify existing nodes** (adjust layout/styles/content) → `figma-use`
  - **Design system/library work** (tokens/components/modes) → `figma-generate-library` + `figma-use`
  - **Code Connect mappings** → `figma-code-connect`
- **Next tool calls**: the minimal list, in order, with arguments

## Step 1: Parse the Figma URL (if present)

If the user provided a URL, extract:

- **fileKey**: the segment after `/design/` or `/file/` (or branch key in `/branch/...`)
- **nodeId**: the `node-id` query param
- Convert nodeId from hyphens to colons: `1234-5678` → `1234:5678`

If there is **no `node-id`**, you cannot precisely target a node. Your next step is to ask for a link that includes `node-id` or use selection-based workflows (if available).

## Step 2: Establish ground truth with read tools (before any writes)

Run these before proposing a write script:

- `get_metadata(fileKey, nodeId)` to understand the node’s type and child structure
- `get_screenshot(fileKey, nodeId)` to anchor visual expectations

If the node is huge and design context may truncate:

- Start with `get_metadata`
- Then call `get_design_context` only on the specific child nodes you need

## Step 3: Decide which workflow applies

Use the metadata + screenshot to decide:

- **If it’s a full screen/page build**:
  - Prefer `figma-generate-design`
  - Next step: discovery pass for design system components/variables/styles (inspect existing screens first; then `search_design_system`)
- **If it’s a targeted modification**:
  - Use `figma-use`
  - Next step: a read-only `use_figma` probe to locate nodes deterministically (by name/type/traversal), then a small write
- **If it’s tokens/components/library changes**:
  - Use `figma-generate-library`
  - Next step: discovery inventory + scope lock (what tokens/components are in/out)

## Step 4: Hard stop conditions (do not write yet)

Do NOT proceed to `use_figma` writes if any of these are true:

- You don’t have a nodeId (and no selection-based context)
- You don’t have a screenshot reference for visual changes
- You cannot name the exact nodes you intend to modify (no stable IDs or deterministic find strategy)
- You suspect a design system exists but haven’t searched/inspected for reusable components/variables/styles yet

## Step 5: Hand-off to the right skill (mandatory)

Once triage is complete:

- For **any `use_figma` call**, ensure `figma-use` is loaded first.
- For **screen builds**, also load `figma-generate-design`.
- For **design system/library builds**, also load `figma-generate-library`.

