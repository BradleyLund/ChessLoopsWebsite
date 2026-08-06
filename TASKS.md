# TASKS

Backlog for this project's autonomous build rotation visits (see root `CLAUDE.md` → "Autonomous build rotation" for how this file gets used).

## Known Bugs
- App Store link is still the placeholder `https://apps.apple.com/app/chessloops` on both the nav and both CTA buttons in `index.html` (and referenced in `CLAUDE.md` as "update when live"). Needs the real App Store URL/ID from Bradley once the app is live — not something to guess at autonomously.

## Backlog (next up, roughly prioritized)
_(empty — the only open item is the Known Bugs entry above, which isn't autonomously actionable. Next visit: do a fresh review pass rather than assume there's nothing left to find.)_

## Icebox / later
- Revisit App Store CTA link once the app has actually shipped

## Log
- 2026-07-25: Reviewed site. Fixed a stale `© 2025` footer on `index.html` (legal pages already said `© 2026`). Added a favicon (brand knight glyph `favicon.svg`) since the site had none across any of the three pages. Commits 03add16, adba6c8.
- 2026-07-30: Known Bugs entry (App Store placeholder link) isn't autonomously actionable per its own note, and Backlog #1 (og:image) needs a real image asset I don't have — did #2 instead (now #1 above), which needed no asset: added a `theme-color` meta tag (`#141816`, matching `--dark`) to all three pages. Commit d7f2aaf.
- 2026-08-02: Known Bugs entry is still not autonomously actionable, and this time actually tested the "needs a real image asset" assumption on the old Backlog #2 (PNG favicon fallback) rather than taking it at face value — turns out I can generate real raster assets: rendered `favicon.svg` via a local HTML wrapper in claude-in-chrome at high res, screenshotted it, and used Pillow to produce a multi-resolution `favicon.ico` (16/24/32/48/64px) and a 180x180 `apple-touch-icon.png`. Linked both as fallbacks alongside the existing SVG icon on all three pages; verified with curl (200s) and an in-browser check (no console errors, layout unaffected). Updated the remaining og:image item's note since the same asset-generation pipeline applies there too — it's no longer actually blocked. Commit f82ec72.
- 2026-08-06: Implemented Backlog #1 (og:image), using the same render → screenshot → Pillow pipeline proved out 2026-08-02. Built a 1200x630 branded card (Playfair Display wordmark, DM Sans tagline, the favicon's gold knight glyph, plus a large translucent knight-head watermark that emerged from rendering the U+265E codepoint at 560px — neither Playfair Display nor Georgia actually define that glyph, so the browser falls back to a system symbol font that draws a detailed knight head) in a throwaway `og-image-render.html`, queried the live page's exact `getBoundingClientRect()`/`devicePixelRatio` to crop precisely rather than guessing offsets from the screenshot, and deleted the render-source file afterward (matches the 2026-08-02 favicon commit's own precedent of committing only the final asset). Added `og:image`/`og:image:width`/`og:image:height`/`og:image:alt` plus a `twitter:card` set to `index.html` only — `terms.html`/`privacy.html` never had `og:` tags either, and aren't share-worthy pages. Verified with curl (200 on both `index.html` and the new `og-image.png`), an in-browser console check (no errors), and a screenshot confirming the rest of the page is unaffected. Commit d3ebbed.
