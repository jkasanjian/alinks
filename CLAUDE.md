# Claude Code context

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
