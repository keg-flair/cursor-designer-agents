# Golden examples — `analytics-insights`

## Scenario A (happy path): signup funnel with definitions

### Prompt (user)

“Given this funnel, identify the biggest leak, propose ranked UX hypotheses (with mechanism), fastest tests, and instrumentation gaps.”

### Inputs provided (user)

- **Time window**: Last 30 days
- **Segment**: All users, logged-out
- **Funnel**:
  1. `landing_view` → 100,000
  2. `signup_page_view` → 40,000  (40% step rate vs landing)
  3. `signup_start` → 10,000       (25% step rate vs signup page)
  4. `signup_complete` → 6,000     (60% step rate vs start)

**Definitions (provided)**

- Steps counted as unique sessions per day (engineering-confirmed)
- `signup_start` fires on first field focus in the signup form

### Golden output (model)

#### 1) What we know (from provided data)

- **Time window**: Last 30 days
- **Segment**: Logged-out, all users
- **Funnel / steps**: landing_view → signup_page_view → signup_start → signup_complete
- **Biggest leak**: `signup_page_view` → `signup_start` (75% of users who reach the page never start the form)
- **Notes on definitions**: Unique sessions/day; start = first field focus

#### 2) Top hypotheses (ranked)

##### 1)

- **Hypothesis**: If we reduce perceived effort and clarify why signup is needed on the signup page, `signup_start` will increase because users will understand value before interacting.
- **Mechanism**: Users bounce when the page reads like a wall of requirements without a compelling reason to continue.
- **Where in the flow**: Between `signup_page_view` and `signup_start`
- **Expected signal**: `signup_start / signup_page_view` ↑ with stable `signup_complete / signup_start`
- **Confidence**: Medium (fits the shape; needs qualitative + instrumentation checks)
- **Fastest test**:
  - On-page microcopy test + “primary job-to-be-done” header variant (A/B)
  - 5 usability sessions: “try to sign up” with think-aloud on first 20 seconds
- **Risks / trade-offs**: Stronger persuasion copy can feel salesy; may hurt trust if overpromising

##### 2)

- **Hypothesis**: If first-interaction latency/bugs on the signup page are reduced, `signup_start` will increase because users can successfully focus/interact with fields.
- **Mechanism**: JS errors, slow hydration, or overlapping UI can prevent first field focus from firing reliably—or discourage interaction.
- **Where in the flow**: `signup_page_view` → `signup_start`
- **Expected signal**: `signup_start` ↑ correlated with lower client errors / faster TTI on that page
- **Confidence**: Low–Medium (possible, but not evidenced in the numbers alone)
- **Fastest test**:
  - Error monitoring slice for signup page route
  - Performance trace on p75 mobile for that page
- **Risks / trade-offs**: Engineering-heavy; may uncover non-UX root causes

##### 3)

- **Hypothesis**: If CTA placement/affordance from landing → signup is misaligned, many `signup_page_view` sessions are exploratory and not intentful signups—tightening entry paths will change the mix and improve start rate.
- **Mechanism**: Users open signup to “peek,” then leave once they see requirements.
- **Where in the flow**: upstream of `signup_page_view` (still shows up as leak to start)
- **Expected signal**: Lower volume but higher `signup_start / signup_page_view` (not always “good”; depends on growth goals)
- **Confidence**: Low (needs referrer/intent segmentation)
- **Fastest test**:
  - Segment by entry source (if available): landing CTA vs footer link vs ads
- **Risks / trade-offs**: Optimizing for start rate could reduce top-of-funnel traffic quality

#### 3) Instrumentation gaps (blockers to confidence)

- Missing **referrer/entry CTA** attribution on `signup_page_view` (can’t separate peek vs intent)
- Missing **client error** tagging correlated with session id on signup page
- Missing **performance markers** (TTI / first input delay) tied to funnel steps
- Unclear whether `signup_start` is reliable if users use autofill (focus events may undercount)

#### 4) Next analyses (cheap, decisive)

- Break `signup_page_view → signup_start` by **device**, **browser**, **geo**, **entry source**
- Compare users who **scroll** vs not (if scroll depth exists) vs start rate
- Cohort by **campaign** (if UTMs exist): identify low-start segments with high page views

#### Test plan / validation

- Ship one copy/layout variant with a clear primary metric: `signup_start / signup_page_view`
- Guardrail: `signup_complete / signup_start` should not fall (catch “started but can’t finish” regressions)

---

## Scenario B (messy inputs): “big drop after signup” with no definitions

### Prompt (user)

“We have a big drop after signup. Thoughts?”

### Golden output (model)

#### 1) What we know (from provided data)

- **Time window**: Unknown
- **Segment**: Unknown
- **Funnel / steps**: Unknown (what exactly counts as “after signup”?)
- **Biggest leak**: Cannot be identified from the statement alone
- **Notes on definitions**: Missing (session vs user, device, event definitions)

#### 2) Top hypotheses (ranked) — explicitly low confidence

##### 1)

- **Hypothesis**: The drop is caused by a **post-signup activation** gap (users sign up but don’t reach first value action).
- **Mechanism**: Empty states, unclear next step, missing guidance, or verification walls.
- **Where in the flow**: Unknown until funnel steps are defined
- **Expected signal**: Activation metric ↑ if onboarding is fixed
- **Confidence**: Low (plausible generic mechanism; no evidence yet)
- **Fastest test**: Define the **first value moment** event and measure 7-day activation by segment
- **Risks / trade-offs**: “Activation” definitions can be politically contentious—align stakeholders first

#### 3) Instrumentation gaps

- Need the exact funnel events + denominators + timeframe + segment
- Need whether “signup” means account created, email verified, or profile completed

#### 4) Next analyses (cheap, decisive)

- Paste the funnel table + definitions; add **step-to-step conversion** view (not just raw counts)

#### Test plan / validation

- Once the funnel is defined, re-run hypothesis ranking with confidence tied to evidence
