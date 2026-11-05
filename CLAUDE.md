# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A one-page static landing site for Quest Board (the app lives in a separate repo, `guildquests/quest-board`). Hosted on GitHub Pages at https://guildquests.github.io. No JavaScript, no framework, no tests, no linter.

## Commands

Node 22.

```
npm ci          # install
npm run build   # build public/style.css (minified)
npm run dev     # rebuild public/style.css on change
```

To preview, open `public/index.html` in a browser after a build. There is no dev server.

## How it fits together

- `public/` is the whole site and is deployed as-is. `public/index.html` is the only page.
- `src/input.css` is the only CSS source. Tailwind v4 (CSS-first config, no `tailwind.config.js`) compiles it to `public/style.css`, which is git-ignored and built in CI.
- `@import "tailwindcss" source(none)` plus `@source "../public/index.html"` means Tailwind scans only `index.html` for class names. If you add another HTML file, add a matching `@source` line or its classes will not be generated.
- Design tokens live in the `@theme` block in `src/input.css` (colors such as `bg`, `panel`, `line`, `primary`, `accent`, `easy`/`medium`/`hard`; fonts `font-brand`, `font-title`, `font-sans`). Use these utilities (`bg-panel`, `text-muted-text`, `font-brand`) rather than raw Tailwind palette colors. The site is dark-only.
- Fonts are self-hosted in `public/fonts/`. `@font-face` URLs are relative to the output file `public/style.css`, not to `src/`.
- Animations use `motion-safe:` variants so they respect reduced-motion settings. Keep that pattern.
- Deploy: every push to `main` runs `.github/workflows/landing.yml` (npm ci, build, upload `public/`, deploy to Pages). Pushing to `main` publishes the site.

## Content rules

- Pre-launch: links to the `quest-board` GitHub repo and "open source" wording were removed on purpose (commit `381591e`). Do not add them back until told the app repo is public. The self-host section is a short Docker summary for the same reason.
- The "Try the demo" buttons point to `https://quest.hiyan.cloud`.
- Media and fonts keep their own licenses; record any new third-party asset in `CREDITS.md`. The intro video's music file must not be added to the repo (Pixabay license), and the video was made with Remotion, which the page does not depend on.
- Images are `.webp` with explicit `width`/`height` and descriptive `alt` text; below-the-fold images use `loading="lazy"`.
