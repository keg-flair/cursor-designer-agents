## House style (applies to all skills)

Use this as the shared convention baseline across the skill suite.

### Evidence and honesty

- **Never present guesses as facts.**
- Clearly separate:
  - **Provided** (what the user gave)
  - **Observed** (what can be seen in screenshots/recordings)
  - **Assumed** (explicitly labeled)
  - **Unknown / needs verification**

### Clarifying questions

- Ask **at most 2–3** clarifying questions.
- Only ask when answers materially change:
  - the spec’s API surface / states
  - the audit’s priorities
  - the hypothesis ranking / next analyses

### Fallback behavior (when inputs are missing)

If evidence is missing or vague, still produce something useful:
- A **low-confidence** draft (clearly labeled)
- A short **“highest-value next inputs”** list (max 5 bullets)
- A **verification / test plan** (how to prove or disprove)

### Severity conventions (audits)

- **P0 / Must-fix**: blocks completion, severe trust/safety risk, unrecoverable errors, or likely WCAG failure (high confidence).
- **P1 / Should-fix**: meaningful friction/confusion/anxiety; users can recover but it’s costly.
- **P2 / Nice-to-have**: polish and efficiency improvements; not a primary driver of failure.

### Confidence conventions (insights/synthesis)

- **High**: supported by repeated evidence + clear mechanism (or multiple converging signals).
- **Medium**: plausible and fits the shape, but needs a decisive cut/qual check.
- **Low**: speculative; treat as triage suggestions and focus on what to measure next.

### Token hooks protocol (design system outputs)

1. **Prefer existing tokens** and existing components/patterns.
2. **Describe tokens by intent, not hex**:
   - surface, text, border, icon, focus ring, elevation, spacing, radius, motion
3. **Propose new tokens only when reusable** across multiple components/states.
4. **Name tokens semantically** (meaning-based), not color-based (`blue-500`) or one-off usage labels.

