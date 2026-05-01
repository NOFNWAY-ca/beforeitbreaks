# AGENTS.md

## What This Directory Is

Client work. Each subdirectory is a separate client project. All projects follow the same pattern: bespoke single-file HTML tools delivered directly to clients.

## Projects

| Directory | Client | Status |
|---|---|---|
| `terracomm/` | TerraComm Inc. (Erik) | May be in active use -- confirm before changing |
| `septic-dispatch/` | Septic Dispatch demo | Generic demo app, no live client |
| `mcmahon-ranch/` | McMahon Ranch | Existing single-file app |
| `Take Pride/` | TBD | Empty, not started |

Each project has its own `AGENTS.md` and `lessons.md`. Read those before touching anything in that subdirectory.

## Universal Constraints

- One HTML file per project. Client receives a single file that opens in any browser.
- No frameworks, no build step, no external dependencies.
- All data stays local (localStorage or CSV export) -- nothing leaves the browser.
- Delivery is direct file handoff, not deployment.

## How a Build Session Works
The user will paste a Project Brief. It contains everything needed to build the app -- tabs, data fields, business rules, colours, fonts, sample data. Read the entire brief before writing any code. If anything is ambiguous or missing, ask before starting -- do not invent answers.

## HTML App Standards

### Structure
- Single file. All CSS, JS, and HTML in one `.html` file.
- Google Fonts via `<link>` tag is the only external dependency allowed.
- All data lives in localStorage. Key prefix = short client name, e.g. `sd_` for Septic Dispatch.
- No frameworks. Vanilla JS only.

### CSS
- Always use CSS custom properties (variables) for all colours, defined in `:root`.
- Font stack: one display/heading font (Oswald, Barlow, Laila, etc.) paired with one body font (Source Sans 3, DM Sans, etc.). Match to brand tone.
- Never use Inter, Roboto, Arial, or system-ui as primary fonts.
- Mobile-first. Every view must work on a phone screen.
- Sticky header with nav tabs. Tab content in `.page` divs shown/hidden with `.active` class.

### JavaScript
- All data stored as JSON in localStorage.
- On first load, if localStorage is empty, seed with the sample data from the brief.
- Functions grouped by section with clear `// -- SECTION NAME --` comments.
- No jQuery, no lodash, no external JS.
- Modals for add/edit forms. Overlay + modal pattern (see reference apps in this directory).

### Design Rules
- Colour scheme, fonts, and tone come from the Project Brief. Do not substitute.
- Header: dark brand colour, company wordmark left, nav tabs right.
- Nav active tab: bottom border in accent colour.
- Tables: dark header row in primary brand colour, white text, hover highlight on rows.
- Buttons: primary = solid brand colour. Secondary = ghost/outline. Destructive = soft red.
- Stat/summary cards at top of data-heavy tabs.
- All form inputs inside modals, not inline in tables.

### Hard Limits
- Do not add features not listed in the brief.
- Do not add a login/auth system unless the brief explicitly requires it.
- Do not add animations beyond simple CSS transitions on buttons and modals.
- Do not use `alert()` or `confirm()` -- use inline UI feedback instead.
- Do not leave any tab empty on first load -- seed data must make every section feel real.

## Delivery
Output the complete `.html` file into the client subdirectory. One-line summary of what was built and any decisions made that weren't in the brief. Update the project's `lessons.md` with anything that came up during the build that future sessions should know.

## Agent Sync

- Each client project should have a `SYNC.md`.
- Read that file before making changes, then update it after meaningful work so Codex and Claude stay in sync automatically.

## Reference Apps
`take-pride.html` and `TerraComm_TimeTracker_V2.html` are in this directory as permanent
style and structure references. Read both before starting any new client build.
