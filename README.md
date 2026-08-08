# ChromaScope

**Color Palette Viewer, Editor & Converter** — a fully client-side, single-file HTML tool for working with color palettes from Procreate, Adobe, GIMP, and other sources.

## Features

- **Import**: Drag-and-drop or file picker for `.swatches` (Procreate), `.ase` (Adobe Swatch Exchange), `.aco` (Adobe Color), `.gpl` (GIMP Palette)
- **Multiple palettes**: Load several files simultaneously; switch between them via tabs
- **7 color naming libraries**: meodai/color-names (4,959), Name That Color (1,566), CSS/HTML (138), X11 (138), xkcd Survey (949), Pantone approximations (118), Basic (20) — **live-rename on format change**
- **Color detail panel**: Click any swatch to see all color codes (HEX, RGB, HSL, HSB, CMYK, LAB) with click-to-copy
- **Visual color editor**: Saturation/brightness canvas + hue slider + numeric inputs (HEX, RGB, HSV)
- **Harmony views**: Palette-only, Complementary, Analogous, Triadic, Split-Complementary, Tetradic
- **Export**: Quick-export strip — `.ase`, `.gpl`, `.swatches`, PNG image
- **Settings**: 4 themes (Dark Black, Dark Grey, Dark Light Grey, Light), font size control, naming format selector
- **Persistence**: Palettes stored in IndexedDB; settings in localStorage
- **Privacy**: All processing runs in-browser — no server, no uploads, no tracking

## Architecture

Single-file HTML/CSS/JS app (428 KB), assembled from source components via `assemble.py`:

```
src/
  template.html    — HTML shell with {{placeholders}}
  styles.css       — CSS with design tokens, 4 themes
  app.js           — Application logic (color math, parsers, UI)
data/
  meodai.json      — meodai/color-names bestof dataset (4,959 entries)
  ntc.json         — Name That Color dataset (1,566)
  html.json        — CSS/HTML named colors (138)
  x11.json         — X11 color names (138)
  xkcd.json        — xkcd color survey (949)
  pantone.json     — Pantone approximations (118)
  basic.json       — Basic color names (20)
  favicon.b64      — Site icon (64×64 PNG, base64)
  header-icon.b64  — Header icon (40×40 PNG, base64)
  logo.b64         — Footer logo (200×200 PNG, base64)
lib/
  jszip.min.js     — JSZip 3.x (97 KB, MIT license)
assemble.py        — Build script with JS validation
index.html         — Assembled output
```

### Key design decisions

- **Live color renaming**: Color data is stored as raw RGB. Display names are computed on demand from the active naming library. Changing the library in Settings triggers a re-render, updating all visible names instantly — no re-upload or page reload required.
- **IndexedDB for persistence**: Avoids the localStorage quota limits encountered in earlier projects. Palettes survive page reloads.
- **Color naming via LAB distance**: The nearest-name algorithm converts both the target color and every library entry to CIELAB space and finds the minimum Euclidean distance — the same approach used by the `color-namer` npm package.
- **All color math is custom**: No dependency on chroma.js at runtime. HEX↔RGB, HSL, HSV, CMYK, and LAB conversions are implemented inline (~150 lines).

## Dependencies & Licenses

| Library | Version | License | Purpose |
|---------|---------|---------|---------|
| [JSZip](https://stuk.github.io/jszip/) | 3.x | MIT | Parse/create `.swatches` files (Procreate ZIP format) |
| [meodai/color-names](https://github.com/meodai/color-names) | bestof | MIT | 4,959 curated color names |
| [color-namer](https://github.com/colorjs/color-namer) | datasets | MIT | NTC, Pantone, HTML, X11, Basic, ROYGBIV name lists |
| [xkcd-colors](https://github.com/JonathanVanSchenwordsck/xkcd-colors) | — | CC-BY-NC 2.5 (survey data) | 949 xkcd color survey names |

All libraries are bundled inline — no CDN requests, no external network calls.

## Building from source

```bash
python3 assemble.py
```

Requires Node.js (for `--check` JS validation). Outputs `index.html`.
