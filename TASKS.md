# TASKS

Backlog for this project's autonomous build rotation visits (see root `CLAUDE.md` → "Autonomous build rotation" for how this file gets used).

## Known Bugs
- App Store link is still the placeholder `https://apps.apple.com/app/chessloops` on both the nav and both CTA buttons in `index.html` (and referenced in `CLAUDE.md` as "update when live"). Needs the real App Store URL/ID from Bradley once the app is live — not something to guess at autonomously.

## Backlog (next up, roughly prioritized)
1. Add an `og:image` meta tag to `index.html` (currently has `og:title`/`og:description`/`og:url` but no image, so link previews on social/iMessage show nothing). Needs a real screenshot or brand graphic exported as an asset first — social scrapers generally need a raster PNG/JPG, not SVG, so this isn't a quick text-only fix like the others here.
2. Consider a lightweight PNG fallback favicon (`favicon.ico` / apple-touch-icon) alongside the existing SVG one, for browsers/contexts that don't support SVG favicons. Same asset-generation blocker as #1.

## Icebox / later
- Revisit App Store CTA link once the app has actually shipped

## Log
- 2026-07-25: Reviewed site. Fixed a stale `© 2025` footer on `index.html` (legal pages already said `© 2026`). Added a favicon (brand knight glyph `favicon.svg`) since the site had none across any of the three pages. Commits 03add16, adba6c8.
- 2026-07-30: Known Bugs entry (App Store placeholder link) isn't autonomously actionable per its own note, and Backlog #1 (og:image) needs a real image asset I don't have — did #2 instead (now #1 above), which needed no asset: added a `theme-color` meta tag (`#141816`, matching `--dark`) to all three pages. Commit d7f2aaf.
