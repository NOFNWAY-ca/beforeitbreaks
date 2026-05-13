# Before it Breaks Sync

## Status
Active marketing/demo site with multiple standalone demos.

## Current Structure
- `index.html` = portfolio/landing page
- `dispatch.html` = septic operations demo
- `law-demo.html` = legal workflow demo
- `caylie-*.html` = planner variants

## Recent Changes
- Added `SAR-Demo/index.html`, a direct-link landing page for the three KIND rescue demos at `/SAR-Demo`, with noindex protection and links to all tiers.
- Added `SAR-Demo.html` as a bare-path fallback that redirects `/SAR-Demo` to `/SAR-Demo/` for GitHub Pages.
- Renamed the PetSet demo family to `KIND`, short for Key Intake and Data, including demo filenames, landing-page references, localStorage keys, export filenames, and visible product copy.
- Pulled the KIND demo family off the public landing page and added `noindex, nofollow` meta tags so the files can stay reachable by direct URL without being visibly promoted.
- Moved the client prep organizer out of the site and into a visible home-directory folder for local use.
- Standardized the septic demo wording to `Septic Dispatch`.
- Added missing project docs and sync workflow.
- Added `kind-tier-1-intake.html`, a standalone KIND Tier 1 rescue intake board with localStorage persistence, live summary counts, filters, sortable table columns, and add/edit modal workflow.
- Extended `kind-tier-1-intake.html` with data safety and rescue workflow features including delete confirmation, JSON export/import, persistent filters, save feedback, safer dialog handling, and status-driven rescue workflow updates.
- Added `kind-tier-2-foster.html`, a standalone KIND foster coordination board based on the intake demo, with persisted foster records, capacity-aware assignments, shared import/export, photo support, printing, and status history retained.
- Added `kind-tier-3-medical.html`, a standalone KIND medical tracking board based on the intake demo, with per-animal medical records, timeline display inside the animal modal, printable medical summaries, photo support, and persisted status history.
- Added tier branding across the KIND demos with per-tier product names, fixed `TIER` badges, and locked Tier 3 upgrade placeholders on the Tier 1 and Tier 2 pages.
- Expanded `kind-tier-2-foster.html` with a Tier 2 foster capacity dashboard that surfaces total capacity, available spots, assigned load, full homes, and per-foster occupancy pills.
- Expanded `kind-tier-3-medical.html` with a Tier 3 medical alerts panel, keyword-driven alert scanning, a global upcoming-care feed, and a `Print All` medical intelligence view.
- Refined `kind-tier-3-medical.html` into a more clinical Tier 3 presentation with stronger alert emphasis, urgency pills, and a vertical medical timeline that distinguishes due items from completed care.
- Refined `kind-tier-1-intake.html` into the industrial Tier 1 baseline with flatter registry-style UI, sharper controls, monospaced data treatment, and a stable core-tool header.
- Refined `kind-tier-2-foster.html` so it inherits the Tier 1 product baseline while adding foster coordination as a softer dashboard layer with clearer capacity metrics and shared data styling.
- Continued the tier realignment by making `kind-tier-3-medical.html` truly cumulative: it now retains Tier 2 foster coordination inside Tier 3 with a dedicated Foster Overview, foster table and modal, shared import/export of foster data, and assignment-capacity warnings that still sit underneath the medical intelligence layer.
- Finished the cross-tier consistency pass so the ladder reads clearly: Tier 1 now carries an explicit intake kicker and locked medical placeholder, Tier 2 carries the same locked medical placeholder while keeping foster coordination as the added layer, and Tier 3 remains the full intake + foster + medical product.
- Updated `index.html` so the landing page now explains the KIND ladder directly with a dedicated featured section linking Tier 1 intake, Tier 2 foster coordination, and Tier 3 medical intelligence as one cumulative product family.

## Recent Changes (continued)
- Updated `Client Prep Desk/client-prep.html` to match actual public pricing: Price Helper scale tiers changed to Simple ($500) / Standard ($1,200) / Complex ($2,500); messiness and data risk modifiers reduced proportionally; scale select in editor renamed to Simple/Standard/Complex with dollar amounts; blank client defaults updated (priceLow $500, priceHigh $1,200, scale "standard"). Clears stale localStorage to take effect.

## Open Questions
- Whether the Caylie variants should stay as separate demos or be consolidated.

## Recent Changes (continued)
- Built `festival-command.html` — a full single-file event organizer demo for festival/fair/event organizer clients. Fictional event: Harvest & Holler, Millwood MB, Aug 9–10 2025. Five modules: Schedule (visual time grid), Vendors (with live budget sync), Volunteers, Budget (two-column with auto vendor fees line and net surplus/deficit), Incidents/Lost & Found. Dark/light mode, localStorage persistence, seed data, settings panel with export and reset, print views for schedule and volunteer roster. Confirm2 styled dialog throughout (no window.confirm).

- Completed full hardening pass on `festival-command.html`: incidents search input wired, boot-time version migration guard, stale-data toast (5-min threshold), cross-tab storage listener, and FileReader-based JSON import handler on the settings panel.
- Fixed iOS/Safari boot and layout risks in `festival-command.html`: storage access now falls back to in-memory data if localStorage is blocked, newer syntax hazards were removed, the app height is synced to the mobile viewport, and the top navigation scrolls horizontally on narrow screens.
- Follow-up iPhone fix for `festival-command.html`: added small Safari polyfills for missing DOM/string/array helpers and delayed full app boot until after `DOMContentLoaded`; verified click handlers by driving Chrome DevTools against Vendors/Add Vendor/Settings.
- Local-only bug pass on `festival-command.html`: fixed fallback storage precedence when browser writes fail, switched festival/date defaults to local date/time instead of UTC, removed stale-save residue on reset, and escaped user/imported data in rendered dashboard, schedule, vendors, volunteers, budget, and incident views. Verified with syntax check, headless render, click-handler check, blocked-storage check, and injected HTML/script display check.
- Added an ES5-only top-control shim to `festival-command.html` so iPhone taps on theme, settings, and nav tabs are handled through both `touchend` and `click` without relying on the larger app script's direct click bindings. Verified touch-dispatched theme/settings/vendors actions through Chrome DevTools.
- Added `festival-command-v2.html` as a versioned copy for WhatsApp/iPhone sharing so recipients get a fresh filename instead of a cached/stale `festival-command.html` attachment.
- Synced `festival-command-v4.html` with the latest iPhone hardening and added `festival-command-v5.html` as the fresh WhatsApp/iPhone sendable file. Current version has anchor-based nav, the ES5 touch shim, delayed `.js` activation, storage fallback, escaped rendered data, and static fallback content in every main module so the page is not an empty shell if the app script is blocked.
- Added `festival-command-v6.html` after an additional browser-failure pass. Settings now has a CSS/hash fallback when app JavaScript is blocked, app-only settings actions stay hidden until boot completes, the theme button only appears after the lightweight touch shim runs, and storage fallback precedence now allows real localStorage updates unless a write actually fails. Verified v6 with syntax checks, headless render, touch controls, click controls, blocked storage, and injected HTML/script safety.

- Added the Before it Breaks thumbnail and preview identity system: favicon SVG/ICO/PNG assets, apple touch icon, 1200x630 PNG/SVG Open Graph images, and dedicated KIND tier preview images.
- Wired page-specific favicon, canonical, Open Graph, and Twitter/X metadata into `index.html` and the three KIND demo pages.
- Added a quiet KIND demo ladder section back to `index.html` with thumbnail cards for intake, foster coordination, and medical tracking.
- Reworked the KIND tier thumbnails so they resemble the actual demo interfaces instead of generic dark preview cards, regenerated the 1200x630 PNGs, and pointed the landing-page KIND cards at the PNG assets.
- Added `kind-tier-*-thumb-v2` assets and switched homepage cards plus KIND Open Graph/Twitter metadata to those versioned filenames to bypass stale CDN caches on the original thumbnail URLs.
- Added `kind-tier-*-thumb-v3` assets after early verification cached 404s for the v2 paths before GitHub Pages finished publishing them, then switched homepage cards and metadata to v3.
- Added `THUMBNAILS.md` documenting the asset roles, preview sizes, metadata locations, absolute social image URLs, and preview testing steps.
- Added `DEPLOY.md` as the operational deployment reference for `sync.sh`, pre-sync checks, post-sync verification, and preview debugger use.

## Recent Changes (continued)
- Registration identity cleanup completed (2026-05-07): business name standardized to "Before it Breaks" (lowercase 'i') across all HTML files, doc headings, and metadata. Credibility line added to footer of `index.html`. Invoice template added at `docs/invoice-template.md`. No layout changes made.
- 2026-05-12: Business registration PDFs are kept local and private. Added `*.pdf` to `.gitignore` so sync/deploy does not publish registration paperwork by accident.

## Recent Changes (continued)
- Fixed `caylie_V2.html` (renamed to `caylie_V4.html`) which was a non-functional hollow interface on iPhone. Root causes: (1) `color-mix()` CSS function not supported on iOS < 16.2 — replaced all instances with pre-computed rgba/hex variables defined per theme; (2) Google Fonts `<link rel="stylesheet">` in `<head>` was blocking script execution in WebKit/Safari — removed from head entirely and moved to a dynamically-injected `<link>` at the top of the `<script>` block so nothing can block JS; (3) `window.scrollTo(0,0)` on tab switch was scrolling back to the persistent dashboard, making it look like tabs did nothing — now scrolls to the section element instead. Also added `-webkit-backdrop-filter`, replaced `inset:0` with explicit TRBL on modals, and removed optional chaining `?.` for broader iOS compat.
- Fixed `caylie_V5.html` iPhone blank-content/control failure. Removed Safari parse blockers from the main script (`??`, object spread, optional catch binding, argument spread), added small DOM/array polyfills, guarded boot with a fallback render, moved final mobile overrides after desktop component CSS so the iPhone layout wins, and added real static dashboard/jobs/contact/med/wellbeing fallback markup directly in the HTML so the page is not hollow even if Safari blocks the app script. Added a separate ES5-only control script before the main app script so tabs, settings, and the floating add button still work if the larger app script does not parse on iPhone. Copied the fixed file forward to `caylie_V7.html` as the current fresh iPhone-sendable filename to avoid stale attachment/cache behavior. Verified with script parse check, Chrome DevTools iPhone emulation, and a deliberate broken-main-script test: 390px viewport, 390px document scroll width, dashboard/jobs render, Contacts tab activates, and the floating add button opens the contact modal.
- Follow-up `caylie_V7.html` iPhone control fix after buttons still did not tap on device: converted sidebar tabs, bottom tabs, settings, and floating add from `<button onclick>` controls to real anchors with `href` targets and `data-*` attributes, then changed the early compatibility shim to Festival Command style document-level `click`/`touchend` delegation. Added CSS `:target` fallbacks for sections and modals so anchors still do useful work if JavaScript is blocked. Verified normal main-script mode, deliberately broken-main-script mode, and direct `touchend` dispatched on the nav SVG/icon target.
- Created `caylie_V8.html` after hardening the V7 control model further. The early shim now uses private tab/modal functions instead of calling globals that the full app later overwrites, then conditionally hands off to the full renderer only when available. Static modal controls and app-rendered add controls were converted to anchors with `data-action`, and modal cancel controls use `data-modal-close`. Verified V8 script parsing, normal iPhone emulation, direct `touchend` on icon targets, and broken-main-script fallback.
- Added `noindex, nofollow` metadata to `caylie_V8.html` so it can be shared by direct hidden URL without being promoted to search engines.
- Refined `index.html` commercial positioning without redesigning the site: added concrete hero service language, moved the "Big companies have teams. You have me." pitch directly under the hero, added a small "Who this is for" block, foregrounded Septic Dispatch as the first proof example, kept the KIND ladder before NOFNWAY, reframed NOFNWAY as public proof-of-capability, surfaced the ownership/longevity line, adjusted How It Works Step 1 and process summary, softened contact expectations, and renamed the FAQ heading.

## Open Questions
- Whether the Caylie variants should stay as separate demos or be consolidated.
- Caylie hasn't confirmed V4 works on her iPhone yet — the fix is sound but unconfirmed. Key question is how she's transferring the file (AirDrop, email, iCloud) since re-opening an old attachment would show the old broken version.

## Next Recommended Step
- Confirm caylie_V4.html works on Caylie's iPhone with the fresh file.
- Test `festival-command.html` in browser (open, reset to seed, export, re-import, check incidents search and cross-tab toast).
- Add `festival-command.html` to the landing page (`index.html`) as a featured demo once tested.
- Add short notes to `README.md` describing each demo page so the directory is self-explanatory at a glance.
