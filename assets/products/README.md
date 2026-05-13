# Product images

Drop your product photos in this folder, then reference them from the JSON files in `/data/`.

## How to add an image to a card

1. **Save the image here.** Use a short, lowercase, hyphenated filename — e.g. `gopro-hero12.jpg`, `peak-design-tripod.jpg`. Avoid spaces and capital letters; they make URLs messy.
2. **Open the matching JSON** in `/data/` (e.g. `data/featured.json` for the Featured row).
3. **Add an `image` field** to the product:

   ```json
   {
     "title": "GoPro HERO12 Black",
     "brand": "GoPro",
     "image": "assets/products/gopro-hero12.jpg",
     ...
   }
   ```

4. **Refresh the page.** The striped placeholder is replaced by your photo.

If `image` is missing or the path is wrong, the card falls back to the striped placeholder with the `placeholder` text — handy while you're still gathering photos.

## File specs

| Property        | Recommendation                                                |
| --------------- | ------------------------------------------------------------- |
| **Format**      | `.jpg` for photos, `.png` if you need transparency            |
| **Aspect**      | 4:3 (regular cards) or 5:4 (Featured row). Anything works — the card crops to fit, centered. |
| **Resolution**  | ~800×600 px is plenty. Cards display at ~280px wide.         |
| **File size**   | Aim for < 200 KB each. Compress with [Squoosh](https://squoosh.app) or [TinyPNG](https://tinypng.com). |
| **Naming**      | `kebab-case.jpg` — no spaces, no capitals                     |

## Total budget

You have ~20 products. At 150 KB average, the whole gallery is ~3 MB — fast on every connection, and the project stays fully self-contained (no broken links if a cloud host changes its terms).

## Where to get product images

- **The manufacturer's site** — usually the cleanest shots. Right-click → Save image as.
- **Your own photos** — best for personality. A real photo of your gear in the wild beats a stock studio shot every time.
- **Retailer pages** (Amazon, REI, etc.) — fine for personal/affiliate use; the brands generally want their gear shown.

Check the licensing if you're unsure — most brands are happy to be featured on an affiliate page.
