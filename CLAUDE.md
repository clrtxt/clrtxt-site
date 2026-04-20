# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**clrtxt** is a static marketing website for an AI consulting business targeting small businesses and solo operators. The entire site is a single self-contained file: `index.html`.

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
- **Responsive layout** with a single breakpoint at 640px
- **Inline JavaScript** — a single scroll listener that toggles a `scrolled` class on the nav for a border-fade effect

The only external dependency is the Inter font loaded from Google Fonts.
