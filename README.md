# joshgoesoutside.com

Personal affiliate-link site — gear I actually use on hikes, snowboard trips, paddles, and dog adventures.

Static HTML/CSS/JS. No build step. Product data is loaded at runtime from JSON files in `data/`.

---

## Project structure

```
.
├── index.html               # The whole site (HTML + CSS + JS)
├── data/                    # Product data, one file per category
│   ├── camera.json
│   ├── camping.json
│   ├── hiking.json
│   ├── snow.json
│   ├── paddle.json
│   ├── dog.json
│   └── README.md            # How to edit products / feature items
├── assets/
│   ├── cover.jpg            # Hero image
│   ├── profile.jpg          # Avatar
│   ├── products/            # Product images (optional, see README inside)
│   └── products/README.md
├── CNAME                    # Custom domain for GitHub Pages
└── README.md
```

---

## Run locally

Because the page loads JSON via `fetch`, opening `index.html` with `file://` won't work in most browsers. Use any tiny static server:

```bash
# from the project folder
python3 -m http.server 8000
# then open http://localhost:8000
```

Or with Node:

```bash
npx serve .
```

---

## Editing content

- **Products** → edit JSON in `data/`. See [`data/README.md`](data/README.md).
- **Product images** → drop into `assets/products/` and reference from the JSON. See [`assets/products/README.md`](assets/products/README.md).
- **Hero / profile / copy** → edit `index.html` directly.

---

## Deploying to joshgoesoutside.com

The repo is set up for **GitHub Pages** with a custom domain. The included `CNAME` file tells GitHub Pages to serve the site at `joshgoesoutside.com`.

### 1. Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

### 2. Enable GitHub Pages

1. Go to the repo on GitHub → **Settings** → **Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Choose **Branch: `main`**, **Folder: `/ (root)`**, and **Save**.
4. Wait ~1 minute for the first build. GitHub will show the live URL.

### 3. Point your NameCheap domain at GitHub Pages

In NameCheap → **Domain List** → **Manage** `joshgoesoutside.com` → **Advanced DNS**, set these records (delete the default NameCheap parking records first):

| Type    | Host  | Value                  | TTL       |
| ------- | ----- | ---------------------- | --------- |
| A       | `@`   | `185.199.108.153`      | Automatic |
| A       | `@`   | `185.199.109.153`      | Automatic |
| A       | `@`   | `185.199.110.153`      | Automatic |
| A       | `@`   | `185.199.111.153`      | Automatic |
| CNAME   | `www` | `<your-username>.github.io.` | Automatic |

Replace `<your-username>` with your GitHub username. The trailing dot on the CNAME is important.

### 4. Verify in GitHub

Back in **Settings → Pages**:

- The **Custom domain** field should already say `joshgoesoutside.com` (from the `CNAME` file).
- Once DNS propagates (usually 15 min – a few hours), GitHub will issue an HTTPS certificate.
- Tick **Enforce HTTPS**.

You're live.

### Alternative: Netlify or Vercel

Both work too and are arguably easier than Pages:

- **Netlify**: `netlify deploy --prod` from this folder, or connect the GitHub repo in the Netlify dashboard. Add `joshgoesoutside.com` as a custom domain; Netlify gives you DNS values to paste into NameCheap.
- **Vercel**: same flow with `vercel --prod` or via the dashboard.

If you go this route, delete the `CNAME` file (it's GitHub-Pages-specific).

---

## License

Personal project. All product names and links belong to their respective owners.
