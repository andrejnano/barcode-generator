# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A client-side barcode generator web app that bulk-generates QR codes and EAN-13 barcodes from CSV input, packages them into a ZIP, and downloads it. Everything runs in the browser — no backend.

## Architecture

Single-file app: `index.html` contains all HTML, CSS, and JavaScript inline. No build step, no bundler, no framework.

**CDN dependencies** (loaded via `<script>` tags):
- **PapaParse** — CSV parsing
- **bwip-js** — barcode/QR rendering to canvas
- **JSZip** — ZIP file creation
- **FileSaver.js** — triggers browser download

**Flow:** CSV input (paste or file upload) → PapaParse → validation & preview table → bwip-js renders each barcode to canvas → canvas.toBlob → JSZip → FileSaver download.

**CSV column detection** is fuzzy — looks for headers containing "name"/"product", "qr"/"url"/"link", "ean"/"barcode"/"gtin" (case-insensitive).

## Development

No install or build required. Open `index.html` in a browser or serve with any static server:

```
python3 -m http.server 8000
# or
npx serve .
```

Deployed to Vercel as a static site (`vercel.json` sets no build command and serves from `.`).

## Key Functions

- `parseCSV()` — parses input, detects columns, validates EAN-13 format, populates preview
- `generate()` — iterates parsed rows, renders barcodes via `renderToCanvas()`, builds ZIP
- `sanitizeFilename()` — strips unsafe chars for ZIP entry names
