# Golden examples — `design-system-governance`

## Scenario A (happy path): contribution workflow for a growing team

### Prompt (user)

“Create a lightweight design system governance starter pack: contribution workflow, decision record template, and release notes template.”

### Inputs provided (user)

- **Consumers**: 6 product teams, mostly web
- **Pain**: inconsistent contributions; unclear who approves; breaking changes surprise teams
- **Release model**: weekly package releases + hotfix as needed

### Golden output (model)

#### Contribution workflow (lightweight)

##### Intake

- **Proposal**: problem statement + users impacted + alternatives considered (1 page max)
- **Evidence**: screenshots, analytics snippet, support themes (optional but encouraged)

##### Review

- **Design system council**: design + eng + a11y (rotate weekly reviewer)
- **SLA**:
  - **Triage**: 2 business days
  - **Decision**: 5 business days for new components; 2 days for token tweaks (unless breaking)

##### Build + document

- **Requirements for merge**:
  - Figma component + documentation page updated
  - Code implementation + Storybook (or equivalent) examples
  - Accessibility notes + keyboard spec for interactive components
  - Migration notes if replacing an old pattern

##### Release

- **Versioning**: semver for packages; communicate breaking changes 1 release ahead when possible
- **Adoption**: provide codemod or deprecation window for breaking APIs

#### Decision record template (copy/paste)

```markdown
## DR-XXX: <short title>

### Context
What problem are we solving? Who is impacted?

### Decision
What are we doing?

### Alternatives considered
- Option A:
- Option B:

### Consequences
- Pros:
- Cons:
- Migration plan:
- Verification plan:
```

#### Release notes template (copy/paste)

```markdown
## Design System vX.Y.Z — <date>

### Highlights
- 

### New
- 

### Improvements
- 

### Fixes
- 

### Breaking changes
- **What changed**:
- **Why**:
- **Migration**:
- **Rollback plan**:

### Deprecations
- 

### Shoutouts
- 
```

#### Test plan / validation

- Pilot the workflow on one real contribution next sprint and time-box retro notes (what felt heavy?)

---

## Scenario B (messy inputs): “We need governance” (no details)

### Prompt (user)

“We need governance.”

### Golden output (model)

#### Assumptions (minimal)

- **Assumption**: You want something adoptable in 2 weeks, not a full enterprise program.

#### Minimum clarifying questions (pick answers inline next message)

- How many teams consume the system?
- Monorepo vs multi-repo? (Impacts release + migration mechanics)
- What’s failing today: quality, velocity, accessibility, brand consistency, or all of the above?

#### Starter pack (still usable)

- **Roles**: owner (accountable), maintainers (execute), reviewers (rotate)
- **Rules of the road**:
  - New patterns start in a product only if they’re labeled **experimental** and have an exit plan
  - Promote to system only after 2+ teams need it OR it reduces high-risk inconsistency (a11y/security)

#### Test plan / validation

- Run a **90-minute workshop** with 1 designer + 1 engineer + 1 PM to agree on intake + versioning basics
