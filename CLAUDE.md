# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

This is a **static, single-page affiliate site** for joshgoesoutside.com. No frameworks, no build step.

## Stack
- One `index.html` (HTML + inline CSS + inline JS, ~1000 lines)
- Product data in `data/*.json`, fetched at runtime
- Images in `assets/`

## Local dev
There is no `npm`/`make`. Just a static server, because `fetch` won't work over `file://`:
```bash
python3 -m http.server 8000
```

## Architecture (inline JS in `index.html`)

Render flow, all in `index.html`:
1. `SECTIONS` array (~line 794) maps each category to `{ key, file: 'data/<x>.json', target: '<dom-id>' }`. This array is the source of truth for which categories load.
2. `loadAll()` (~line 870) fetches all JSON files in parallel, calls `fillCarousel()` to render cards into each section's container, then builds the Featured carousel by filtering `featured: true` items across all categories and sorting by `position` (ties broken alphabetically by title).
3. `makeCard()` (~line 818) renders one product. All user-controlled strings go through `escapeHtml()` — keep it that way.
4. `showLoadError()` renders an in-place error card when a JSON fetch fails (e.g., served over `file://`).

**Adding a new category** requires changes in three places: a new `data/<name>.json` file, a new entry in `SECTIONS`, and a new `<section>` + carousel container in the HTML with the matching `target` id. The chip-nav `IntersectionObserver` (~line 942) also has a hardcoded section-id list — update it too, or the active-chip highlight won't work for the new section.

## Editing rules
- **Product content**: edit `data/<category>.json`. Schema is documented in `data/README.md`. Do NOT add fields without updating the rendering code in `index.html`.
- **Featured carousel**: built automatically from items across category files where `"featured": true`, ordered by `"position"`. There is no separate `featured.json`.
- **Page structure / styling / interactions**: edit `index.html` directly. Keep CSS and JS inline — that's the design choice for this project.
- **Images**: drop into `assets/products/`, reference by path in JSON. See `assets/products/README.md`.

## JSON gotchas
- Trailing commas break the page (it's parsed by `JSON.parse`).
- Order in the file = order on the page.

## Deploy target
GitHub Pages → custom domain `joshgoesoutside.com` (see `CNAME` and `README.md`). DNS lives at NameCheap.

## What NOT to do
- Don't introduce a build pipeline, bundler, or framework unless explicitly asked. The site is intentionally zero-dependency.
- Don't split `index.html` into multiple files unless asked.
- Don't add tracking/analytics without asking.
- Don't commit anything in `uploads/` — it's local scratch (already gitignored).
