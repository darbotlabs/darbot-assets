# darbot-assets

Centralized brand and logo assets for Darbot Labs products.

## Directory Structure

### Product-Specific Assets

#### `darbot-coder/`
Brand kit for Darbot Coder (neon terminal-green #00FF66 on deep black with soft glow).

- `master/` — High-resolution master files (1024, 2048, 4096px)
- `transparent/` — Transparent background versions (dark-only)
- `platforms/` — Platform-specific exports:
  - `android/` — Android launcher icons (36–512px)
  - `ios/` — iOS app icons (20–1024px)
  - `macos/` — macOS app icons (16–1024px)
  - `windows/` — Windows square tiles (120–310px)
  - `web/` — Web favicons and PWA icons
  - `emoji/` — Emoji-sized icons (32–128px)
  - `social/` — Social media banners (GitHub, LinkedIn, OpenGraph, Twitter)
- `darbot-coder-variants-svg/` — SVG design variants (A–D concepts, master versions v1–v5)
- `darbot_coder_emoji_pack/` — Flat and transparent emoji-style icons (18–1024px, includes ICO)
- `apps/web-darbot-coder/public/` — Web app assets (horizontal logos, OpenGraph image)
- `src/assets/` — Source assets for builds

#### `darbot-router/`
Logo pack for Darbot Router with comprehensive format coverage.

- `svg/` — Master SVG files (transparent and dark background)
- `png/` — PNG exports:
  - `transparent/` — Transparent background
  - `background/` — With background
- `png_rich_*/` — Rich/detailed PNG variants (bg, transparent, flatsteps)
- `jpg/` — JPEG exports:
  - `dark/` — Dark background
  - `white/` — White background
- `webp/` — WebP exports (+ transparent)
- `avif/` — AVIF exports (+ transparent)
- `ico/` — Windows ICO files (multi-resolution)
- `icns/` — macOS ICNS files
- `pdf/` — Vector PDF exports
- `platform/` — Ready-to-use platform assets:
  - `vscode/` — VS Code extension icon
  - `swagger/` — FastAPI/Swagger UI favicon
  - `web/` — Web favicons and Apple touch icons
  - `pwa/` — PWA manifest icons (192, 512, maskable)
- `previews/` — Preview images and OpenGraph
- `archive/` — Archived/legacy versions

#### `darbot-browser/`
Browser extension assets.
- Multi-resolution PNG icons (16–512px)
- ICO file for Windows

#### `darbot-windows/`
Windows desktop application assets.
- Logo icons (16–64px PNG, ICO)
- Third-party integration icons (npm, NuGet, VS)

#### `darbot-cli/`
CLI application assets (placeholder).

### Shared/Legacy Assets

#### `darbot_windows_logo_assets/`
Legacy Windows logo assets (similar to darbot-windows).

#### `DarbotAssetTemplate/`
Template directory for creating new asset packs.

### Agent Platform Assets

#### `darbotlabs_fde_agents_platform_pack/`
Full-stack agent icons (A1–A5 variants) with comprehensive platform exports.
- Each agent (A1–A5) includes:
  - SVG (neon, outline black/white)
  - `png/` — All sizes (16–1024px), neon and outline variants
  - `platform/` — Web, Windows, Teams, Power Platform icons
  - `print/` — Print-ready assets
- `manifest.json` — Asset metadata

#### `darbotlabs_VISA_fde_agents/`
VISA-branded FDE agent icons.
- `darbotlabs_A1–A5.svg` — Agent SVG files
- `mono/` — Monochrome variants

### Root Assets

| File | Description |
|------|-------------|
| `darbot-1024px.png` | Primary logo (1024px) |
| `darbot-horizontal-banner-1500x500.png` | Horizontal banner |
| `logo.png` | Standard logo |
| `darbot_logo_stylized.png` | Stylized logo variant |
| `manifest.json` | Root asset manifest |
| `A_digital_vector_graphic_design_*.png` | Generated vector design |
| `ChatGPT Image *.png` | AI-generated concept images |
| `DarbotAssetTemplate.zip` | Asset template archive |

## Usage Guidelines

- **Dark backgrounds**: Prefer dark backgrounds for neon glow effects (Darbot Coder)
- **Light backgrounds**: Place marks on a black/dark tile
- **Colors**: Avoid recoloring the neon green (#00FF66)
- **Shadows**: Avoid drop shadows where glow is already applied
- **Aspect ratio**: Keep icons square for app and favicon usage
- **Clear space**: Maintain ~8% of canvas as clear space around logos