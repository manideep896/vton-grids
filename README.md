# VTON Benchmark — per-model grids

This repo hosts the interactive 10 × 16 try-on matrices for five VTON
models, part of a larger benchmark. Each grid is a real HTML table with
individual image cells, styled in a gold palette matching
[ionio.ai](https://www.ionio.ai).

## Live URLs (after enabling GitHub Pages)

- `/` — landing page with links to each model
- `/catvton.html` — CatVTON grid
- `/kling.html` — Kling (Kolors) grid
- `/qwen.html` — Qwen Image Max Edit grid
- `/fashn.html` — FASHN VTON 1.5 grid
- `/nano_banana_pro.html` — Nano Banana Pro grid

## Embedding in Webflow (or any site)

Each grid is a plain HTML file that works standalone. Embed in Webflow with an
Embed element:

```html
<iframe
  src="https://YOUR-USERNAME.github.io/YOUR-REPO/catvton.html"
  width="100%" height="2400" frameborder="0" loading="lazy"
  style="border:1px solid rgba(212,175,55,.25);border-radius:8px;">
</iframe>
```

Repeat for each model. Replace the `src` URL to match your GitHub Pages URL.

## Stats

- 799 individual try-on images (5 models × ~160 each)
- All images at 1024 max long-edge, JPEG quality 95
- Each grid page is ~5 KB HTML + lazy-loads the 186 images referenced

## Credits

Part of the VTON benchmark — five hosted models, 640 generations, full
engineering log at [ionio.ai](https://www.ionio.ai).
