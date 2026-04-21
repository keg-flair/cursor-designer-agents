# Golden examples — `component-spec-writer`

## Scenario A (happy path): `Toast` (web)

### Prompt (user)

“Write a component spec for `Toast`. Include anatomy/slots, variants, states, content rules, token hooks, a11y, theming, and a QA checklist. Call out invalid combinations.”

### Inputs provided (user)

- **Platforms**: Web
- **Theming**: Light + dark
- **Needs**: Optional action (Undo), queueing, critical vs non-critical semantics

### Golden output (model)

#### Overview

- **Component name**: `Toast`
- **Purpose / user value**: Lightweight, transient feedback about a background outcome without blocking the page
- **Non-goals**:
  - Not a modal decision surface (use `Dialog` / `Modal`)
  - Not for long-form content (use `InlineAlert` / `Banner`)
- **Platforms**: Web

#### Anatomy / slots

- **Container**: holds layout, elevation, and dismiss affordance region
- **Icon slot** (optional but recommended for semantics): success/warning/error/info
- **Title** (optional): short label
- **Body**: 1–2 lines max by default; truncation rules apply
- **Actions slot** (optional): 0–1 primary action (e.g., Undo); avoid two competing primaries
- **Dismiss control** (optional): icon button; must not be the only way critical info is communicated

#### Variants

- **Semantic variants**: `info`, `success`, `warning`, `error`
- **Placement**: `bottom-right` (default), `top-center` (optional system choice)
- **Queue behavior**: `replace-latest` vs `stack` (pick one as default; document)

#### Variant matrix (compact)

| Variant | Icon | Action | Typical use |
| --- | --- | --- | --- |
| `info` | recommended | optional | neutral background outcomes |
| `success` | recommended | optional | completed actions |
| `warning` | recommended | optional | recoverable issues |
| `error` | required | recommended | failed actions / requires attention |

#### States

- **Default**: visible, auto-dismiss timer running (if enabled)
- **Hover / Focus**: dismiss + action are keyboard reachable; focus ring visible
- **Paused**: timer pauses on hover/focus within toast (optional but recommended for accessibility + reading)
- **Loading** (optional): only if toast represents an in-flight process; prefer progress UI elsewhere if long-running

#### Behavior

- **Duration**:
  - Default auto-dismiss: tuned by variant (`error` longer than `success`)
  - Critical `error` may be **persistent** until dismissed (product policy)
- **Queueing**:
  - If `stack`, define max visible count + overflow behavior (“+3 more” pattern vs priority queue)
- **Motion**:
  - Enter/exit transitions respect reduced motion (no essential information conveyed by motion alone)

#### Theming + token hooks

- **Surface**: `toast.surface`
- **Border**: `toast.border`
- **Text**: `toast.text.title`, `toast.text.body`
- **Icon colors**: `toast.icon.info|success|warning|error`
- **Elevation**: `toast.elevation`
- **Spacing**: `toast.padding.x`, `toast.padding.y`, `toast.gap.iconText`
- **Radius**: `toast.radius`
- **Focus ring**: `focus.ring.color`, `focus.ring.width`

#### Accessibility

- **Role/live region** (implementation guidance): use appropriate live politeness; avoid spamming polite announcements for high-frequency events
- **Keyboard**:
  - Action is reachable
  - Dismiss is reachable
  - Focus management policy when toast appears (avoid stealing focus for non-blocking success toasts)
- **Color**: semantic meaning not conveyed by color alone (icon + text)

#### Invalid combinations

- Two primary actions (“Retry” + “Undo”) competing without hierarchy
- `success` styling used for destructive irreversible actions
- Auto-dismiss on `error` without an obvious recovery path (unless policy explicitly allows)

#### QA checklist

- [ ] Variant/state coverage (including dark mode)
- [ ] Long strings: truncation + wrapping rules don’t clip actions
- [ ] Keyboard path for dismiss/action; visible focus
- [ ] Live region behavior: no noisy duplicate announcements
- [ ] Reduced motion path verified
- [ ] Queue behavior verified under rapid events

#### Test plan / validation

- **Design QA**: token swap across themes; verify icon + text parity
- **Eng QA**: keyboard + SR spot checks on dismiss/action paths
- **Analytics** (optional): toast shown/dismissed/acted upon (avoid PII in labels)

---

## Scenario B (messy inputs): “Spec Button” with no context

### Prompt (user)

“Write a spec for `Button`.”

### Inputs provided (user)

- Component name only

### Golden output (model)

#### What I need to write a high-quality spec (minimum)

- **Primary use cases** (3–5): e.g., form submit, destructive confirm, navigation, icon-only toolbar
- **Non-goals**: what `Button` should explicitly not be used for in your system
- **Platforms + frameworks** (if relevant): web vs native differences
- **Theming constraints**: brand colors, dark mode, token names you already use

#### Draft spec skeleton (still useful)

- **Variants**: `primary`, `secondary`, `tertiary`, `destructive` (+ `ghost` if you have it)
- **Sizes**: `sm`, `md`, `lg`
- **States**: default/hover/pressed/focus/disabled + loading (if supported)
- **Content rules**: max label length; icon + label rules; icon-only labeling requirements
- **Accessibility**: focus, disabled semantics (prefer `aria-disabled` pattern if you disable clicks but keep tooltips—policy dependent)
- **Invalid combinations**: destructive styled as primary without confirm pattern (system policy)

#### Test plan / validation

- Once use cases arrive, validate the variant matrix against real screens (forms, modals, tables, empty states)
