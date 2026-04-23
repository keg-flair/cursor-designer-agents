## Empty/loading/error states template (copy/paste)

### Summary

- **Surface**: (screen / flow / component)
- **Primary user goal**:
- **Constraints**: (a11y, localization, compliance/trust, offline, theming)

### State taxonomy

- **No data ever** (new user / zero items):
- **No results** (filters/search yield none):
- **No access** (permission/role):
- **Unavailable** (service down / maintenance):

### State matrix

| State | Trigger | User message (headline + body) | Primary action | Secondary action | System behavior | A11y notes |
| --- | --- | --- | --- | --- | --- | --- |
| Loading |  |  |  |  |  |  |
| Empty: first-time |  |  |  |  |  |  |
| Empty: no results |  |  |  |  |  |  |
| Error: retryable |  |  |  |  |  |  |
| Error: validation |  |  |  |  |  |  |
| Error: permission |  |  |  |  |  |  |
| Success/confirmation |  |  |  |  |  |  |

### Copy patterns

- **Empty**:
- **Error**:
- **Loading**:

### Recovery policy

- **Retry**:
- **Undo**:
- **Escalation**:

### Design system hooks (token-first)

- **Surface/text/border/icon/status/focus/motion**:

### QA checklist

- [ ] Filtered empty vs true empty handled
- [ ] Recovery paths exist (no dead ends)
- [ ] Copy is localizable and robust to long strings
- [ ] Keyboard + focus + announcements verified
- [ ] Reduced motion verified

