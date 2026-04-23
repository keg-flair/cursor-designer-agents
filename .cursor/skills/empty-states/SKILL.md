---
name: empty-states
description: Produces an implementation-aware empty/loading/error/success state plan for a screen, flow, or component, including recovery policy, instrumentation prompts, accessibility, and token hooks. Use when the user asks “what happens when there’s no data / slow network / failure?” or wants a state matrix.
---

# Empty / Loading / Error States

Shared conventions:
- House style: `docs/HOUSE_STYLE.md`
- Cursor enforcement: `.cursor/rules/`

## Defaults

- **Ship-ready**: include triggers, UI behavior, recovery actions, and verification plan.
- **State taxonomy**: explicitly distinguish “new user empty” vs “no results” vs “no access”.
- **Recovery-first**: no dead ends; every failure offers a best next action.
- **A11y baseline**: focus, announcements, labels, reduced motion.

## Constraints

- **Do not invent** backend error codes or business rules as fact; label assumptions.
- Ask **at most 3 clarifying questions** (only if it changes which states exist or the recovery policy).

## Clarifying questions (ask max 3)

1. What is the **surface** (component/screen/flow) and critical task?
2. Which failure modes matter: validation, permissions, network/offline, server, partial failure?
3. Is there a **success metric** (drop-off, retries, support contacts) we should optimize?

## Inputs to request (only if missing)

- Screenshots/Figma link + which step(s) the states apply to
- “Empty” definitions: zero items vs no results vs first-time user
- Constraints: localization, compliance/trust, theming, offline support

## Method

1. Define the **state taxonomy** (what “empty” means).
2. Build the **state matrix** with triggers, actions, and system behavior.
3. Define **recovery policy** (retry/undo/escalation).
4. Add **token hooks** by intent and **a11y** requirements.
5. Add a lightweight **verification plan** (what to test, what to measure).

## Output template

```markdown
## State plan: [Surface name]

### Assumptions / constraints
- …

### State taxonomy (define “empty”)
- **No data ever** (new user / zero items):
- **No results** (filters/search yield none):
- **No access** (permission/role):
- **Unavailable** (service down / maintenance):

### State matrix
| State | Trigger | UI behavior | Copy (headline + body) | Primary action | Secondary action | A11y | Instrumentation (optional) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Loading | … | skeleton/spinner + timeout policy | … | n/a | n/a | reduced motion + announcements | … |
| Empty: first-time | … | education + examples | … | Create/Add | Learn more | heading/focus | … |
| Empty: no results | … | preserve query/context | … | Clear filters | Adjust search | announce count | … |
| Error: retryable | … | preserve inputs; backoff | … | Retry | Contact support | focus to summary | … |
| Error: validation | … | inline + summary policy | … | Fix inputs | n/a | labels/assoc | … |
| Error: permission | … | explain why + next steps | … | Request access | Back | no dead ends | … |
| Success/confirmation | … | toast/inline summary | … | View item | Undo (if possible) | don’t steal focus | … |

### Recovery policy
- **Retry**: what is preserved vs reset
- **Undo**: eligibility + time window
- **Escalation**: when to suggest support, status page, or later retry

### Design system hooks (token-first)
- Surface/text/border/icon/status/focus/motion/elevation/spacing/radius tokens

### Test plan / verification
- **Design QA**: density/themes/long strings
- **Engineering QA**: keyboard/focus/announcements; offline/timeout
- **Metrics to watch** (if applicable): retries, recovery success, support contacts
```

