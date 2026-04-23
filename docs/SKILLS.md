# Skills catalog

This repo ships:

- **Cursor project skills** under `.cursor/skills/`
- **Claude-compatible skills** under `skills/`

Most skills exist in both places; `.cursor/skills/` is what you copy into a Cursor repo, and `skills/` contains Claude-compatible variants. They may intentionally diverge.

## General UX / design system skills (Cursor + Claude-compatible)

## design-specs-writer

- **Use when**: “write a spec”, “handoff notes”, “document this component/flow”, “spec out this feature”
- **Inputs**: component/feature context, platform(s), constraints, link/screenshot (optional)
- **Output**: engineering-ready spec (states/behaviors/edge cases/a11y/token hooks/open questions)
- **Golden example**: `docs/examples/design-specs-writer.md`

## competitive-design-audit

- **Use when**: competitor comparison, teardown, benchmarking a feature/flow/pattern
- **Inputs**: scope + decision to inform, comparator list (or permission to propose), any evidence links/screens
- **Output**: comparative audit (patterns/trade-offs/opportunities/recommendations + what to capture next)
- **Golden example**: `docs/examples/competitive-design-audit.md`

## ux-audit

- **Use when**: heuristic review, friction analysis, flow critique
- **Inputs**: screenshots/recording (best), goal + success definition, constraints
- **Output**: prioritized findings (P0–P2), concrete fixes, quick wins, validation plan
- **Golden example**: `docs/examples/ux-audit.md`

## accessibility-review

- **Use when**: WCAG-informed review, “is this accessible?”, accessibility regression checklist
- **Inputs**: platform + target standard, screenshots showing focus/error states if possible
- **Output**: must-fix/should-fix/nice-to-have issues + regression checklist + verification plan
- **Golden example**: `docs/examples/accessibility-review.md`

## component-spec-writer

- **Use when**: documenting/spec’ing a reusable design system component
- **Inputs**: component purpose + platforms + theming constraints + primary use cases
- **Output**: component spec (anatomy/variants/states/behavior/content/token hooks/a11y/QA)
- **Golden example**: `docs/examples/component-spec-writer.md`

## design-system-governance

- **Use when**: contribution workflow, approvals, breaking-change management, release notes templates
- **Inputs**: consumer teams + repo/release model + current pain points
- **Output**: governance starter pack (workflow + decision record + release notes templates)
- **Golden example**: `docs/examples/design-system-governance.md`

## research-synthesis

- **Use when**: turning raw notes into themes → insights → opportunities
- **Inputs**: study goal, participants/segment, verbatim snippets
- **Output**: evidence-backed synthesis + hypotheses + success signals + follow-ups
- **Golden example**: `docs/examples/research-synthesis.md`

## analytics-insights

- **Use when**: funnel/event drop-offs need UX hypotheses + next analyses
- **Inputs**: funnel steps + definitions + timeframe + segment
- **Output**: ranked hypotheses (mechanism + tests) + instrumentation gaps + next analyses
- **Golden example**: `docs/examples/analytics-insights.md`

## empty-states

- **Use when**: empty/loading/error/success state design for a screen, flow, or component
- **Inputs**: surface + goal, what “empty” means, constraints (a11y/localization/offline)
- **Output**: state taxonomy + state matrix + copy patterns + recovery policy + token hooks + QA checklist
- **Golden example**: `docs/examples/empty-states.md`

## Figma workflow skills (Cursor-only)

These exist under `.cursor/skills/figma-*` and are designed for Cursor + Figma MCP workflows.

## figma-master

- **Use when**: you want the agent to choose the right Figma workflow (generate vs edit vs discovery)
- **Inputs**: Figma link (preferably with `node-id`) + desired outcome + constraints
- **Output**: routed workflow + next actions + stop conditions

## figma-triage

- **Use when**: Figma request is ambiguous or targeting isn’t clear yet
- **Inputs**: Figma link (with `node-id` if possible), desired changes, constraints
- **Output**: clarified scope + minimal next steps before any writes

## figma-design-system-discovery

- **Use when**: you need to inventory components/variables/styles to avoid hardcoding
- **Inputs**: file key / link + reference screen/component name (if any)
- **Output**: design system inventory + recommended next workflow

## figma-cleanup-and-resume

- **Use when**: multi-step Figma work must be resumable/reversible without duplicates
- **Inputs**: runId (if resuming), intended scope, target file/page
- **Output**: tagging + ledger strategy + safe cleanup constraints

