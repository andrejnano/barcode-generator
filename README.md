# Barcode Generator

Bulk generate QR codes and EAN-13 barcodes from a CSV. Runs entirely in the browser — no backend, no data uploaded.

**[Live](https://barcode-generator-nine-iota.vercel.app)**

## What it does

Paste a product list (or upload a CSV), get a ZIP with all your barcodes — SVG and PNG.

| Column | Required | Description |
|--------|----------|-------------|
| `product_name` | Yes | Used as the file name |
| `qr_data` | No | URL or text to encode as QR |
| `ean13` | No | 12 or 13-digit EAN (check digit auto-calculated) |

## Features

- **SVG + PNG output** — vector for print, raster for everything else
- **EAN-13 check digit** — enter 12 digits, the 13th is calculated; enter 13, it's validated
- **Product ID extraction** — parses IDs from URLs and prefixes filenames for easy searching
- **Grouped or flat ZIP** — one folder per product, or all files together
- **Configurable** — QR size, error correction, barcode size, number visibility

## Run locally

```
npx serve .
```

No install, no build step. Single `index.html`.

## Deploy

Connected to Vercel — push to `main` to deploy. Or manually:

```
vercel --prod
```
