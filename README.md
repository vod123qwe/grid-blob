# Grid Blob

A single-file web tool for generating banner graphics in a grid / metaball ("goo") style. Paint cells on a grid and adjacent ones melt together into soft, organic blobs — then export the result as a **true-vector SVG**, a raster **PNG/JPG**, or copy the SVG straight to your clipboard and paste it into Figma as editable vectors.

**Live:** https://vod123qwe.github.io/grid-blob/

## What it does

You lay out a grid over an artboard and click (or drag) to fill cells. Neighbouring filled cells — including diagonals — are fused by an SVG goo filter into one rounded shape. On export the goo is *baked into real vector paths* (marching squares + Catmull-Rom smoothing), so the output is clean geometry with no filters — perfect for design tools.

## Features

- **Goo grid painting** — left-click/drag to paint, right-click/drag to erase; adjustable brush size (1–8).
- **Artboard / Grid / Box controls** — dimensions, padding, columns/rows, stroke, colours with alpha.
- **Figma-style fill editor** — Solid, Linear, Radial and Angular gradients with multi-stop editing, a draggable direction/position dial, and a reverse-gradient button. Works for both the artboard and the boxes.
- **Box shaping** — shape (square / circle / diamond / triangle / plus) plus two sliders: **Rounding** (how round the merged blob is) and **Connector** (how thick the bridges between cells are).
- **Style presets** — Custom / Blue / Purple / Silver / White, plus your own savable presets.
- **Templates** — Slider banner, Category banner, Custom; with a quick cell-size fit stepper.
- **Canvas** — zoom (Ctrl+wheel, Ctrl+0 to reset), pan (middle mouse, or hold H / Space), undo/redo (Ctrl+Z / Ctrl+Shift+Z).
- **Export** — SVG (true vector), PNG / JPG at 1×–4×, or **Copy SVG** to the clipboard.
- **Reset** — clear the canvas back to the selected style's base screen.

## Export to Figma

Two ways to get a result into Figma:

1. **Copy SVG** → on the Figma canvas press <kbd>Ctrl/Cmd</kbd> + <kbd>V</kbd>. The pasted SVG becomes editable vector layers (`#background`, `#grid`, `#boxes`).
2. **Export → SVG** → drag the downloaded `.svg` file into Figma.

There is also a native **Figma plugin** version of the same tool that inserts the result directly onto the canvas via `createNodeFromSvg`.

## Run locally

No build step. Either open `index.html` directly, or serve it:

```bash
node serve.js   # http://localhost:8790
```

## Tech notes

- Single `index.html`, no dependencies.
- Live preview uses an SVG goo filter (`feGaussianBlur` + `feColorMatrix` alpha threshold + `feFlood`/`feComposite`).
- Vector export rasterises the boxes' alpha, traces contours with marching squares (sub-pixel interpolation), and smooths each loop into a cubic-Bézier path.
