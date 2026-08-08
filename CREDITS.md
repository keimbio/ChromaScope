# Credits & Attributions

## Color Naming Data

- **meodai/color-names** by David Aerne — [github.com/meodai/color-names](https://github.com/meodai/color-names) — MIT License. The "bestof" curated subset (4,959 color names) is bundled.
- **color-namer** by Zeke Sikelianos — [github.com/colorjs/color-namer](https://github.com/colorjs/color-namer) — MIT License. The NTC, Pantone, HTML, X11, and Basic name datasets are extracted from this package.
- **xkcd Color Survey** by Randall Munroe — [xkcd.com/color/rgb](https://xkcd.com/color/rgb/) — CC BY-NC 2.5. 949 color names from the 2010 xkcd color survey, accessed via the [xkcd-colors](https://www.npmjs.com/package/xkcd-colors) npm package.

## Libraries

- **JSZip** by Stuart Knightley — [stuk.github.io/jszip](https://stuk.github.io/jszip/) — MIT License. Used for parsing and creating Procreate `.swatches` files (ZIP format).

## Reference Implementations

- **Palette Studio** by Joan Roig — [github.com/joanroig/palette-studio](https://github.com/joanroig/palette-studio) — MIT License. The ASE parser logic and palette import/export patterns were studied as a functional reference during development. No code was directly copied; Chromascope's parsers and exporters were written from scratch in vanilla JS.

## Design

- Color math (RGB↔HSL/HSV/CMYK/LAB) implemented from published algorithms (Wikipedia, Bruce Lindbloom's site).
- UI design modeled on the Spectator and Claude Export Viewer tool family by Klara Keim.
