# Darbot Variant Prompt Template (GenLM)

Use this when asking a generative model to design a new Darbot variant.

---

## Inputs you provide

- **Variant name:** `<Darbot Memory>`
- **Capability:** `<long-term memory / recall / knowledge base>`
- **Hero metaphor(s):** `<memory chip + spark>`
- **Where it will be used:** `<VS Code extension, FastAPI Swagger UI, npm>`
- **Must-match base:** `DarbotBase_v1.svg` (outer silhouette + visor geometry)

---

## Prompt

**Goal:** Create a Darbot variant logo using the existing Darbot base character.

### Hard constraints (non-negotiable)
- Keep the **outer silhouette path** and **visor outline path** exactly as in `DarbotBase_v1.svg`.
- Default face style: **visor only** (no mouth, no expressive facial features).
- Visor indicators: **three small rounded squares** in the top-left of the visor.
- The hero element must stay inside the body safe zone and be legible at **32px**.
- Output must be **SVG** with:
  - Groups: `#darbot-base`, `#darbot-visor`, `#darbot-visor-indicators`, `#darbot-visor-badge`, `#darbot-hero`, `#darbot-accents`
  - `viewBox="0 0 2048 2048"`
  - **No filters**, no blur, no feathering; flat fills/gradients only.
  - Minimal nodes; smooth curves.

### Style tokens
- Outer stroke: Darbot Spectrum gradient (or neon theme if specified).
- Visor fill: dark indigo gradient.
- Hero palette: use Darbot tokens where possible; keep contrast on dark backgrounds.

### Composition
- Keep hero centered at approx `(1024, 1230)`.
- Keep hero inside a safe circle with radius ~`420`.
- Maintain clear negative space between hero and visor + outer stroke.

### Deliverables
1) `darbot-<variant>_master.svg` (layered with groups)
2) `darbot-<variant>_transparent.png` @ 2048×2048
3) `darbot-<variant>_icon.png` @ 512×512 and 128×128

---

## What the model should do before finalizing (self-audit)

- Render the SVG at **16, 32, 64, 128, 256, 512**.
- Check:
  - The base silhouette + visor proportions did not shift.
  - The hero is readable at 32px.
  - No unexpected thickening from strokes (prefer layered fills for bordered shapes).
  - No micro-segments/jagged edges.

