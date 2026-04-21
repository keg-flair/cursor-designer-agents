---
name: figma-design-system-discovery
description: Discover and summarize a Figma file’s design system building blocks (components, variables, styles, conventions) to enable safe generate/modify workflows. Use before writing to Figma when you need a component/token/style inventory or naming conventions.
---
## Goal

Produce a reusable inventory of a Figma file’s design system so future `use_figma` writes can reuse components/variables/styles instead of hardcoding values.

## When to use

- Before generating a new screen/page in Figma
- Before modifying an existing screen when you suspect it’s built from a design system
- When you need to know: component sets, variant axes, TEXT properties, variables (including library variables), text styles, effect styles

## Inventory output contract (always)

Return a structured summary with:

- **Pages**: names + IDs (or shortlist)
- **Reference screens**: 1–3 candidate frames/pages to inspect for conventions
- **Components**:
  - key component sets/components (name + key + how to import)
  - for the most relevant components: which properties exist (TEXT/BOOLEAN/VARIANT/INSTANCE_SWAP) and any naming quirks
- **Variables**:
  - whether variables are local vs library
  - discovered naming scheme (e.g. `color/bg/...`, `space/...`)
- **Styles**:
  - text styles and effect styles naming patterns
- **Conventions**:
  - common frame widths, layout primitives, spacing strategy, naming patterns

## Required workflow (read-first)

### Step 1: Prefer inspecting existing screens

If the target file already contains screens using the same design system, inspect instances/bound variables/styles there first. Treat those as authoritative.

### Step 2: Discover components

Use a read-only `use_figma` script to:

- iterate candidate frames
- collect unique main component keys for instances
- detect component sets vs standalone components

If there are no reference screens, fall back to `search_design_system` with multiple short queries (button/input/card/nav/typography/etc.).

### Step 3: Discover component properties (TEXT keys matter)

For the most relevant components:

- import by key (component or component set)
- create a temporary instance
- read `componentProperties` (and optionally nested instances)
- remove the temp instance

This yields the authoritative property keys needed for `setProperties()`.

### Step 4: Discover variables (local AND library)

You MUST use both:

- local: `figma.variables.getLocalVariableCollectionsAsync()` + `getLocalVariablesAsync()`
- library: `search_design_system` with `includeVariables: true`

If you find variables bound on existing nodes, record their keys so they can be re-imported (`importVariableByKeyAsync`) during writes.

### Step 5: Discover styles (text + effect)

Preferred:

- inspect a reference screen for `textStyleId` / `effectStyleId` usage patterns

Fallback:

- `search_design_system` with `includeStyles: true` for “heading/body/caption/shadow/elevation”

### Step 6: Recommend the next workflow

- screen build → `figma-generate-design`
- targeted modification → `figma-use`
- design system work → `figma-generate-library`

## Stop conditions

Stop and do not proceed to writes if:

- No reference screens exist AND `search_design_system` returns nothing useful
- You cannot identify how to set text (no TEXT properties and text layers are deeply nested/locked)
- Variables/styles exist but cannot be imported (missing keys / access constraints)

