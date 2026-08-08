# Changelog

All notable changes to Chromascope will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] — 2026-08-08

### Added
- **File import**: Drag-and-drop and file picker support for `.swatches` (Procreate), `.ase` (Adobe Swatch Exchange), `.aco` (Adobe Color Table), `.gpl` (GIMP Palette). Multiple files can be loaded simultaneously; each becomes a separate palette tab.
- **7 color naming libraries** bundled locally: meodai/color-names (4,959 entries), Name That Color/ntc.js (1,566), CSS/HTML named colors (138), X11 (138), xkcd color survey (949), Pantone approximations (118), Basic (20). The active library is selectable in Settings.
- **Live color renaming**: Changing the naming format in Settings instantly updates all displayed color names across the entire app. This works because raw RGB data is stored separately from display names; names are computed on demand via nearest-neighbor search in CIELAB space. PaletteStudio gets this wrong (requires re-import); Chromascope handles it correctly by design.
- **Color detail panel**: Slide-in panel showing all color codes (HEX, RGB, HSL, HSB, CMYK, LAB) with click-to-copy on each row.
- **Visual color editor**: Saturation/brightness canvas with pointer drag, hue slider, numeric inputs for HEX, RGB, and HSV. Edits are applied to the in-memory palette and persisted on panel close.
- **Harmony views**: Six palette view modes — Palette Only, Complementary, Analogous, Triadic, Split-Complementary, Tetradic. In harmony modes, related colors appear as small chips beneath each swatch.
- **Quick-export strip**: One-click export to `.ase`, `.gpl`, `.swatches`, and PNG image. No modal, no extra steps.
- **4 theme options**: Dark (Black), Dark (Dark Grey), Dark (Light Grey), Light. Dark Black is the default.
- **Font size control**: Adjustable via range slider in Settings.
- **IndexedDB persistence**: Loaded palettes survive page reloads. Settings stored in localStorage.
- **Embedded assets**: Site icon (rainbow) as favicon and header icon; personal logo in footer. All base64-encoded inline — no external image requests.
- **All color math implemented inline**: HEX↔RGB, HSL, HSV, CMYK, and CIELAB conversions plus harmony generation (complementary, analogous, triadic, split-complementary, tetradic) — no runtime dependency on chroma.js.
- **JSZip bundled inline** for `.swatches` file parsing (Procreate format is a ZIP containing `Swatches.json`).
- **Privacy-first architecture**: Single-file HTML, fully client-side, no CDN loads, no network requests, no tracking.

### Technical Notes
- **ACO parser**: Supports RGB, HSB, CMYK, Grayscale, and LAB color spaces in the v1 ACO format. LAB-to-RGB conversion is approximate (converts to grayscale as a fallback); a full LAB→XYZ→RGB pipeline would improve accuracy. This parser has not yet been tested against real ACO files — treat as provisional.
- **Swatches parser**: Expects the Procreate `.swatches` ZIP format containing `Swatches.json` with HSV color data. Older `.swatches` formats or non-Procreate swatches files may use different internal structures.
- **.ase parser**: Handles RGB, CMYK, and Grayscale color models. LAB-model ASE entries are not yet supported.
