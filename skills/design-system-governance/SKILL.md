---
name: design-system-governance
description: Creates lightweight governance artifacts for a design system: contribution workflow, decision record template, and release notes template (plus adoption/migration guidance). Use when teams struggle with consistency, approvals, breaking changes, or contribution throughput.
---

# Design System Governance

See shared conventions in `docs/HOUSE_STYLE.md` (severity language, fallbacks, evidence labels).

## Defaults

- **Lightweight and adoptable**: aim for something a team can pilot in 1–2 weeks.
- **Decision + release oriented**: optimize for fewer surprises (breaking changes, unclear ownership).
- **Practical templates**: copy/paste-ready artifacts.

## Governance maturity rubric (pick a level, default to Level 1)

- **Level 1 (Starter)**: intake + lightweight review + release notes; minimal ceremony.
- **Level 2 (Scaling)**: SLAs, defined roles/rotation, migration guidance, deprecation windows.
- **Level 3 (Enterprise)**: auditability, compliance gates, formal accessibility verification, multi-platform parity tracking.

## Constraints

- **Do not invent** team structure, release cadence, or toolchain specifics.
- **Ask at most 3 clarifying questions**; if unanswered, proceed with reasonable defaults and label them.

## Clarifying questions (ask max 3)

1. How many teams consume the system, and which platforms (web/native)?
2. Repo/release model (monorepo vs multi-repo; package vs “docs only”)?
3. What’s the biggest pain today: quality, velocity, accessibility, brand drift, breaking changes, or approvals?

## Inputs to request (only if missing)

- Consumer teams count + primary platform
- Current release cadence (if any)
- Current pain points + one recent example of a “bad contribution”

## Fallback behavior (when details are missing)

If the user only says “we need governance”, produce a **Level 1 starter pack** with:
- Roles + review rotation suggestion
- Minimal definition of done
- Decision record + release notes templates
- A short “what to answer next” list to evolve to Level 2

## Output template

```markdown
#### Contribution workflow (lightweight)

##### Intake
- Proposal: problem statement + users impacted + alternatives considered
- Evidence: screenshots/analytics/support themes (optional)

##### Review
- Roles: owner (accountable), maintainers (execute), reviewers (rotate)
- SLA: triage + decision targets

##### Build + document (definition of done)
- Figma + docs updated
- Code example(s) + usage guidance
- Accessibility notes (keyboard/focus) for interactive components
- Migration notes if replacing an old pattern

##### Release + adoption
- Versioning policy (semver if packaged)
- Deprecation window + migration plan for breaking changes

#### Decision record template (copy/paste)
```markdown
## DR-XXX: <short title>
### Context
### Decision
### Alternatives considered
### Consequences (pros/cons)
### Migration plan
### Verification plan
```

#### Release notes template (copy/paste)
```markdown
## Design System vX.Y.Z — <date>
### Highlights
### New
### Improvements
### Fixes
### Breaking changes (what/why/migration/rollback)
### Deprecations
### Shoutouts
```

#### Test plan / validation
- Pilot on one real contribution next sprint; retro what felt heavy vs helpful
```

