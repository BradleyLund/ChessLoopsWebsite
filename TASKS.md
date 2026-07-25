# TASKS

Backlog for this project's autonomous build rotation visits (see root `CLAUDE.md` → "Autonomous build rotation" for how this file gets used).

## Known Bugs
- App Store link is still the placeholder `https://apps.apple.com/app/chessloops` on both the nav and both CTA buttons in `index.html` (and referenced in `CLAUDE.md` as "update when live"). Needs the real App Store URL/ID from Bradley once the app is live — not something to guess at autonomously.

## Backlog (next up, roughly prioritized)
1. Add an `og:image` meta tag to `index.html` (currently has `og:title`/`og:description`/`og:url` but no image, so link previews on social/iMessage show nothing). Needs a real screenshot or brand graphic exported as an asset first.
2. Add a `theme-color` meta tag (`#141816`, matching `--dark`) to all three pages for a consistent mobile browser chrome color.
3. Consider a lightweight PNG fallback favicon (`favicon.ico` / apple-touch-icon) alongside the new SVG one, for browsers/contexts that don't support SVG favicons.

## Icebox / later
- Revisit App Store CTA link once the app has actually shipped

## Log
- 2026-07-25: Reviewed site. Fixed a stale `© 2025` footer on `index.html` (legal pages already said `© 2026`). Added a favicon (brand knight glyph `favicon.svg`) since the site had none across any of the three pages. Commits 03add16, adba6c8.
