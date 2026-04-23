# Usage

## Best inputs (what to attach)

- **Screenshots**: include the whole screen plus any modal/toast states if possible.
- **Figma links / component names**: paste the URL and call out the frame/component name.
- **Analytics**: paste the funnel steps, timeframe, and segment. If definitions are ambiguous, paste the exact metric definitions.

## Golden examples (calibration)

If you want outputs to match a consistent “house style,” skim `docs/examples/` and ask the agent to match the structure of the relevant file.

## Prompt patterns that work well

### UX audit (`ux-audit`)

- “Audit these screens for friction. Prioritize P0/P1/P2 issues and propose concrete fixes. Include a test plan.”
- “Assume first-time user. Audit this flow. Identify moment-of-truth decision points, likely churn points, and fixes. Include quick wins and a validation plan.”

### Accessibility review (`accessibility-review`)

- “Do an accessibility review of these screens. Return must-fix/should-fix/nice-to-have issues, plus a regression checklist.”

### Component spec (`component-spec-writer`)

- “Write a component spec for `Toast`. Include variants/states, content rules, token hooks, a11y, theming, and QA checklist. Call out invalid combinations.”
- “Include a compact variant matrix and call out invalid combinations.”

### Design system governance (`design-system-governance`)

- “Create a lightweight governance starter pack: contribution workflow, decision record template, and release notes template.”

### Research synthesis (`research-synthesis`)

- “Cluster these notes into themes. Produce insights and opportunities, with evidence snippets.”
- “Turn themes into falsifiable hypotheses and define success signals.”

### Analytics → UX insights (`analytics-insights`)

- “Given this funnel, propose ranked UX hypotheses for the biggest leak and what to measure next.”
- “List instrumentation gaps that prevent confident conclusions.”

### Design spec (`design-specs-writer`)

- “Write a design spec for `FEATURE_OR_COMPONENT`. Include assumptions, scope, anatomy/steps, variants, states, interactions, content guidelines, edge cases, accessibility, token hooks, open questions, and a test plan.”

### Competitive design audit (`competitive-design-audit`)

- “Run a competitive design audit for `PATTERN_OR_FLOW`. Compare 3–5 relevant products plus one best-in-class reference. Summarize market patterns, trade-offs, opportunities, and give concrete recommendations. Include what to capture next if evidence is missing.”

## If you want more consistent outputs

When asking, include:
- **goal metric**
- **primary user goal**
- **constraints** (a11y, localization, payments/auth, time)
- **success definition** (what “better” means)

