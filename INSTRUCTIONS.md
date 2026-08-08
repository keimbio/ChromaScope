# Chromascope — Setup & Usage Instructions

## Quick Start (Just Use It)

1. Open `chromascope.html` (or `index.html`) in any modern browser — Chrome, Safari, Firefox, or Edge.
2. Drop a palette file onto the window, or click **Import** in the top-right corner.
3. That's it — your colors appear immediately.

Everything runs locally in your browser. Nothing is uploaded anywhere.

---

## Supported File Formats

| Format | Extension | Source |
|--------|-----------|--------|
| Procreate Swatches | `.swatches` | Procreate (iPad) |
| Adobe Swatch Exchange | `.ase` | Illustrator, Photoshop, InDesign |
| Adobe Color Table | `.aco` | Photoshop |
| GIMP Palette | `.gpl` | GIMP, Inkscape, Krita |

You can drop multiple files at once — each becomes a separate tab.

---

## Using the App

### Viewing Colors
- Click any swatch to open the **detail panel** on the right
- The panel shows all color codes: HEX, RGB, HSL, HSB, CMYK, LAB
- Click any code row to copy it to your clipboard

### Editing Colors
- In the detail panel, use the **color picker** (the gradient square) to adjust saturation and brightness
- Use the **hue slider** (the rainbow bar below) to change the hue
- Or type values directly into the HEX, RGB, or HSB number fields
- Edits are saved when you close the panel

### Harmony Views
- Use the view tabs above the palette: **Complementary**, **Analogous**, **Triadic**, **Split-Comp**, **Tetradic**
- Each swatch shows its harmony colors as small chips underneath
- Click a chip to copy its hex value

### Changing Color Names
- Open **Settings** (gear icon, top-right)
- Under **Color Names → Naming Format**, pick a library:
  - **meodai** (default): 4,959 creative, community-curated names
  - **Name that Color (NTC)**: 1,566 traditional color names
  - **CSS/HTML**: The 138 standard web color names
  - **X11**: Classic X Window System color names
  - **xkcd Survey**: 949 names from Randall Munroe's color survey
  - **Pantone Approx.**: ~118 Pantone-inspired names
  - **Basic**: 20 simple names (red, blue, green, etc.)
- **Names update instantly** across the entire app — no need to re-import

### Exporting
- Use the **Export strip** below the view tabs:
  - **.ase** — Adobe Swatch Exchange (works with Illustrator, Photoshop)
  - **.gpl** — GIMP Palette (works with GIMP, Inkscape, Krita)
  - **.swatches** — Procreate Swatches (import back into Procreate)
  - **PNG** — Image of the palette with hex labels

---

## Deploying to GitHub Pages

If you want to host Chromascope online (e.g., at `yourusername.github.io/chromascope`):

1. Create a new GitHub repository named `chromascope` (or whatever you like)
2. Upload `index.html` to the root of the repo — that's the only file needed
3. Go to your repo's **Settings → Pages**
4. Under **Source**, select **Deploy from a branch**
5. Choose **main** branch and **/ (root)** folder, then click **Save**
6. After a minute, your site will be live at `https://yourusername.github.io/chromascope/`

### If you want to build from source:

1. Clone or download the full project (all folders: `src/`, `data/`, `lib/`)
2. Open Terminal
3. Type `cd ` (with a trailing space), then drag the project folder from Finder into the Terminal window
4. Press Enter
5. Run: `python3 assemble.py`
6. This creates/updates `index.html` in the project root

**Requirements for building:**
- Python 3 (already on macOS)
- Node.js (for JS syntax validation — install from [nodejs.org](https://nodejs.org) if needed)

---

## Troubleshooting

**"No Swatches.json found"** — The .swatches file might use a different internal format. Try re-exporting it from Procreate.

**Colors look wrong from .ase files** — Some ASE files use CMYK or LAB color spaces, which are converted to RGB. The conversion is approximate and may not perfectly match what you see in Adobe apps.

**Names don't change** — Make sure you're changing the naming format in Settings, not just browsing the dropdown. The change takes effect immediately on selection.

**File won't load** — Check the file extension. Chromascope supports `.swatches`, `.ase`, `.aco`, and `.gpl`. Other formats (like `.act`, `.clr`, `.pal`) are not currently supported.
