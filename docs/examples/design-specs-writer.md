# Golden examples — `design-specs-writer`

## Scenario A (happy path): `Bulk actions toolbar` spec (web)

### Prompt (user)

“Write a design spec for the bulk actions toolbar in our employee directory table. Include states, behaviors, edge cases, a11y, token hooks, open questions, and a test plan.”

### Inputs provided (user)

- **Platform**: Web
- **Users**: Admin + Manager roles
- **Primary user goal**: Apply bulk updates quickly and safely without accidental changes
- **Constraints**: Must be keyboard accessible; destructive actions require confirmation; table supports pagination
- **Existing system**: Uses a shared `DataTable` component and `Button`, `Checkbox`, `Toast`

### Golden output (model)

## Bulk actions toolbar — Design spec

### Assumptions / constraints

- Assumption: Selection persists within the current table view (page) unless specified; cross-page selection is explicitly surfaced.
- Constraint: Destructive actions require confirmation and clear auditability (who changed what).

### Overview

- **What it is**: A contextual toolbar that appears when one or more rows are selected, enabling safe bulk operations (e.g., change manager, update status, export).
- **Who it’s for**: Admins and Managers with permission to update employee records.
- **Primary user goal**: Apply bulk updates quickly and safely without mistakes.
- **Success definition**:
  - Fewer accidental bulk changes (proxy: undo/rollback usage + support tickets)
  - Faster time-to-complete bulk action flows

### In scope / out of scope

- **In scope**:
  - Toolbar appearance rules and contents
  - Selection + counts + permission-based actions
  - Confirmation + progress + success/failure feedback
- **Out of scope**:
  - The underlying employee edit forms
  - New bulk action types beyond the initial set

### UX requirements (non-negotiables)

- Always communicate **how many** items will be affected.
- Provide a safe path for destructive actions: **confirm** + **clear consequences**.
- Never allow bulk actions the user lacks permission for; communicate why actions are unavailable.
- Works via keyboard only, including selecting rows and invoking actions.

### Anatomy / slots

- **Selection summary**: “3 selected” + optional “Clear”
- **Actions region**: primary bulk action(s) + overflow menu for secondary actions
- **Scope indicator** (if cross-page selection exists): “This page” vs “All results” with an explicit toggle
- **Dismiss**: optional if toolbar overlays content; otherwise it persists while selection exists

### Variants

- `density`: compact | comfortable (inherits table density)
- `scope`: page | all-results (only if supported)

### States

| State | Trigger | UI behavior | Notes |
| --- | --- | --- | --- |
| Hidden | 0 selected | No toolbar | Default |
| Visible | ≥1 selected | Toolbar appears | Should not cause layout jump if avoidable |
| Actions disabled | Permission missing / 0 eligible | Disable specific actions | Explain via tooltip/help text |
| Confirming | Destructive action chosen | Confirmation dialog/sheet | Must include count + consequences |
| Processing | Action submitted | Show progress state | Disable repeat submit; allow cancel if supported |
| Success | Action completes | Toast + optional inline summary | Include count + “View changes” if exists |
| Error | Action fails | Error message + retry guidance | Keep selection intact to recover |

### Interactions & behavior

- **Selection**:
  - Header checkbox selects all rows in view (page) with indeterminate state for partial selection.
  - If “Select all results” is offered, it must be an explicit second step (not implicit).
- **Invoking actions**:
  - Primary action button triggers the default bulk action (configurable).
  - Overflow menu lists secondary actions grouped by type (safe vs destructive).
- **Feedback**:
  - Processing state shows spinner + “Updating 3 employees…”
  - Success toast: “Updated 3 employees” with optional “Undo” when feasible.
- **Undo / escape hatches**:
  - Provide Undo for reversible actions (e.g., status change) when technically feasible.
  - For irreversible actions, provide a clear “View audit log” path instead.

### Content guidelines

- **Labels**: Action labels are verbs (“Change manager”, “Export”, “Deactivate”).
- **Confirmation copy**:
  - Must include affected count and consequence: “Deactivate 3 employees? They will lose access immediately.”
- **Empty/eligibility messaging**:
  - If only some selected rows are eligible, say so: “2 of 5 selected are eligible for export.”

### Edge cases

- Long names in action labels or selection summary (truncate, keep counts visible).
- Mixed permissions across selected rows (eligible subset handling).
- Pagination changes while selection exists (selection persistence policy must be explicit).
- Partial failures (some rows succeed, some fail): show summary + exportable error list if needed.

### Accessibility

- **Keyboard**:
  - Row selection is reachable and operable via keyboard.
  - Focus moves logically into the toolbar when it appears without stealing focus from active input unexpectedly.
- **Focus management**:
  - Confirmation dialog traps focus and returns focus to the triggering control on close.
- **Labels / names**:
  - Checkbox labels announce row context (“Select John Doe row”).
- **Contrast**:
  - Disabled actions remain readable; focus ring visible on all toolbar controls.
- **Motion + reduced motion**:
  - Toolbar entrance avoids excessive motion; reduced motion uses minimal transitions.

### Design system hooks (token-first)

- **Reuse**: `DataTable`, `Checkbox`, `Button`, `Menu`, `Dialog`, `Toast`
- **Token hooks**:
  - Surface + elevation tokens for toolbar container
  - Spacing/gap tokens aligning with table density
  - Semantic tokens for destructive actions

### Open questions (owners TBD)

- [ ] Does selection persist across pagination? If yes, how do we show “All results” selection safely?
- [ ] Which actions must support Undo vs audit-log-only?
- [ ] What is the maximum number of rows allowed in a single bulk operation?

### Test plan / how to verify

- **Design QA**: density variants, long text, dark mode
- **Engineering QA**: keyboard path + focus return + partial failure handling
- **User validation**: 5 usability sessions on bulk update + destructive confirmation comprehension

---

## Scenario B (messy inputs): “Write a spec for onboarding” with no assets

### Prompt (user)

“Write a spec for our onboarding flow.”

### Inputs provided (user)

- None

### Golden output (model)

### Assumptions (minimal)

- Assumption: “Onboarding” includes account setup + first value action, but the steps are not defined.

### What’s missing (minimum to produce a credible spec)

- Steps/screens in the flow (even a bullet list)
- Primary user goal + success definition
- Platform + constraints (a11y, localization, auth/payments)

### Useful draft skeleton (still actionable)

- Outline the spec sections (scope, steps, states, edge cases, a11y, instrumentation, open questions).
- Provide a “Step template” the team can fill:
  - Step name
  - User task
  - Inputs + validation
  - Errors/recovery
  - Exit criteria

### Test plan / how to verify

- Once steps are provided, run a quick audit for moment-of-truth points and define success signals per step.

