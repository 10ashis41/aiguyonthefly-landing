# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static marketing site for "AI Guy on the Fly" — no build step, no framework, no
dependencies. Every page is a single self-contained `.html` file with inline `<style>`
and no external CSS/JS files (aside from a third-party analytics script). There is no
`package.json`, test suite, or linter in this repo.

To preview changes, just open the `.html` file directly in a browser (or serve the
directory with any static file server) — no build/compile step is involved.

## Structure

- `index.html` — hub/landing page listing all tools, links out to each product page below.
- `book.html`, `chat.html`, `invoice.html`, `mail.html`, `sign.html`, `stats.html` —
  one landing page per product/tool, each pitching a single feature (booking, chat inbox,
  invoicing, email, e-signatures, stats/analytics).
- `aiguy_logo.png`, `aiguy_favicon.png` — shared brand assets.

## Architecture notes

- **No shared stylesheet.** Every page repeats the same design system (dark theme,
  `#00d4ff` accent, Inter font, header/hero/CTA/footer layout) via its own `<style>`
  block. When changing shared visual style (colors, spacing, button styles), the change
  must be applied to each `.html` file individually — there is no single source of truth.
- **Consistent page template.** Each product page (`book.html`, `chat.html`, etc.) follows
  the same layout: header with brand name → tag pill → h1 with a highlighted `<span>` →
  subhead → checklist of bullets → CTA button group (`btn-primary` / `btn-secondary`) →
  footer linking back to `index.html`. New product pages should follow this same pattern.
- **CTA buttons are placeholders.** The `Get This Set Up For Me` / `Buy Now` links use
  `href="#"` — they are not wired to a real checkout/booking flow yet.
- **Analytics.** Each page embeds a self-hosted analytics script:
  `https://stats.aiguyonthefly.com/script.js` (Umami-style, via `data-website-id`).
- **Deployment.** The site auto-deploys on push (seen via a VM webhook triggered from
  commits, per git history) — no CI config lives in this repo, so the deploy hook is
  configured externally, not through GitHub Actions.
