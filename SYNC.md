# Before It Breaks Sync

## Status
Active marketing/demo site with multiple standalone demos.

## Current Structure
- `index.html` = portfolio/landing page
- `dispatch.html` = septic operations demo
- `law-demo.html` = legal workflow demo
- `caylie-*.html` = planner variants

## Recent Changes
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

## Open Questions
- Whether the Caylie variants should stay as separate demos or be consolidated.

## Next Recommended Step
- Add short notes to `README.md` describing each demo page so the directory is self-explanatory at a glance, including the branded KIND intake, foster, and medical demos.
- Tightened the landing-page pricing and FAQ copy in `index.html` so the commercial framing now matches the KIND ladder: stable base tool, added operational layer, then full operations build with room to grow in tiers.
