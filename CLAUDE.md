# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static landing page website for ChessLoops, a mobile chess training app. Hosted on GitHub Pages with custom domain `chessloops.com`. The site serves as a download landing page and hosts legal pages (terms, privacy) that the iOS app links to directly.

## Development

No build step. Static HTML/CSS only — open `index.html` in a browser or run a local server:

```bash
python -m http.server 8765
```

## Architecture

- `index.html` — Landing page with hero, Woodpecker Method explanation, difficulty levels, features, and App Store CTA
- `terms.html` — Terms & Conditions (linked from iOS app)
- `privacy.html` — Privacy Policy (linked from iOS app)
- `styles.css` — Shared stylesheet for all pages
- `CNAME` — GitHub Pages custom domain config (`chessloops.com`)
- `.nojekyll` — Disables Jekyll processing on GitHub Pages
- `MobileAppClaude.md` — Reference CLAUDE.md from the ChessLoops mobile app repo (not part of the website)

## Key Details

- App Store link (live as of 2026-08-11): `https://apps.apple.com/us/app/chessloops/id6758915748` — appears in `index.html`'s nav, hero badge, hero CTA button, and bottom CTA section. This has broken once already (the original placeholder silently went dead) — verify it still resolves to the correct app before relying on it, see `TASKS.md`'s standing per-visit check
- Contact email in legal pages: `support@chessloops.com`
- CSS uses Google Fonts: Playfair Display (display) + DM Sans (body)
- Scroll-reveal animations via IntersectionObserver in inline script on `index.html`
- Legal pages (`terms.html`, `privacy.html`) share the same nav/footer/styles pattern — keep them consistent when editing
- The iOS app deep-links directly to `https://chessloops.com/terms.html` and `https://chessloops.com/privacy.html`
