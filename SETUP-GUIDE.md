# End-to-end setup: GitHub Pages → Webflow embed

This folder hosts 5 interactive VTON grid pages styled in the Ionio gold
palette. Push it to a public GitHub repo, flip on Pages, and embed each page
into your Webflow article as an iframe. The whole setup takes 10-15 minutes.

## Part 1 — Upload to GitHub (5 minutes)

### Option A: GitHub web UI (no git needed)

1. Go to https://github.com/new
2. Name the repo something like `vton-grids` or `vton-benchmark-grids`.
3. Set **Public** (required for free GitHub Pages).
4. Check **Add a README file**. Click **Create repository**.
5. Once created, click **Add file** → **Upload files** at the top of the repo.
6. Drag this entire `vton-grids-github/` folder's CONTENTS (not the folder
   itself — open it and drag everything inside) into the browser window.
   You'll be uploading ~100 MB across 825 images plus 6 HTML files.
7. Scroll down, commit message: `initial grids`, click **Commit changes**.
8. Wait for the upload to finish (2-3 minutes for 100 MB over a reasonable
   connection).

### Option B: git CLI (if you already have git set up)

```bash
cd /Users/Ellendula.SaiManideep/Downloads/vton-grids-github
git init
git remote add origin https://github.com/YOUR_USERNAME/vton-grids.git
git add .
git commit -m "initial grids"
git branch -M main
git push -u origin main
```

## Part 2 — Turn on GitHub Pages (1 minute)

1. In your new repo, click **Settings** (top-right tab).
2. Left sidebar → **Pages**.
3. Under "Build and deployment":
   - **Source**: *Deploy from a branch*
   - **Branch**: `main` / `/ (root)`
   - Click **Save**.
4. GitHub starts building. Takes 30-60 seconds.
5. The page refreshes with a banner: *"Your site is live at
   https://YOUR_USERNAME.github.io/vton-grids/"*. Copy that URL.

**Test it**: open `https://YOUR_USERNAME.github.io/vton-grids/catvton.html`
in a new tab. You should see the full CatVTON grid with all 160 images.

## Part 3 — Embed into Webflow (5 minutes per grid × 5 grids)

For each grid you want in your article:

1. In Webflow Designer, open your blog-post page or template.
2. Drag an **Embed** element (found under Components → Embed) into the
   article where you want the grid.
3. Paste this HTML, replacing the URL with your GitHub Pages URL:

```html
<iframe
  src="https://YOUR_USERNAME.github.io/vton-grids/catvton.html"
  width="100%"
  height="2400"
  frameborder="0"
  loading="lazy"
  style="border:1px solid rgba(212,175,55,.25);border-radius:8px;background:#fff;">
</iframe>
```

4. Click **Save & Close**. Repeat the Embed for each of the 5 models:
   - `catvton.html`
   - `kling.html`
   - `qwen.html`
   - `fashn.html`
   - `nano_banana_pro.html`

**Height tuning**: 2400 px is right for a full 10 × 16 grid at default cell
size. If your Webflow breakpoint is narrower than 1100 px, the iframe will
get a horizontal scrollbar inside the embed — this is intentional, the grid
is wide and meant to be scrolled horizontally on smaller screens.

## Part 4 — Optional niceties

**Landing page embed**. If you want one clean "see all models" card on the
blog before the individual grids, embed `index.html` too:

```html
<iframe src="https://YOUR_USERNAME.github.io/vton-grids/"
  width="100%" height="800" frameborder="0" loading="lazy"></iframe>
```

**Custom domain** (optional). In GitHub repo Settings → Pages → Custom
domain, you can set something like `grids.ionio.ai` if you add a CNAME
record in your DNS pointing to `YOUR_USERNAME.github.io`. Makes the iframe
URL cleaner.

**Responsive iframe trick**. Webflow's default Embed doesn't auto-resize.
If you want the iframe to auto-fit its content height, wrap it:

```html
<div style="position:relative;padding-top:56.25%;">
  <iframe src="..."
    style="position:absolute;inset:0;width:100%;height:100%;border:0;"
    loading="lazy"></iframe>
</div>
```

But this only gives an aspect-ratio fix, not true content fit. Easiest is
to set an explicit height like 2400 and let the inner grid scroll.

## Why iframes (and not some fancier integration)

- **Respects the gold palette.** The iframe loads exactly the HTML you
  built, no CSS conflicts with Webflow's own styles.
- **Updates propagate.** Change a file in the GitHub repo, it's live
  everywhere it's embedded within seconds.
- **Zero maintenance.** No Webflow CMS collections to keep in sync, no
  asset manager to re-upload 800 images.
- **SEO note**: iframes' content isn't as discoverable by search engines
  as native page content. If SEO for the grid pages matters, also link to
  the GitHub Pages URLs directly from the blog body.

## Troubleshooting

**Pages shows 404 after enabling**: GitHub Pages takes up to a minute the
very first time. Refresh after 60 seconds.

**Images don't load inside the iframe**: Make sure you uploaded the
`images/` folder too. The HTML pages reference images via relative paths
(`images/thumbs/p01.jpg`, `images/catvton/…jpg`).

**Webflow shows a broken iframe**: Webflow's Embed has a 10 KB size limit
on the embed HTML — our iframe tag is well under that. If it still
complains, use the **HTML Embed Widget** component instead, which has a
50 KB limit.

**Images are slow to load**: They're lazy-loaded (see the `loading="lazy"`
attribute in each cell). Scroll slowly the first time to let the browser
fetch them. Subsequent views are cached.

## Folder structure that's getting uploaded

```
vton-grids-github/              (this folder — upload its contents to GitHub)
├── README.md                   shows on the repo homepage
├── SETUP-GUIDE.md              this file
├── .nojekyll                   tells GitHub Pages to serve files as-is
├── index.html                  landing page with links to 5 grids
├── catvton.html                CatVTON full 10×16 grid
├── kling.html                  Kling (Kolors) grid
├── qwen.html                   Qwen Image Max Edit grid
├── fashn.html                  FASHN VTON 1.5 grid
├── nano_banana_pro.html        Nano Banana Pro grid
└── images/
    ├── thumbs/                 p01–p10.jpg + g01–g16.jpg (26 label thumbs)
    ├── catvton/                160 result JPGs
    ├── kling/                  160 result JPGs
    ├── qwen/                   160 result JPGs
    ├── fashn/                  160 result JPGs
    └── nano_banana_pro/        159 result JPGs
```

Total: 825 images, 102 MB. Well under GitHub's 1 GB per-repo soft limit.
