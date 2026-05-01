# McMahon Ranch Sync

## Status
Market-ready single-file ranch management MVP with offline support, reporting, inventory, and compliance fields.

## Current Files
- `mcmahon-ranch.html` = current deliverable
- `manifest.json` = PWA manifest for standalone install
- `sw.js` = service worker caching the app shell for offline use

## Recent Changes
- Rebuilt the app around a unified `mr_app_v2` localStorage model with migration from the older multi-key storage.
- Added Dashboard, Operations, Inventory, Health, Equipment, Pastures, and Reports flows.
- Added Manitoba Premises ID, CCIA / RFID fields, withdrawal-day tracking, clearance dates, and dashboard withdrawal warnings.
- Added medication inventory decrement on treatment save, feed and medication stock management, JSON export/import, and High-Viz mode.
- Added annual livestock, CCIA movement, and tax / sales printable reports.
- Added `manifest.json`, `sw.js`, and service worker registration.

## Open Questions
- Service worker support only works from an HTTP or HTTPS origin. If the client normally opens the HTML directly from `file://`, the offline browser cache layer will not register, though the app still works as a local file.
- The reports currently treat births as animals entering the premises and sales / deaths as animals leaving. If purchase intake becomes a real workflow, add a separate intake log.

## Next Recommended Step
- Preview the rebuilt app in a browser and confirm whether the client wants purchases, breeding records, or pasture rotation added as the next MVP step.
