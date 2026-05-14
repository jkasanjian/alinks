# Editing products

Each category section of the page is driven by its own JSON file in this `data/` folder. To update what shows on the site, edit the relevant file — no HTML changes needed.

## Files

| File             | Section on the page    |
| ---------------- | ---------------------- |
| `camera.json`    | Camera                 |
| `camping.json`   | Camping                |
| `hiking.json`    | Hiking                 |
| `snow.json`      | Snowboard              |
| `paddle.json`    | Beach & Lake           |
| `dog.json`       | Dog                    |

> **There is no `featured.json`.** The Featured carousel at the top of the page is built automatically from items in the files above — see [Featuring an item](#featuring-an-item) below.

## Each product looks like this

```json
{
  "title": "GoPro HERO12 Black",
  "price": 4,
  "bullets": [
    "What I filmed last week's hike on",
    "5.3K + HyperSmooth 6.0 stabilization",
    "Surprisingly good in low light at sunset"
  ],
  "placeholder": "Camera body",
  "from": "Amazon",
  "url": "https://amzn.to/your-affiliate-link",
  "video": "",
  "featured": true,
  "position": 1
}
```

### Fields

- **title** — product name shown on the card.
- **price** — number of filled `$` icons (0–4).
- **bullets** — short list of personal notes. 2–4 looks best.
- **placeholder** — text shown in the striped placeholder until you add a real product image (see below).
- **from** — the retailer label in the bottom-right of the card (e.g. `Amazon`, `REI`).
- **url** — your affiliate URL. Use `"#"` while you're still gathering links.
- **video** — link to a video you made about this product. Shows as a `MY VIDEO LINK →` badge **only when the item is featured**. Leave as `""` for no badge.
- **image** *(optional)* — a path to a product image (e.g. `"assets/products/gopro.jpg"`). If set, it replaces the placeholder. See `assets/products/README.md` for the full image workflow + recommended file specs.
- **featured** *(optional)* — set to `true` to also show this item in the Featured carousel at the top of the page. Omit or set `false` otherwise.
- **position** *(optional)* — the slot this item occupies in the Featured carousel. Lower numbers come first. Only matters when `featured` is `true`.
- **isAffiliated** *(optional)* — defaults to `true`. When `true` (or omitted), the card's "Link to buy" shows an asterisk (`*`) marking it as an affiliate link, consistent with the disclosure at the bottom of the page. Set to `false` for any link that is not an affiliate link.

## Featuring an item

To feature any product, open its category file, find the item, and add two fields:

```json
"featured": true,
"position": 1
```

The Featured carousel pulls every item across all category files where `featured` is `true`, then orders them by `position` ascending. The item stays in its real category section too — being featured just means it *also* appears at the top.

**If two items end up with the same `position`**, that's fine — the one whose title comes first alphabetically wins the earlier slot. (But ideally, keep positions unique.)

To unfeature, set `"featured": false` or just delete those two fields.

## Adding a product

1. Open the right `data/<section>.json` file.
2. Copy an existing `{ ... }` block, paste it where you want the card to appear (order in the file = order on the page).
3. Edit the fields. Save.
4. Refresh the page.

## Removing a product

Delete its `{ ... }` block (and the trailing comma if needed). Save.

## Tips

- **Order matters.** First in the file = leftmost card.
- **Watch your commas.** JSON requires a comma between items but **not** after the last one. If the page breaks, this is usually why.
- **Quotes inside strings.** Use a backslash: `"10\" sensor"`.
- **Run locally.** Because the page loads JSON via `fetch`, opening `index.html` directly with `file://` won't work in some browsers. Use any tiny static server, e.g. `python3 -m http.server` from the project folder.
