# Project Brief — Septic Dispatch
**Date:** 2026-04-03
**Directory:** `septic-dispatch/`
**Status:** Demo Reference

---

## 1. Client & Context
**Business name:** Septic Dispatch
**Location:** Generic Manitoba service-area demo
**Phone:** Not applicable
**What they do:** Seasonal septic tank pumping and portable toilet rentals. Commercial, residential, and event/construction clients across several Manitoba municipalities.

**Who uses the app:**
| Role | How They Use It |
|---|---|
| Owner | Takes booking calls, schedules all jobs, manages settings, prints daily lists |
| Tank Driver A | Picks up printed job list at shop each morning |
| Tank Driver B | Picks up printed job list at shop each morning |
| PT Driver | Picks up printed job list, logs PT deployments and pickups |
| Floating Driver | Picks up printed job list, logs PT deployments and weekend cash rentals |
| Office/Admin | Views schedule, oversees PT inventory |

**Device context:** Shop desktop is the primary device. Drivers interact with the app at the shop only — morning pickup and end-of-day dropoff. App must work offline. No field sync required.

**Current paper workflow being replaced:**
- Incoming calls recorded in a notebook
- Daily job lists handwritten or printed per driver
- PT inventory tracked informally

**Paper workflows NOT being replaced in this build:**
- Carbon-copy invoice books filled at each job
- Dump logs kept in the truck (monthly paper log, filled during each dump run)
- Payment collection and cash handling at end of day

---

## 2. App Purpose
A two-tab operations tool that digitizes the front half of the daily workflow — capturing incoming calls cleanly, building and printing the daily job list for each driver, and tracking the portable toilet fleet. It does not touch invoicing, dump logging, or payment collection. Those paper workflows are working and are scoped for later phases.

This brief remains useful as a planning reference even though the original prospective client did not proceed.

---

## 3. Tabs / Sections

### Tab 1 — Schedule

**Who uses it:** Owner primarily. All roles can view.

**Purpose:** Capture incoming calls as notes, promote them to scheduled jobs, and produce a clean printed job list for each driver each morning.

**Section A — Call Notes (quick capture)**
Fast entry is the priority. The owner takes calls while driving or at the shop. Entry should be possible in under 30 seconds.

Fields:
| Field | Type | Required | Notes |
|---|---|---|---|
| Customer name | Text | Yes | |
| Phone | Text | No | |
| Address / location | Text | Yes | |
| Municipality | Dropdown | Yes | From settings list |
| Tank size | Dropdown | No | 500 / 750 / 1000 / 1250 / 1500 gal / Unknown |
| Notes | Textarea | No | Access issues, dogs, gate codes, etc. |
| Urgency | Dropdown | Yes | Routine / Soon / Urgent |
| Date called | Date | Yes | Defaults to today |

Interactions: Add new call note (large, prominent button — most common action). Edit. Delete. Promote to scheduled job.

**Voice capture — microphone button on the call note form:**
The owner is often on the phone while entering notes. A microphone button inside the new call note form allows them to dictate while the customer is still talking.

How it works:
- Mic button appears at the top of the new call note form, clearly visible
- Tapping it starts the Web Speech API in continuous listening mode
- Everything spoken transcribes in real time into a staging text area labelled "Voice transcript" — raw, unedited
- Below the transcript, a "Fill fields from transcript" button lets the owner review and confirm before anything is committed to the form fields
- Transcript text can also be edited manually before confirming
- After confirming, the owner still reviews and adjusts individual fields normally — voice is a capture aid, not an auto-submit
- A clear "Stop" button ends recording; mic button returns to idle state

Implementation rules:
- Use the browser's built-in Web Speech API (window.SpeechRecognition or window.webkitSpeechRecognition). No external service, no API key.
- Check for API availability on load. If not available, hide the mic button entirely — do not show an error, do not break the form.
- Chrome requires internet for speech recognition (sends to Google). Safari processes on-device and works offline. Do not try to work around this — just let it behave as the browser allows.
- The form must be fully usable without voice at all times. Voice is an enhancement, not a dependency.
- Mic button visual states: idle (grey), listening (red, pulsing), processing (spinner). Make it obvious when the mic is hot.

Unscheduled call notes should be visually distinct and easy to find — they represent work that hasn't been assigned yet.

**Section B — Job Board**
Promoting a call note to a job adds:
| Field | Type | Required | Notes |
|---|---|---|---|
| Assigned driver | Dropdown | Yes | From settings driver list |
| Scheduled date | Date | Yes | |
| Rate | Currency | No | Defaults to base rate from settings — unobtrusive |
| Status | Dropdown | Yes | Unscheduled / Scheduled / Done / Cancelled |

Interactions:
- Filter by date (default = today)
- Filter by driver
- Mark done
- Edit
- Cancel
- Print day's job list

**Print view — this is important:**
When the owner clicks Print for a given date, the app produces a clean, printer-friendly layout showing each driver's jobs for that day on a single page. Each driver's section is clearly separated. Fields shown: customer name, address, municipality, tank size, notes. Rate is not shown on the printed list. This is what drivers take with them — it must be genuinely readable, not an afterthought.

Business rules:
- A call note exists independently until explicitly promoted to a job. Do not auto-promote.
- Rate field defaults silently. Show it only when editing a job, never in the daily list or print view.
- Distance and inconvenience fees are rare and unstructured — handle via Notes field only. No separate fee fields.

---

### Tab 2 — PT Tracker

**Who uses it:** PT driver, floating driver, owner.

**Purpose:** Track the portable toilet fleet. 150+ units total. The vast majority are tracked by type and count only. A small subset have user-defined individual identifiers and are tracked unit-by-unit.

**Section A — Fleet Overview**
Stat cards at top: Total units, Currently deployed, Available, Needs service. Calculated from live data.

**Section B — Type Inventory**
Each toilet type is a row. Types are configurable in Settings.

| Column | Notes |
|---|---|
| Type name | e.g. Standard, Deluxe, Accessible, Heated |
| Total owned | Editable directly in this view |
| Deployed | Calculated from active deployments of this type |
| Available | Total minus Deployed (calculated, not entered) |
| Needs service | Manual count, editable directly in this view |

**Section C — Individual Units**
Small subset of units with their own identifiers. Identifier format is user-defined — no enforced format or prefix.

Fields per unit:
| Field | Type | Notes |
|---|---|---|
| Unit ID | Text | User-defined — e.g. "A7", "Blue-01", "Heritage-3" |
| Type | Dropdown | From type list in Settings |
| Physical notes | Text | Colour, insulation, metal-clad — set once, rarely changed |
| Tarp ID | Text | Paired winterization tarp identifier |
| Status | Dropdown | Available / Deployed / Needs Service |
| Current customer | Text | Populated on deployment, cleared on return |
| Deploy date | Date | Populated on deployment |
| Expected return | Date | Optional |

**Section D — Log a Deployment**
Applies to both individual units and count-based types.

| Field | Type | Required | Notes |
|---|---|---|---|
| Unit | Select | Yes | Choose individual unit ID, or choose type + quantity for count-based |
| Customer name | Text | Yes | |
| Address | Text | Yes | |
| Customer type | Dropdown | Yes | Construction / Event / Residential / Municipal / Cash Rental |
| Deploy date | Date | Yes | Defaults to today |
| Expected return | Date | No | |
| Notes | Text | No | |

CRITICAL: If Customer Type = Cash Rental, the cash rental flag is set automatically. No dollar amounts are stored or displayed. No invoice record of any kind is created or implied. The deployment record exists for unit tracking only.

**Section E — Log a Return**
Mark a unit or count-based deployment as returned. Clears customer info, resets status to Available, records return date and timestamp.

Active deployments should be visible as a list — customer name, unit(s), deploy date, expected return, overdue flag if past expected return date.

---

## 4. Business Rules & Edge Cases

**Municipality dropdown:**
Used on jobs for service area record-keeping only. Dump routing is handled on paper and is out of scope for this build.

Municipalities:
- Ste. Anne
- La Broquerie
- R.M. of Hanover
- City of Steinbach

**Dump fee exemption flag:**
One municipality can be flagged as dump-fee-exempt in Settings. Admin-controlled, not hardcoded. Informational only in this build — no calculation depends on it.

**Rates:**
- Base service rate: $125 (default, editable in Settings)
- Dump fee: $15 per load (default, editable in Settings)
- Per-job rate override is available but unobtrusive — only visible when editing a job
- No tax calculation in this build

**Cash rentals:**
Deployment record is created for unit tracking. No invoice. No dollar amount. Customer type "Cash Rental" automatically sets the flag — no separate checkbox needed.

**PT type inventory:**
Total owned is entered manually and edited directly in the type inventory table. Deployed count is always calculated from active deployment records — never manually entered. Available = Total minus Deployed minus Needs Service.

**Settings — everything configurable:**
The following must be editable by the owner in a Settings panel. Settings access should be unobtrusive — a small gear icon in the header, not in the main nav.
- Municipality list (name, dump-fee-exempt flag)
- Driver list (name)
- Truck list (name/number) — reference only, trucks not tracked in this build
- PT type list (name)
- Base service rate
- Dump fee per load

---

## 5. What This App Does NOT Do
- Route logging or dump run tracking (paper system in truck, Phase 2)
- Voice-to-field auto-parsing (transcript is manual review only — do not attempt to parse names, addresses, or tank sizes from speech automatically)
- Invoicing of any kind (carbon-copy books, Phase 3)
- QuickBooks or CSV export (Phase 3)
- Customer history or database (future phase)
- Multi-device sync
- Login or authentication
- Auto-routing or map integration
- Push notifications or reminders
- Tax calculation
- Payment processing
- Any dollar amounts on cash rental records

---

## 6. Visual Design
**Primary (navy):** #0d1e3d
**Blue:** #1a3f7a
**Bright blue:** #1e5fc2
**Red (accent):** #c8102e
**Background:** #f2f4f8
**Border:** #cdd4e0
**Muted text:** #5a6b80
**Success:** #1a6634
**Warning:** #b35c00

**Heading font:** Oswald — bold, condensed, industrial. Matches the truck lettering aesthetic.
**Body font:** Source Sans 3 — clean and readable at small sizes.

**Tone:** Industrial, no-nonsense, field-ready. Dense but not cluttered. High contrast. Built for a shop desktop and occasional phone use at the counter.

**Wordmark:** "RENE'S" in Oswald bold, "SEPTIC SERVICES" smaller below it. Navy header background. Red bottom border on header. Gear icon (⚙) far right of header for Settings access.

**Reference apps:** TerraComm for header/nav structure and density. Take Pride for modal and form patterns.

**Print view:** Clean, black and white, no background colours. Company name and date at top. Each driver's jobs in a clearly separated block. Large enough type to read in a truck cab.

---

## 7. Sample Data

**Settings — pre-loaded defaults:**
- Municipalities: Ste. Anne, La Broquerie, R.M. of Hanover, City of Steinbach
- Drivers: Driver A, Driver B, Driver C (PT), Driver D (Floating)
- PT Types: Standard, Deluxe, Accessible, Heated
- Base rate: $125 | Dump fee: $15

**Call Notes (unscheduled):**
- Bergmann / 204-555-0181 / 247 Clearwater Dr, Steinbach / City of Steinbach / 1000 gal / "Dog in yard, use side gate" / Routine
- Fehr / 204-555-0234 / Rural Rte 4, La Broquerie / La Broquerie / 750 gal / (no notes) / Soon
- Unknown / 204-555-0099 / 89 Oak Ave, Ste. Anne / Ste. Anne / Unknown / "Backing up, needs ASAP" / Urgent

**Scheduled Jobs (today):**
- Peters / Blumenort Rd, Blumenort area / R.M. of Hanover / 1500 gal / Driver A / Scheduled
- Reimer / 14 Maple Cres, Mitchell area / R.M. of Hanover / 1000 gal / Driver A / Scheduled
- Klassen / Hwy 52, Kleefeld area / R.M. of Hanover / 750 gal / Driver B / Scheduled
- Neufeld / Rural Rte 12, Ste. Anne / Ste. Anne / 1000 gal / Driver B / Done
- Penner Construction / Industrial Dr, Steinbach / City of Steinbach / PT service call / Driver C / Scheduled

**PT Type Inventory:**
- Standard: 80 owned, 2 needs service
- Deluxe: 40 owned, 0 needs service
- Accessible: 20 owned, 1 needs service
- Heated: 15 owned, 0 needs service

**Individual Units:**
- "A1" / Deluxe / "Blue, insulated, metal-clad" / Tarp "T-A1" / Deployed / Penner Construction, Industrial Dr / today minus 14 days
- "A2" / Deluxe / "Blue, insulated, metal-clad" / Tarp "T-A2" / Available
- "H1" / Heated / "White, heated unit" / Tarp "T-H1" / Deployed / Kleefeld Winter Event / today minus 21 days / return expected today
- "H2" / Heated / "White, heated unit" / Tarp "T-H2" / Needs Service / "Heater element issue"

**Active Deployments (count-based):**
- 8x Standard / Penner Construction / Industrial Dr, Steinbach / Construction / today minus 21 days
- 4x Deluxe / Reimer Wedding / 45 Garden Rd, Ste. Anne / Event / yesterday / returns tomorrow
- 3x Accessible / City of Steinbach Park Program / Municipal / today minus 30 days / no end date
- 2x Standard / Friesen / Cash Rental / today / returns tomorrow

---

## 8. Open Questions
None. Ready for build.
