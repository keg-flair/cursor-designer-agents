# Golden examples — `accessibility-review`

## Scenario A (happy path): checkout “Pay now” affordance + error text

### Prompt (user)

“Do an accessibility review of these checkout screens. Return must-fix/should-fix/nice-to-have issues, plus a regression checklist.”

### Inputs provided (user)

- **Platform**: Web
- **Target**: WCAG 2.2 AA intent (engineering verification still required)
- **Screens**:
  - Primary button uses light gray text on a slightly lighter gray background
  - Error text under card fields is red-only with no icon/programmatic association called out visually

### Golden output (model)

#### Summary

- **Scope**: Checkout web flow (as provided)
- **Standard**: WCAG 2.2 AA **intent** (contrast/focus/labels need measurement in implementation)

#### Findings

##### Must-fix

- **Contrast (text/UI components)**: Primary “Pay now” label likely fails contrast for normal text and/or UI component boundaries
  - **Why it matters**: Users with low vision or bright environments cannot reliably identify the primary action
  - **Remediation**:
    - Use **token-driven** primary colors with verified contrast on default/hover/focus/disabled
    - Ensure **disabled** state doesn’t look like a normal inactive button (clarify unavailable vs available)
  - **Verify**: Automated contrast checks on all button states; spot-check with high contrast mode

- **Error identification + association**: Errors appear communicated primarily through color
  - **Why it matters**: Color-blind users and screen reader users may miss the problem scope
  - **Remediation**:
    - Add visible error icon + text pattern; associate message with field (`aria-describedby` pattern in implementation)
    - Announce errors without relying solely on color (copy + placement + focus management policy)
  - **Verify**: Keyboard-only submission path; SR spot checks on invalid submit

##### Should-fix

- **Focus visibility**: If focus rings are suppressed for “clean UI,” restore visible focus for all interactive controls
  - **Verify**: Tab through full checkout; confirm focus order matches visual order

##### Nice-to-have

- **Motion**: If success animations are prominent, provide reduced-motion behavior
  - **Verify**: OS reduced-motion setting + CSS preference behavior (engineering)

#### Regression checklist (release QA)

- [ ] Keyboard: tab order logical; no traps in dialogs
- [ ] Focus: always visible; modals manage focus return
- [ ] Names: buttons/links have descriptive accessible names (not just “Click here”)
- [ ] Forms: labels, instructions, errors associated; error summary on submit (if used)
- [ ] Contrast: text + icons + UI controls across themes (light/dark)
- [ ] Zoom: usable at 200% zoom without loss of function (spot-check)

#### Test plan / validation

- **Engineering**: axe + manual keyboard pass on payment step states (valid/invalid/loading)
- **Design**: token audit for primary/error colors across states
- **Research** (optional): 3–5 sessions with SR users if checkout is business-critical

---

## Scenario B (messy inputs): “Is this accessible?” with one blurry screenshot

### Prompt (user)

“Is this accessible?” (+ 1 low-res screenshot, no platform)

### Golden output (model)

#### What I can conclude from the screenshot

- I can flag **obvious heuristic risks** (e.g., tiny text, low contrast that appears borderline), but I **cannot certify** WCAG conformance from image quality alone.

#### Assumptions

- **Assumption**: Web UI unless you confirm mobile native patterns differ materially

#### Must-fix / should-fix (conditional)

- **Must-fix (conditional)**: Any control that appears to rely on color alone for state—verify with implementation + SR
- **Should-fix (conditional)**: If text appears below ~12–14sp equivalent for primary tasks, validate readability and zoom behavior

#### Highest-value next inputs

- **Platform** (web/iOS/Android)
- **High-res screenshots** for default + error + focus states
- **A screen recording** of keyboard navigation for the critical path

#### Test plan / validation

- Once clearer assets arrive, rerun the regression checklist in Scenario A and narrow findings to verified issues
