# GLCD Font Bitmap Viewer

A browser-based tool for visualising bitmap font data used in Graphic LCD (GLCD) display libraries. Load a `.h` font header file and instantly see every glyph rendered from the raw hex byte arrays.

**Try it live:** [https://euankirkhope.github.io/GLCDFontViewer/](https://euankirkhope.github.io/GLCDFontViewer/)

## Supported Table Formats

| Format | Header | Width | Description |
|---|---|---|---|
| **STANG** | None | Fixed | No header bytes. Each character is `W × ⌈H/8⌉` bytes of column data, packed sequentially. |
| **MIKRO** | 4-byte | Fixed | Header: `[width, height, firstChar, lastChar]`. Character data follows immediately. |
| **GLCD_UTILS** | 4-byte | Variable | Header: `[maxWidth, height, firstChar, charCount]`. Each character record starts with a width byte, padded to `1 + maxW × ⌈H/8⌉`. |

All formats use column-major, LSB-first bit ordering (bit 0 = top row).

## Usage

1. Open the viewer in a browser.
2. Drop a `.h` font file onto the drop zone (or click to browse).
3. The viewer auto-detects the table format and font dimensions from the array name and byte layout.
4. Adjust parameters manually if needed:
   - **Table Format** — Auto-detect, STANG, MIKRO, or GLCD_UTILS.
   - **Header** — Auto, 4-byte header, or No header. Selecting "No header" skips the first 4 bytes but still applies the chosen format's record layout.
   - **Font Width / Height** — Glyph dimensions in pixels.
   - **First Char** — ASCII code of the first character in the array.
   - **Pixel Scale** — Zoom level for rendering.
   - **On Color** — Pixel colour (green, white, blue, amber, pink).

## File Compatibility

Accepts `.h`, `.c`, `.hpp`, `.cpp`, and `.txt` files. The parser extracts all `0x__` hex bytes from the first `{ ... }` block found in the file, and attempts to read the array name from a preceding declaration (e.g. `const char Font5x7[] PROGMEM = { ... };`).

Dimension auto-detection looks for patterns like `Font5x7`, `font_8x16`, or `Font12x24` in the array name.

## License

The Unlicense

## AI

100% created by Claude...
