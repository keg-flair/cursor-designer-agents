# Golden examples — `competitive-design-audit`

## Scenario A (happy path): compare bulk actions patterns

### Prompt (user)

“Run a competitive design audit for bulk actions in a people directory table. Compare 3–5 relevant products plus one best-in-class reference. Summarize market patterns, trade-offs, opportunities, and give concrete recommendations.”

### Inputs provided (user)

- **Decision to inform**: Should we use a persistent bulk toolbar, a row-level action pattern, or an overflow-only pattern?
- **Comparators** (user-provided): Airtable, Notion, Rippling, BambooHR
- **Best-in-class** (suggested): Linear (for fast multi-select + command patterns)
- **Evidence**: no screenshots provided (audit will be pattern-level, not pixel-accurate)

### Golden output (model)

## Competitive design audit: Bulk actions in a directory table

### Assumptions / constraints

- No screenshots/links were provided, so findings are **pattern-level hypotheses** to verify, not definitive “what Product X does” claims.
- Constraint: Bulk actions must be safe (confirmation for destructive actions; clear affected count).

### Decision this informs

- Choose the primary bulk action model: **contextual toolbar** vs **row-level actions** vs **overflow-only**.

### TL;DR

- The market tends to converge on a **contextual bulk toolbar** once selection exists, because it reduces hunting and makes “scope + count” explicit. The best implementations pair it with strong safeguards (confirmation, undo) and clear selection scope (page vs all results).

### Products audited

| Product | Tier | Why included | Evidence |
| --- | --- | --- | --- |
| Airtable | Adjacent | power-user tables + bulk edits | not provided |
| Notion | Adjacent | multi-select + bulk ops patterns | not provided |
| Rippling | Direct/adjacent | HR/admin workflows | not provided |
| BambooHR | Direct/adjacent | people directory mental model | not provided |
| Linear | Best-in-class reference | fast selection + bulk operations | not provided |

### Comparison by aspect

#### Aspect 1: Entry point / discoverability

- **Pattern observed**: Selection creates a strong “mode switch” that unlocks bulk actions.
- **Trade-offs**:
  - Toolbar: high discoverability after first select; supports many actions
  - Overflow-only: clean UI but hides power; slower for repeat use
  - Row-level only: good for single-item actions; poor for true bulk workflows
- **Implication for us**: If bulk actions are common, optimize for speed after the first selection (toolbar or command pattern).

#### Aspect 2: Safeguards (confirmation, undo, scoping)

- **Pattern observed**: Destructive actions require explicit confirmation; best systems show **count + consequence**.
- **Trade-offs**:
  - Undo is great for reversible actions but can be hard for permissioned or multi-step operations
  - Cross-page selection increases power but increases risk; needs explicit scoping UI
- **Implication for us**: If we offer cross-page selection, we must invest in scoping and auditability.

#### Aspect 3: Feedback (processing, partial failures)

- **Pattern observed**: Bulk actions need robust feedback (processing states, partial failure summaries).
- **Trade-offs**:
  - “Instant success” toasts are simple but can mask partial failures
  - Detailed results improve trust but add UI complexity
- **Implication for us**: Provide a tiered approach: toast for success + expandable “details” for failures.

### Pattern analysis

- **What the market converges on (and why)**:
  - Contextual bulk toolbar is common because it externalizes state (“you’re in multi-select mode”) and keeps actions near the work.
- **Where products diverge (and what it implies)**:
  - Some systems prioritize UI cleanliness (overflow-only) at the cost of speed; others embrace power-user workflows (toolbar + keyboard shortcuts).
- **Who does it best (and why it works)**:
  - Best-in-class systems make selection + actions feel like one loop: select → act → feedback → recover.

### Opportunities for differentiation

- **Opportunity**: “Eligible subset” intelligence
  - **User value**: Selecting mixed-permission rows is common; show how many are eligible before action.
  - **Why competitors don’t do it**: Requires permission modeling + UI complexity.
  - **Risks / trade-offs**: Confusing if over-explained; needs careful microcopy.
  - **How to validate**: Track how often actions are blocked by permissions + measure reduced failure attempts.

- **Opportunity**: Recovery-first bulk operations
  - **User value**: Fewer support tickets and fear—provide Undo where possible + audit log for the rest.
  - **Risks / trade-offs**: Engineering cost; requires clear policy on reversibility.
  - **How to validate**: Compare completion rates + error recovery success.

### Recommendations

- **Do**: Implement a **contextual bulk toolbar** that appears on selection with clear count and action grouping (safe vs destructive).
- **Consider**: Add keyboard accelerators (optional) and a scoped “Select all results” only if your users truly need cross-page bulk ops.
- **Avoid**: Overflow-only bulk actions for frequent workflows; it will under-serve power users and slow teams.

### What to capture next (if evidence missing)

- For each product, capture:
  - How selection is initiated and indicated
  - Where bulk actions appear
  - Confirmation patterns for destructive actions
  - Feedback on partial failure + undo

---

## Scenario B (messy inputs): “How does X do it?” with no decision

### Prompt (user)

“How does Workday handle bulk actions?”

### Golden output (model)

### Clarify scope (max 2 questions)

1. What decision are you trying to make (toolbar vs overflow vs row-level, safety model, scoping)?
2. Which role experience matters (admin vs manager vs employee) and which platform (desktop vs mobile)?

### If unanswered, proceed with a useful default

- Provide a short checklist of what to look for in Workday:
  - How multi-select is entered/exited
  - Where actions live
  - Confirmation and audit trail cues
  - How permissions affect eligible rows

### Test plan / validation

- Ask the user to capture 5 screenshots for: default table, selection state, destructive confirm, success feedback, failure state.

