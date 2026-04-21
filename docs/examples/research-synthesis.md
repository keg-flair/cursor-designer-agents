# Golden examples — `research-synthesis`

## Scenario A (happy path): checkout interviews (synthetic notes)

### Prompt (user)

“Cluster these notes into themes, produce insights and opportunities, include evidence snippets, and turn insights into falsifiable hypotheses with success signals.”

### Inputs provided (user)

**Study goal**: Understand why first-time buyers hesitate at payment  
**Participants**: 8 recent first-time buyers (synthetic personas for this example)

**Raw notes (verbatim snippets)**

- P3: “I clicked pay and it just said ‘something went wrong’—I didn’t know if it charged me.”
- P1: “I hate entering my address again; I thought it would autofill.”
- P5: “The shipping options looked the same price but different days—I wasn’t sure which to pick.”
- P2: “I couldn’t tell if the discount applied.”
- P7: “After paying I got a blank screen for a second—I refreshed, scared I’d double pay.”

### Golden output (model)

#### Study context

- **Study goal**: Understand hesitation/failure at payment + post-submit anxiety for first-time buyers
- **Participants / segment**: First-time buyers (n=8)
- **Method**: Interviews (synthetic example)
- **Key constraints**: Web checkout; payment errors are opaque today

#### Themes (clusters)

##### Theme 1: **Payment failure recovery is opaque**

- **What we heard**: Users cannot tell whether money left their account when errors occur.
- **Evidence snippets**:
  - “I clicked pay and it just said ‘something went wrong’—I didn’t know if it charged me.”

##### Theme 2: **Price/discount confidence breaks trust**

- **What we heard**: Users struggle to confirm discounts applied and compare shipping value.
- **Evidence snippets**:
  - “I couldn’t tell if the discount applied.”
  - “The shipping options looked the same price but different days—I wasn’t sure which to pick.”

##### Theme 3: **Post-submit anxiety (“did it work?”)**

- **What we heard**: Even brief uncertainty triggers refresh/double-submit fears.
- **Evidence snippets**:
  - “After paying I got a blank screen for a second—I refreshed, scared I’d double pay.”

#### Insights (so what)

- **Insight**: Opaque payment errors create a **trust cliff** at the highest-risk moment.
  - **Why it matters**: Users can’t form a mental model of “charged vs not charged,” so they abort or flood support.
  - **Who it affects**: First-time buyers + higher-risk payment methods
  - **Supporting evidence**: P3 quote

- **Insight**: Users need **confirmable price narratives** (discount + shipping value) before committing.
  - **Why it matters**: Indecision increases time-on-step and amplifies second-guessing at payment
  - **Supporting evidence**: P2 + P5 quotes

#### Opportunities (now what)

- **Opportunity**: Payment error taxonomy + recovery UI
  - **Approach**: Categorized errors + safe messaging + explicit next actions + preserve non-sensitive inputs
  - **Risks / trade-offs**: Too much detail can confuse; needs legal/payments review

- **Opportunity**: “Price story” module on review step
  - **Approach**: Show discount as line items + “you save X” + compare shipping by total delivered date (not just price)
  - **Risks / trade-offs**: UI density; localization formatting

#### Hypotheses + success signals

- **Hypothesis**: If we replace generic payment errors with categorized recovery paths, checkout completion will increase because users can confidently retry without fearing double charges.
  - **Success signals**:
    - Payment step completion ↑
    - Retry success ↑
    - “Double charge” support themes ↓

- **Hypothesis**: If we show an explicit discount breakdown + shipping comparison framed by arrival date, time-on-shipping/payment will decrease because users can decide faster.
  - **Success signals**:
    - Shipping step duration ↓
    - Payment abandonment ↓

#### Open questions / follow-ups

- What are the top 5 underlying payment error codes today (engineering)?
- What is the actual incidence of duplicate orders / refresh-after-pay (analytics)?

#### Test plan / validation

- Moderated usability with forced failures + delayed confirmation
- Quant A/B on error copy + recovery paths (if feasible)

---

## Scenario B (messy inputs): bullet fragments, no study goal

### Prompt (user)

“Synthesize:”

- “annoying”
- “too many steps”
- “not sure it worked”

### Golden output (model)

#### Assumptions

- **Assumption**: These are informal notes from a usability session or internal feedback, but **method + segment are unknown**.

#### What’s missing (minimum to synthesize credibly)

- **Study goal**
- **Who** (persona/segment)
- **Where in the product** (flow step)
- **Verbatim notes** (even rough) tied to participants/tasks

#### Provisional clusters (low confidence)

- **Theme A (low confidence)**: **Friction / too heavy** (“too many steps”)
- **Theme B (low confidence)**: **Outcome uncertainty** (“not sure it worked”)
- **Theme C (low confidence)**: **Emotional signal without mechanism** (“annoying”)

#### Next step

- Paste **5–10 more snippets** with task context (what they were trying to do), and label each snippet with **participant ID + step**.

#### Test plan / validation

- Once richer notes exist, rebuild themes and mark confidence as High only where repeated across participants
