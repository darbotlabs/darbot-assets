# Darbot Asset Refinement Workflow (playbook)

This is the “strip it down, validate, build it back up” workflow used to get **pixel-faithful** and **audit-friendly** SVG assets.

The goal is repeatability: any new Darbot variant can follow this and land in the same quality band.

---

## 0) Decide which output you’re making

You usually want two deliverables (same geometry):

1) **Core icon asset** (the one that ships in products)
   - No filters, no blur, no feathering
   - Clean geometry, minimal nodes
   - Works at 16–128 px

2) **Marketing render** (optional)
   - Can include subtle glows, background gradients, textures
   - Not required for product icons

If you don’t explicitly need marketing styling, treat everything as a *core icon asset*.

---

## 1) Start from the base

- Import `DarbotBase_v1.svg` or `DarbotVariantTemplate_v1.svg`.
- Lock the base group (`#darbot-base`).
- Create the new hero art in `#darbot-hero`.

**Invariant:** never change the `d` attributes of:
- `#darbot-outline`
- `#darbot-visor-shape`

---

## 2) Reduce the reference image to truth

When vectorizing from a raster reference:

### A) Strip to a clean binary mask
- Convert to grayscale
- Increase contrast (aggressively)
- Threshold to a *binary* mask (choose a threshold that preserves edges)
- Apply a small morphological close/open to remove speckle noise

### B) Separate “ink” from “fill”
For assets with thick strokes:
- If you need an **outline-only** vector, isolate the stroke band via edge detection / contour finding.
- If you need **border + fill** (like rounded blocks), prefer **two-layer fills** rather than centered strokes.

---

## 3) Vectorize, then *de-noise the geometry*

### A) Vectorization (initial)
- Use a tracing method that returns polylines/curves.
- Keep a high-enough resolution so curves aren’t underfit.

### B) Node reduction
- Remove micro-segments.
- Replace stair-stepped paths with smooth Béziers.
- Target a “node budget” for each element:
  - Outer contour: as few anchors as possible while preserving shape
  - Visor: low anchor count, smooth corners
  - Hero symbols: low-to-medium anchors (readability > exactness)

### C) Continuity
- Ensure curves are smooth (no visible kinks).
- Prefer consistent curvature (G2/C2-like smoothness) over pointy joins.

---

## 4) Self-validation loop (the most important step)

### A) Render and compare at multiple scales
Render the SVG at:
- 16, 32, 64, 128, 256, 512

Inspect for:
- edge jaggies
- tiny spikes at joins
- thick/thin artifacts
- anything that disappears or muddies at 32px

### B) Overlay check against reference
If you have a raster reference:
- Render SVG to the reference size
- Overlay/blend difference
- Fix any drift in proportions before doing “beautification”

### C) Proportion drift prevention
Common causes:
- Using centered strokes when the reference is “border ring + fill”
- Corner radius too large (turns rounded rects into pills)

Fix:
- Build “bordered” shapes using **two rectangles** (outer + inner) instead of strokes.

---

## 5) Colorization without geometry drift

Rules:
- Don’t change path geometry to “make color look better.”
- Use gradients as paint only.
- Keep a separate **flatsteps** version for icon crispness.

Recommended deliverables:
- `*_master.svg` (rich gradients)
- `*_flatsteps.svg` (banded gradients)
- `*_mono.svg` (single-color)

---

## 6) Export spec + packaging

Export the matrix from the README. Package outputs with:
- predictable filenames
- `platform/` aliases (VS Code, swagger, web)
- `previews/` with side-by-side + overlay renders

---

## 7) Final audit checklist

- [ ] Base silhouette + visor geometry unchanged
- [ ] No filters/blur in core icon assets
- [ ] Clean joins/caps, no micro spikes
- [ ] Hero readable at 32px
- [ ] Transparent PNG + background PNG present
- [ ] ICO/ICNS/favicons generated
- [ ] Preview renders included

