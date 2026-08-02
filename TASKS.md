# TASKS

Backlog for this project's autonomous build rotation visits (see root `CLAUDE.md` → "Autonomous build rotation" for how this file gets used).

## Known Bugs
- App Store link is still the placeholder `https://apps.apple.com/app/chessloops` on both the nav and both CTA buttons in `index.html` (and referenced in `CLAUDE.md` as "update when live"). Needs the real App Store URL/ID from Bradley once the app is live — not something to guess at autonomously.

## Backlog (next up, roughly prioritized)
1. Add an `og:image` meta tag to `index.html` (currently has `og:title`/`og:description`/`og:url` but no image, so link previews on social/iMessage show nothing). Previously logged as blocked on needing a "real" image asset, but that's no longer true — 2026-08-02's favicon fallback (see Log) proved out a real pipeline (claude-in-chrome renders an HTML/SVG page → screenshot → Pillow resize/crop, all in-repo, no external asset needed) that can just as well render a branded 1200x630 OG card using the site's own colors/fonts/knight glyph. Next visit can build directly instead of re-deriving this.

## Icebox / later
- Revisit App Store CTA link once the app has actually shipped

## Log
- 2026-07-25: Reviewed site. Fixed a stale `© 2025` footer on `index.html` (legal pages already said `© 2026`). Added a favicon (brand knight glyph `favicon.svg`) since the site had none across any of the three pages. Commits 03add16, adba6c8.
- 2026-07-30: Known Bugs entry (App Store placeholder link) isn't autonomously actionable per its own note, and Backlog #1 (og:image) needs a real image asset I don't have — did #2 instead (now #1 above), which needed no asset: added a `theme-color` meta tag (`#141816`, matching `--dark`) to all three pages. Commit d7f2aaf.
- 2026-08-02: Known Bugs entry is still not autonomously actionable, and this time actually tested the "needs a real image asset" assumption on the old Backlog #2 (PNG favicon fallback) rather than taking it at face value — turns out I can generate real raster assets: rendered `favicon.svg` via a local HTML wrapper in claude-in-chrome at high res, screenshotted it, and used Pillow to produce a multi-resolution `favicon.ico` (16/24/32/48/64px) and a 180x180 `apple-touch-icon.png`. Linked both as fallbacks alongside the existing SVG icon on all three pages; verified with curl (200s) and an in-browser check (no console errors, layout unaffected). Updated the remaining og:image item's note since the same asset-generation pipeline applies there too — it's no longer actually blocked. Commit f82ec72.
