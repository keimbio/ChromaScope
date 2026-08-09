# Changelog

All notable changes to ChromaScope will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] — 2026-08-09

### Added
- **File import**: Drag-and-drop and file picker for `.swatches` (Procreate), `.ase` (Adobe Swatch Exchange), `.aco` (Adobe Color Table), `.gpl` (GIMP Palette). Multiple files simultaneously; each file becomes a separate palette tab.
- **Procreate `.swatches` parser**: Correctly handles the Procreate ZIP format containing `Swatches.json` with HSV color data (hue/saturation/brightness as 0–1 floats). Handles the array-wrapping variant (some Procreate versions wrap the object in an array) and null entries (empty slots in Procreate's 30-color grid). Based on analysis of the `procreate-swatches` npm package's actual read logic.
- **ASE parser**: Handles RGB, CMYK, and Grayscale color models. Correctly reads the block-based format with UTF-16 color names and IEEE 754 float color channels.
- **ACO parser**: Handles RGB (space 0), HSB (space 1), CMYK (space 2), and Grayscale (space 8) color spaces in v1 format.
- **GPL parser**: Standard GIMP Palette text format.
- **7 color naming libraries** bundled locally: meodai/color-names (4,959), Name That Color (1,566), CSS/HTML (138), X11 (138), xkcd Survey (949), Pantone approximations (118), Basic (20).
- **Live color renaming**: Changing the naming format in Settings instantly re-renders all displayed names. Raw RGB is stored; names are computed on demand via nearest-neighbor search in CIELAB space. This is the correct approach that PaletteStudio gets wrong (it bakes names at import time).
- **Color detail panel**: Slide-in panel with all color codes (HEX, RGB, HSL, HSB, CMYK, LAB), click-to-copy on each row.
- **Visual color editor**: Saturation/brightness canvas with pointer drag, hue slider with drag, numeric inputs for HEX, RGB, and HSV. Edits are persisted to IndexedDB on panel close.
- **6 harmony view modes**: Palette Only, Complementary, Analogous, Triadic, Split-Complementary, Tetradic. In harmony modes, related colors appear as chips beneath each swatch.
- **Quick-export strip**: One-click export to `.ase`, `.gpl`, `.swatches`, and PNG.
- **Color selection**: Ctrl/Cmd+click to multi-select individual swatches. Floating selection bar shows count with Export PNG and Clear buttons.
- **Column control**: 2/3/4/5/6 column grid selector in the toolbar (Spectator-style pill toggles).
- **Size control**: S/M/L/XL font size pills in the header (Spectator-style).
- **4 theme options**: Dark (Black), Dark (Dark Grey), Dark (Light Grey), Light.
- **Background customization**: 4 preset gradients + custom image upload, with dimming slider (modeled on claude-export-viewer).
- **Font size slider** in Settings, synced with the header size pills.
- **IndexedDB persistence** for palettes; localStorage for settings.
- **Swatches export**: Correctly pads to 30 slots with null entries (matching Procreate's expected format).
- **Spectator-style header**: Logo icon + title in Hanken Grotesk Light, size pills, import button, settings gear.
- **Spectator-style footer**: Version badge, GitHub link, privacy statement, credit with logo.
- **All color math inline**: No chroma.js dependency. RGB↔HEX/HSL/HSV/CMYK/LAB conversions + harmony generation.
- **JSZip bundled** for `.swatches` file parsing/creation.
- **Privacy-first**: Single-file HTML, fully client-side, no CDN, no network, no tracking.
