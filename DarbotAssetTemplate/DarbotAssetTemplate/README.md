# Darbot Asset System Template

This folder is a repeatable template for creating, iterating, refining, and shipping **Darbot** logo/icon variants.

It encodes two things:

1) A **stable base character** (ghost silhouette + visor geometry) used across variants.
2) A **repeatable workflow + export spec** so every variant ships with the same high-quality, platform-ready assets.

---

## 1) The Darbot “base character”

**Canonical base:** `base/DarbotBase_v1.svg`

This is the answer to:
> “If the user asked for a logo for Darbot Memory or Darbot Games, what is the base character and visor outline used for all?”

Use **DarbotBase_v1** as the unchanging foundation:
- **Outer silhouette** (ghost contour)
- **Visor outline + visor fill area**
- **Default visor indicator cluster** (three rounded squares)

Everything else belongs to the variant (hero + accents).

### Brand neutrality rules
- Default face = **visor only**.
- Avoid mouths or expressive faces (reduces bias/judgement; keeps Darbot friendly/neutral).
- Exceptions should be rare and intentional (e.g., “Darbot Coder” as a special, terminal-inspired style).

---

## 2) Variant schema (repeatable, but still unique)

A Darbot variant is composed of **modules**:

1) **Base** (unchanged)
   - Silhouette stroke
   - Visor
   - Indicators (three slots)

2) **Hero element** (unique per capability)
   - One dominant symbol that represents the intended use case
   - Simple geometry that stays readable at 32px

3) **Accents** (optional)
   - Glitch, sparkles, secondary badge, etc.
   - Must not alter the base silhouette/visor geometry

Use `templates/variant_manifest_template.yaml` to define variants consistently.

### Designing unique hero elements within a fixed schema
Use these constraints to keep “infinite variety” without losing brand cohesion:

- **Single idea, strongly expressed**
  - Example: Browser = globe + bolt; Router = chip + wires; Memory = chip + stack/recall cue.

- **One stroke language** per variant
  - Prefer monoline or “border ring + fill” shapes.
  - Avoid mixing many unrelated stroke weights.

- **Stay inside the hero safe zone**
  - Recommended (2048 viewBox): center `(1024, 1230)`, radius `~420`.
  - Maintain clean negative space to the visor and the outer silhouette.

- **Re-use tokens (colors, radii, stroke weights)**
  - Consistent “design DNA” makes the variant feel like Darbot even when the hero changes.

---

## 3) Working files and SVG structure

### Required SVG group IDs
Every master SVG should preserve these groups so tooling can automate edits/exports:

- `#darbot-base`
- `#darbot-visor`
- `#darbot-visor-indicators`
- `#darbot-visor-badge` (optional)
- `#darbot-hero`
- `#darbot-accents`

### Geometry invariants
- Do **not** change the base silhouette or visor path data.
- Keep the `viewBox="0 0 2048 2048"`.
- Prefer **layered fills** for bordered shapes (prevents “stroke makes it bigger” distortions).
- Minimize nodes and use smooth curves (avoid micro-segments).

---

## 4) Repeatable iteration workflow

A reliable loop that works across tools and keeps you out of “SVG slop”:

### Phase A — Concept
- Define the **capability** and choose a **hero metaphor**.
- Sketch a rough hero symbol that will read at 32px.

### Phase B — Vector build (clean geometry)
- Start from `templates/DarbotVariantTemplate_v1.svg`.
- Build hero + accents as clean vector shapes:
  - Smooth curves
  - Minimal anchors
  - Consistent corner radii

### Phase C — Visual audits (multi-scale)
Render and review at:
- **16, 32, 64, 128, 256, 512**

Check:
- Base silhouette + visor proportions are unchanged.
- No jagged edges, spikes, micro segments.
- Hero legible at 32px.
- No stroke-induced size drift.

### Phase D — Color + icon-friendly flattening
Ship **two** colored masters when gradients are used:
- **Rich gradient** version (closest to the “hero render”)
- **Flattened / step gradient** version (crisper for icons + better compression)

### Phase E — Export pack
Export the standard format matrix (below) and include platform-friendly filenames.

---

## 5) Export spec (sizes + formats)

Every Darbot variant should ship:

### Vector
- `darbot-<variant>_master.svg` (layered, editable)
- `darbot-<variant>_flatsteps.svg` (icon-friendly)
- `darbot-<variant>_mono.svg` (monochrome outline)

### Raster (PNG)
Transparent PNGs at:
- 16, 24, 32, 48, 64, 96, 128, 180, 192, 256, 512, 1024, 2048

Optional (nice-to-have):
- WebP + AVIF at 32, 64, 128, 256, 512, 1024

### Favicons / app icons
- `favicon.ico` (16/32/48)
- `Darbot<Variant>.ico` (16/24/32/48/64/128/256)
- `Darbot<Variant>.icns` (macOS sizes up to 1024)
- `apple-touch-icon.png` (180)
- `android-chrome-192x192.png`
- `android-chrome-512x512.png`
- `maskable_icon_512.png`

### Social / docs
- `og-image_1200x630.png`

### Platform “aliases” (copy/rename)
- VS Code extension: `icon.png` @ 128×128
- Swagger UI: `favicon.ico` (and optionally `logo-32.png`)
- npm / README: 512 or 1024 PNG (transparent)

---

## 6) Prompting template for GenLM

Use `docs/prompt_template.md`.

It forces:
- Base geometry invariants
- Group structure
- No filters/blur
- Multi-size self-audit before final output

---

## Files in this template

- `base/DarbotBase_v1.svg` — canonical base character + visor
- `templates/DarbotVariantTemplate_v1.svg` — master SVG scaffold for new variants
- `templates/variant_manifest_template.yaml` — repeatable schema for variants
- `docs/prompt_template.md` — prompting template for GenLM

