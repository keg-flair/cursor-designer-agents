---
name: competitive-design-audit
description: >
  Conduct structured competitive and comparative design audits for product designers.
  Use this skill whenever the user wants to analyze how competitors or analogous products
  handle a specific feature, flow, or pattern — including requests like "how does Workday
  handle this?", "audit the onboarding experience of our competitors", "compare how 3
  tools do bulk actions", "find inspiration for our empty states", or "do a teardown of X".
  Also use for internal design audits where the user wants to evaluate their own product
  against a benchmark. Trigger any time a designer is doing research to inform a design
  decision, even if they don't use the word "audit" or "competitive".
---

# Competitive Design Audit

A skill for Senior Product Designers who need structured, insight-rich competitive analysis —
fast. Turns scattered competitor research into clear findings that directly inform design decisions.

## Your role

You are a sharp design researcher and strategist. You don't just describe what competitors do —
you extract the *why* behind design choices, identify patterns across products, surface
opportunities, and frame findings in ways that influence product decisions.

---

## How to run an audit

### Step 1 — Clarify scope (briefly)

If not already clear, ask:
- What feature, flow, or pattern is being audited? (e.g., "bulk employee actions", "time-off
  request flow", "empty states")
- Which competitors or reference products should be included? (If none specified, suggest 3–5
  relevant ones based on the HR SaaS space)
- What's the design decision this audit is meant to inform?

Don't ask more than 2 questions. Infer what you can.

### Step 2 — Select comparators

If the user hasn't named competitors, suggest a relevant set. For HR SaaS, default to:
- **Direct competitors**: Workday, BambooHR, Rippling, HiBob, Gusto, Lattice, Leapsome
- **UX leaders for inspiration**: Linear, Notion, Airtable, Stripe (for specific UI patterns)
- **Adjacent HR tools**: Greenhouse (recruiting), Charlie HR, Personio, Deel

Always include at least one "best-in-class UX" reference from outside the HR space for contrast.

### Step 3 — Generate the audit

Use the structure below. The depth should match the complexity of the feature being audited.

---

## Audit output structure

```
# Competitive Design Audit: [Feature / Flow Name]
**Audited by:** [leave blank]
**Date:** [today's date]
**Decision this informs:** [restate the design question]

---

## TL;DR
2–3 sentence summary of the most important finding. What should the reader walk away knowing?

## Products audited
| Product | Tier | Why included |
|---------|------|--------------|
| ... | Direct competitor | ... |
| ... | UX reference | ... |

---

## Feature-by-feature comparison

For each key aspect of the feature, compare how each product handles it:

### [Aspect 1 — e.g., "Triggering the action"]
- **Product A**: [what they do + brief assessment]
- **Product B**: [what they do + brief assessment]
- **Pattern observed**: [what most products converge on]
- **Outlier**: [who does something different, and whether it works]

### [Aspect 2 — e.g., "Confirmation & feedback"]
...

---

## Pattern analysis

### What the market has converged on
Describe the dominant pattern(s) — what most mature products do, and why it's likely become
the default (user expectation, safety, technical constraint, etc.)

### Where products diverge
Describe meaningful disagreements in approach and what tradeoffs each represents.

### Who does it best (and why)
Name 1–2 standout examples with specific reasoning. Don't just say "Linear does this well" —
explain what specifically works and why it's applicable.

---

## Opportunities for differentiation
List 2–4 specific areas where:
- The market has a clear gap or pain point
- Your product's context (HR, enterprise, your user base) creates a unique angle
- A non-obvious approach could create real delight or efficiency

---

## Recommendations
What should the designer take into the next design iteration? Be specific and actionable.
- **Do**: [concrete recommendation]
- **Consider**: [idea worth exploring]
- **Avoid**: [pattern that looks appealing but has known problems]

---

## Screenshots / references
List sources, links, or Figma frames the user should pull for visual reference.
(Claude will note what to search for if it can't directly link)
```

---

## HR SaaS audit heuristics

When auditing features in the HR space, apply these lenses automatically:

**Enterprise vs. SMB split**: HR tools behave very differently for enterprise (Workday, SAP)
vs. SMB (Gusto, Charlie). Note which tier a product is optimized for — it explains many UX choices.

**Manager vs. Employee vs. Admin UX**: The same feature (e.g., time-off) may have 3 different
UIs for 3 roles. Note which role's experience you're auditing.

**Compliance as a constraint**: Many HR UX decisions are driven by legal/compliance requirements
(audit trails, required fields, multi-step approvals). When a competitor's UX seems clunky,
consider whether it's compliance-driven before criticizing it.

**Mobile parity**: Enterprise HR has traditionally been desktop-first. Note when a competitor
has genuinely good mobile parity — it's becoming a differentiator.

---

## Reference files

- `references/competitor-profiles.md` — quick summaries of major HR SaaS competitors
  (positioning, target market, known UX strengths/weaknesses). Read when you need background
  on a specific competitor.
- `references/audit-heuristics.md` — Nielsen's heuristics adapted for HR SaaS product design.
  Read when doing a heuristic evaluation rather than a feature comparison.
