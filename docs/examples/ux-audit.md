# Golden examples — `ux-audit`

## Scenario A (happy path): onboarding checkout friction

### Prompt (user)

“Audit this onboarding checkout flow for friction. Prioritize P0/P1/P2 issues and propose concrete fixes. Include a test plan.”

### Inputs provided (user)

- **Platform**: Web
- **Primary user goal**: Complete first purchase quickly with confidence
- **Success definition**: Higher checkout completion without increasing refunds/chargebacks
- **Screens / states**:
  - Step 1: Cart summary (OK)
  - Step 2: Shipping (OK)
  - Step 3: Payment (shows generic error: “Something went wrong”)
  - Step 4: Confirmation (sometimes missing)

### Golden output (model)

#### Summary

- **Primary user goal**: Complete first purchase quickly with confidence
- **What’s being audited**: Web checkout flow (cart → shipping → payment → confirmation)
- **Success definition**: Higher checkout completion without increasing refunds/chargebacks

#### Key findings (prioritized)

##### P0 (must fix)

- **Issue**: Payment failure is unactionable and erodes trust at the highest-risk step
  - **Where**: Payment step after card submission
  - **Why it matters**: Users cannot recover without guessing; abandonment spikes here for first-time buyers
  - **Proposed fix**:
    - Replace generic error with **specific, safe** messaging (card declined vs processor timeout vs validation)
    - Provide **next steps** (retry, different payment method, contact support) and preserve entered non-sensitive fields
    - Log a support-friendly **error code** (user-visible) for CS alignment
  - **Risk / trade-off**: Over-specific errors can leak sensitive info—keep messages user-safe and aligned with risk policy
  - **How to verify**:
    - Instrument payment errors by category and measure retry rate + completion
    - Qualitative sessions: observe comprehension + time-to-recover

##### P1 (should fix)

- **Issue**: Confirmation step is inconsistent, increasing anxiety post-payment
  - **Where**: Post-submit confirmation
  - **Why it matters**: Users may duplicate purchases or contact support unnecessarily
  - **Proposed fix**:
    - Always show confirmation with order summary + receipt path + “what happens next”
    - If delayed, show a **processing** state with expected timing + support path
  - **Risk / trade-off**: More UI states to maintain; ensure copy is localized
  - **How to verify**:
    - Support ticket volume for “did my order go through?”
    - Duplicate order rate (if measurable)

##### P2 (nice to have)

- **Issue**: Shipping step could reduce cognitive load for first-time users
  - **Where**: Shipping form
  - **Why it matters**: Minor slowdowns accumulate; address validation can feel punitive
  - **Proposed fix**: Inline validation + clearer field grouping + “why we need this” microcopy for phone number
  - **How to verify**:
    - Field error rate + time-on-step

#### Quick wins

- Improve payment error copy + recovery actions (same sprint)
- Add always-on confirmation shell with loading state (small eng lift, big anxiety reduction)

#### Open questions / assumptions

- **Assumption**: “Something went wrong” maps to multiple underlying causes; needs error taxonomy from engineering/payments
- **Open question**: Are users mostly mobile web? (Could change layout priorities)

#### Test plan / validation

- **Usability check**: 5–8 moderated sessions focused on forced payment failures + slow confirmation
- **Success signals**:
  - Payment step completion ↑
  - Retry success ↑
  - Support contacts for payment/confirmation ↓
- **Edge cases**:
  - International cards, 3DS flows, ad blockers, network timeouts

---

## Scenario B (messy inputs): vague “the app feels slow”

### Prompt (user)

“Our app feels slow. Audit it.”

### Inputs provided (user)

- No screenshots, no flow, no metrics

### Golden output (model)

#### Assumptions (minimal)

- **Assumption**: “Slow” might mean latency, heavy UI, confusing waits, or perceived performance (animations/layout shift)

#### What I can / can’t do without inputs

- I can’t credibly audit specific screens without **screens**, **a screen recording**, or **a defined flow + steps**.

#### Highest-value next inputs (pick any)

- **Screenshots** of the slow moments + the step before/after
- **A 60s screen recording** with actions labeled (“tap here → wait”)
- **Performance context** (device, OS, network), if known

#### Immediate triage checklist (generic)

- **Perceived performance**: skeletons vs spinners; layout shift; long blocking tasks on navigation
- **Feedback loops**: button disabled states; optimistic UI risks; timeout handling
- **Content weight**: oversized images/fonts; unnecessary rerenders (engineering follow-up)

#### Test plan / validation (once inputs arrive)

- Define **2–3 critical journeys** and measure time-to-interactive + time-to-primary action
- Add lightweight UX metrics: rage taps, repeated submits, abandonment by step
