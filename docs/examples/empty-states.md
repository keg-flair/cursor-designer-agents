# Golden examples — `empty-states`

## Scenario A (happy path): “Employee list” empty + error states (web)

### Prompt (user)

“Create an empty/loading/error state plan for our employee list screen. Include copy patterns, recovery actions, a11y notes, token hooks, and a QA checklist.”

### Inputs provided (user)

- **Platform**: Web
- **Surface**: Employee list (table + filters)
- **Primary user goal**: Find an employee quickly and take an action (view profile, update status)
- **Constraints**: Must be keyboard accessible; supports filters + search; has permissions (Admin vs Manager)

### Golden output (model)

#### Summary

- **Surface**: Employee list screen (table + filters)
- **Primary user goal**: Find an employee quickly and take an action
- **Constraints**: keyboard accessible, role-based permissions, filters/search

#### State taxonomy

- **No data ever**: Company has 0 employees loaded (new org)
- **No results**: Filters/search return none (but org has employees)
- **No access**: User lacks permission to view employees
- **Unavailable**: Service error / maintenance

#### State matrix (core)

| State | Trigger | User message (headline + body) | Primary action | Secondary action | System behavior | A11y notes |
| --- | --- | --- | --- | --- | --- | --- |
| Loading | initial page load | **Loading employees** / “This usually takes a few seconds.” | n/a | n/a | Skeleton rows + filter controls disabled until ready | Respect reduced motion; announce loading via non-intrusive status |
| Empty: first-time | 0 employees in org | **No employees yet** / “Add your first employee to get started.” | Add employee | Import CSV | Show brief “what you can do here” bullets | Focus stays on page heading; actions are keyboard reachable |
| Empty: no results | query returns 0 | **No results** / “Try clearing filters or searching by email.” | Clear filters | Edit search | Preserve query/filter chips; show count = 0 | Announce updated results count; don’t clear user input automatically |
| Error: retryable | 5xx / timeout | **We couldn’t load employees** / “Check your connection and try again.” | Retry | Contact support | Preserve filters/search; exponential backoff; show error code (optional) | Move focus to error summary region; ensure Retry is first tab stop |
| Error: permission | 403 / role | **You don’t have access** / “Ask an admin to grant Employee Directory access.” | Request access | Back | Don’t show empty table; explain role context | Avoid blaming language; ensure message is programmatically associated with heading |

#### Copy patterns

- **Empty (first-time)**: “No X yet” + one sentence explaining value + clear next action.
- **No results**: name the current constraints (“0 results for ‘Acme’”) + preserve context + offer fast escape hatch (“Clear filters”).
- **Errors**: safe explanation + what user can do now + what the system did (preserved inputs, retry policy).

#### Recovery policy

- **Retry**: preserves filters/search; retries only the data request; shows “Last updated” on success.
- **Escalation**: after 2 failed retries, offer “Contact support” with an error reference.

#### Design system hooks (token-first)

- **Surface**: empty-state container surface + elevation tokens
- **Text**: headline/body semantic text tokens
- **Status**: warning/error icon + border tokens
- **Motion**: reduced-motion variant uses fade only, no slide

#### QA checklist

- [ ] “No results” preserves filters/search and offers Clear filters
- [ ] Retry preserves user context; focus moves to error summary
- [ ] Keyboard-only path can reach primary action in each state
- [ ] Reduced motion path avoids attention-grabbing transitions

