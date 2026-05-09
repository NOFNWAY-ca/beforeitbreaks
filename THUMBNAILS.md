# BiB Thumbnail and Preview System

Purpose: control how pages appear when shared.
Applies to: homepage and all KIND demo pages.
Uses: Open Graph + Twitter metadata.
Image standard: `1200x630` PNG.

# Asset Inventory

## Core Identity

- `favicon.svg` — master vector favicon
- `favicon.ico` — browser compatibility
- `favicon-32.png` — standard browser icon
- `apple-touch-icon.png` — mobile/iOS bookmark icon

## Social Preview

- `og-image.png` — homepage preview image (`1200x630`)
- `og-image.svg` — editable master version

## KIND Demo Thumbnails

- `kind-tier-1-thumb.png` — Intake Board preview (`1200x630`)
- `kind-tier-1-thumb.svg` — editable master version
- `kind-tier-1-thumb-v2.png` — current Intake Board preview used by metadata and homepage cards (`1200x630`)
- `kind-tier-1-thumb-v2.svg` — current editable master version
- `kind-tier-1-thumb-v3.png` — current Intake Board preview used by metadata and homepage cards (`1200x630`)
- `kind-tier-1-thumb-v3.svg` — current editable master version
- `kind-tier-2-thumb.png` — Foster Coordination preview (`1200x630`)
- `kind-tier-2-thumb.svg` — editable master version
- `kind-tier-2-thumb-v2.png` — current Foster Coordination preview used by metadata and homepage cards (`1200x630`)
- `kind-tier-2-thumb-v2.svg` — current editable master version
- `kind-tier-2-thumb-v3.png` — current Foster Coordination preview used by metadata and homepage cards (`1200x630`)
- `kind-tier-2-thumb-v3.svg` — current editable master version
- `kind-tier-3-thumb.png` — Medical Tracker preview (`1200x630`)
- `kind-tier-3-thumb.svg` — editable master version
- `kind-tier-3-thumb-v2.png` — current Medical Tracker preview used by metadata and homepage cards (`1200x630`)
- `kind-tier-3-thumb-v2.svg` — current editable master version
- `kind-tier-3-thumb-v3.png` — current Medical Tracker preview used by metadata and homepage cards (`1200x630`)
- `kind-tier-3-thumb-v3.svg` — current editable master version

# Metadata Implementation

Metadata exists in:

- `index.html`
- `kind-tier-1-intake.html`
- `kind-tier-2-foster.html`
- `kind-tier-3-medical.html`

Each page includes:

- favicon links
- canonical URL
- `og:title`
- `og:description`
- `og:image`
- `og:url`
- `twitter:card`
- `twitter:image`

Each page uses a page-specific `og:image`.

# Image Standards

- Social preview images: `1200x630` PNG.
- PNG is preferred over SVG for Open Graph.
- SVG is used internally where appropriate.
- Use absolute URLs for `og:image`.
- Keep text readable at small sizes.

# Adding a New Demo Page

1. Create thumbnail PNG (`1200x630`).
2. Create SVG master version.
3. Add image to repo root.
4. Add Open Graph metadata to page.
5. Set page-specific `og:title`.
6. Set page-specific `og:description`.
7. Set `og:image` to new PNG.
8. Verify canonical URL.
9. Test preview rendering.

# Testing and Validation

Recommended tools:

- https://www.opengraph.xyz/
- https://www.linkedin.com/post-inspector/
- Discord paste test

These tools refresh cached previews.

If previews appear outdated, cache refresh is required.

Validation checklist:

- Confirm image files exist in the repo.
- Confirm deployed images load directly by URL.
- Confirm each page has one `og:image`.
- Confirm each page has one `twitter:image`.
- Confirm titles and descriptions are page-specific.

# Deployment Notes

After deploying:

- Confirm images load directly via URL.
- Confirm metadata is visible in page source.
- Run preview debugger once.
- Verify homepage and all demo pages.

# Common Failure Modes

Missing thumbnail:

- `og:image` path incorrect
- file not deployed
- relative URL used instead of absolute

Wrong preview image:

- cached preview not refreshed
- duplicate `og:image` tags exist

No preview image:

- metadata missing
- unsupported image format

# Future Maintenance Notes

- Maintain consistent naming pattern.
- Do not reuse thumbnails across unrelated demos.
- Keep thumbnail text concise.
- Avoid decorative clutter.
- Maintain `1200x630` ratio.
