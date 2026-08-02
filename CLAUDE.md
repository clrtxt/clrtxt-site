# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**clrtxt** is a single-page contact landing site for Thomas Alley at `clrtxt.com`. It is one screen: wordmark, name, email. The page is a single self-contained file, `index.html`, alongside two static assets (`favicon.svg`, `og.png`).

## Development

No build step required. To preview locally, open `index.html` directly in a browser or serve it with any static file server:

```bash
npx serve .
# or
python -m http.server 8000
```

To deploy: edit `index.html`, commit, and push to `master`. GitHub Pages redeploys automatically within ~1 minute. See `DEPLOY.md` for full setup instructions.

## Architecture

Everything lives in `index.html`:
- **Embedded CSS** with CSS custom properties for the design system (orange `#C4622D` brand color, Inter font via Google Fonts)
- **Full-height flex layout** — `body` is a flex column at `100dvh`, the hero flexes to fill, and the footer is pinned to the bottom
- **Responsive layout** with a single breakpoint at 640px
- **No JavaScript.** The page does not scroll; keep it that way unless content is added.

The only external dependency is the Inter font loaded from Google Fonts (weights 300/400/500/800 — the ones actually used).

`og.png` is generated from an SVG source; if the wordmark or email changes, regenerate it (1200×630) so unfurls stay accurate.
