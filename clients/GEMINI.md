# GEMINI.md — Client Projects context

This file provides guidance to Gemini CLI when working in the `beforeitbreaks/clients/` directory.

## What This Directory Is

Bespoke single-file HTML tools for small business clients. Each subdirectory is a separate project.

## Universal Project Constraints

- **Single File:** Deliver one `.html` file containing all CSS, JS, and HTML.
- **No Frameworks:** Vanilla JS only. No build steps.
- **No External Dependencies:** Google Fonts via `<link>` is the only exception.
- **Local-Only Data:** All data remains in `localStorage` or CSV export.
- **Privacy:** Nothing leaves the browser. No auth systems unless explicitly required.

## Build Standards

### Structure & CSS
- Mobile-first design.
- Sticky header with navigation tabs.
- CSS variables for all colors in `:root`.
- Font stack must match the Project Brief (avoid standard system fonts like Inter/Arial).

### JavaScript
- Use `localStorage` with a project-specific prefix (e.g., `tc_` for TerraComm).
- Seed initial load with sample data from the brief.
- Use modals for all add/edit forms.
- No `alert()` or `confirm()`; use inline UI.

### Workflow
- Read the entire Project Brief before coding. Ask questions if ambiguous.
- Follow the Project Brief's color scheme and tone exactly.
- Group JS functions with clear `// -- SECTION NAME --` comments.

## Delivery & Sync

- Output the complete `.html` file to the project directory.
- Update the project's `SYNC.md` after any work.
- Add long-term learnings to `lessons.md`.
- Reference `take-pride.html` and `TerraComm_TimeTracker_V2.html` for style and structure.

## Active Projects
- `terracomm/`: Active time tracking tool.
- `septic-dispatch/`: Generic demo app.
- `mcmahon-ranch/`: Existing ranch management tool.
- `Take Pride/`: Planned/Pending.
