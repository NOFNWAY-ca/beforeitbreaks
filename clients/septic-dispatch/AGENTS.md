# AGENTS.md — Septic Dispatch

## Client Overview
Septic Dispatch is a generic demo app for septic tank pumping and portable toilet rental operations.
It is no longer tied to a live client. Keep branding neutral and operational.

## Who Uses This App
| Role | Name | Primary Use |
|---|---|---|
| Owner | Gerry | Scheduling, booking calls, all admin |
| Tank Driver A | TBD | Daily job list, route log, dump logging |
| Tank Driver B | TBD | Daily job list, route log, dump logging |
| PT Driver | TBD | Portable toilet deployments and pickups |
| Floating Driver | TBD | Pickups, deliveries, weekend rentals |
| Office / Admin | Spouse | Back-office, QuickBooks, invoicing |

## What This App Does
Three-tab operations tool replacing paper notebooks, printed binders, and
carbon-copy invoice books. Tabs: Schedule, Route Log, PT Tracker.
Invoicing (Tab 4) is scoped for a future phase -- do not add it yet.

## Device & Connectivity Context
- Used on personal phones and shop desktop.
- Cell coverage is unreliable on routes. App must work fully offline.
- The shop is the guaranteed sync point. Do not assume internet on the road.
- localStorage only. Nothing leaves the browser.

## Brand & Visual Design
- Primary: #0d1e3d (dark navy -- truck cab and body)
- Blue: #1a3f7a (mid navy)
- Bright blue: #1e5fc2 (tank colour)
- Red: #c8102e (script lettering on truck)
- Background: #f2f4f8
- Heading font: Oswald (bold, industrial)
- Body font: Source Sans 3
- Tone: industrial, no-nonsense, field-ready
- Reference app: TerraComm (structure and density), Take Pride (modal/form patterns)

## Tab 1 -- Schedule
Gerry's domain. Incoming call notes and the daily job list.

### Call Notes (quick capture)
Gerry takes calls while driving or at the shop. Entry must be fast -- target
under 30 seconds, usable one-handed.
Fields:
- Customer name (text, required)
- Phone (text, optional)
- Address / location (text, required)
- Municipality (dropdown -- list is configurable, see Business Rules)
- Tank size (dropdown: 500 gal / 750 gal / 1000 gal / 1250 gal / 1500 gal / Unknown)
- Notes (textarea, optional -- access issues, dogs, gate codes, etc.)
- Urgency (dropdown: Routine / Soon / Urgent)
- Date called (auto = today, editable)

### Job Board
Call notes get promoted to scheduled jobs. A job adds:
- Assigned driver (dropdown from driver list)
- Scheduled date
- Status: Unscheduled / Scheduled / Done / Cancelled

Daily view: filter by date, grouped by driver. This is what drivers see in
the morning.

## Tab 2 -- Route Log
Driver-facing. They record what they actually did.

### Job Completion
Drivers see their jobs for the assigned date. For each job they can:
- Mark complete (records timestamp)
- Add a field note (optional)

### Dump Log
Separate from job completion. Drivers log each dump run:
- Which municipal lagoon this load is recorded against (dropdown -- matches
  municipality list, NOT necessarily where they physically dumped)
- Number of tanks in this load (1 / 2 / 3)
- Truck (dropdown from truck list)
- Date/time (auto = now, editable)
- Notes (optional)

CRITICAL: The lagoon recorded is always the service municipality of the
customers in that load, regardless of physical dump location. This is a
billing and compliance record, not a GPS log.

### Dump Summary
Running totals for the day: jobs done, loads dumped, tanks pumped.

## Tab 3 -- PT Tracker
Portable toilet unit management.

### Numbered Units (~20 units)
Each unit is individually tracked:
- Unit number (e.g. PT-01 through PT-20)
- Status: Available / Deployed / Needs Service
- Current customer (text, populated when deployed)
- Deploy date
- Expected return date (optional)
- Tarp number (each unit has a paired numbered winterization tarp)
- Notes (colour, insulation, metal-clad -- physical characteristics are fixed
  per unit, record once and leave)

### Count-Only Units
Additional units tracked by type and count only (no individual numbers):
- Type (dropdown: Standard / Deluxe / Accessible)
- Total owned
- Currently deployed count
- Available = Total minus Deployed (calculated, not entered)

### Deployments
Log a deployment:
- Unit (select from available numbered units OR count-only type)
- Customer name
- Address
- Customer type: Construction / Event / Residential / Municipal / Cash Rental
- Deploy date
- Expected return
- Cash rental flag: if checked, NO invoice is generated. Deployment is
  recorded for unit tracking only.

### Returns
Mark a unit returned -- clears customer, resets status to Available.

## Business Rules
- Municipality list is configurable (up to 10 municipalities). One is flagged
  as dump-fee-exempt. Do not hardcode names -- use a simple editable list.
- Base service rate is a single default. Per-customer exceptions exist but are
  rare. Rate field on jobs is optional and defaults to base rate.
- Distance/inconvenience fees exist but are rare. Add as an optional notes
  field on jobs, not a structured field.
- Cash PT rentals: create a deployment record, do NOT create an invoice entry
  of any kind.
- Trucks hold 2--3 customer tanks per load. A driver may complete 2--3 jobs
  before logging a dump run. This is normal -- do not enforce 1:1 job-to-dump.
- Drivers plan their own routes. No auto-routing, no map integration.

## What This App Does NOT Do (yet)
- Invoicing (Phase 2)
- QuickBooks CSV export (Phase 2)
- Customer history / database (Phase 2)
- Multi-device sync (by design -- offline first)
- Login or authentication
- Auto-routing or mapping
- Push notifications

## Sample Data to Pre-load
See BRIEF.md for full sample data set. If BRIEF.md is not present, ask
before inventing data.

## Open Questions (must be resolved before build)
See BRIEF.md. If BRIEF.md shows no open questions, proceed.

## Lessons
See lessons.md. If lessons.md does not exist yet, create it after the first
build session.

## Agent Sync

- Read `SYNC.md` before starting work.
- Update `SYNC.md` after meaningful changes so Codex and Claude share the current state.
