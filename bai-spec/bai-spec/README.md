# BAI e-Treasurer · Phase 1 (Citizen App) · Cursor Spec Pack

Drop this folder into the project root next to `index.html`. Tell Cursor:

> "Read every file in `/bai-spec` before writing code. `index.html` is the approved design. Reuse its tokens, classes and components. Never invent new colours, fonts, radii or button styles. Build one screen at a time from `04-screens/`."

## What's in scope (Phase 1 = citizen-facing only)
Phase 2 (e-Commissioner, staff who create tickets) and Phase 3 (employee package / control panel) are **out of scope**. The control panel is where each county's menu gets switched on/off later, so build the nav as config now (see `county.config.json`).

## Files
| File | Purpose |
|---|---|
| `00-design-system.md` | Tokens + existing components from `index.html`. The rulebook. |
| `01-information-architecture.md` | Modules, master side nav, per-county config, access model |
| `02-user-flows.md` | 9 journeys, step by step, mapped to screen IDs |
| `03-component-library.md` | 24 reusable components with props and states |
| `04-screens/*.md` | One ready-to-paste Cursor prompt per screen group |
| `05-open-questions.md` | What the PM must confirm with BAI |
| `county.config.json` | Master nav + per-county toggles, labels, fees, access rules. Counties: demo, culpeper, mecklenburg, marion. |

## Build order (recommended)
1. Config-driven sidebar (`county.config.json`) + global cart button
2. Shared commerce: Cart → Payment method → Card / eCheck → Receipt (built once, used by every service)
3. Real Estate Tax (public pattern) → Personal Property Tax (private pattern)
4. Everything else is a re-skin of steps 2–3
