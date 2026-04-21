# Usage

## Best inputs (what to attach)

- **Screenshots**: include the whole screen plus any modal/toast states if possible.
- **Figma links / component names**: paste the URL and call out the frame/component name.
- **Analytics**: paste the funnel steps, timeframe, and segment. If definitions are ambiguous, paste the exact metric definitions.

## Golden examples (calibration)

If you want outputs to match a consistent “house style,” skim `docs/examples/` and ask the agent to match the structure of the relevant file (for example, `docs/examples/ux-audit.md`).

## Prompt patterns that work well

### UX audit (screenshots/flow)

- “Audit these screens for friction. Prioritize P0/P1 issues and propose concrete fixes.”
- “Assume first-time user. Identify the moment-of-truth decision points and where users might churn.”

### Component spec (design system)

- “Write a spec for `Toast`. Include variants/states, content rules, token hooks, a11y, and QA checklist.”
- “Include a compact variant matrix and call out invalid combinations.”

### Research synthesis

- “Cluster these notes into themes. Produce insights and opportunities, with evidence snippets.”
- “Turn themes into falsifiable hypotheses and define success signals.”

### Analytics → UX insights

- “Given this funnel, propose ranked UX hypotheses for the biggest leak and what to measure next.”
- “List instrumentation gaps that prevent confident conclusions.”

## If you want more consistent outputs

When asking, include:
- **goal metric**
- **primary user goal**
- **constraints** (a11y, localization, payments/auth, time)
- **success definition** (what “better” means)

