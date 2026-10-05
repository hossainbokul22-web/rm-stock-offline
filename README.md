# RM Stock Management — Full Offline PWA

Personal offline Raw Material (RM) Stock Management app with **Voucher AI Agent** (English + বাংলা OCR).

Completely offline after install. Data stays inside the app (localStorage / WebView storage). Existing business logic is unchanged.

## Features

- **RM Daily Entry** (Store Receive) with correction & admin edit
- **Input Batch** (3-shift support)
- **Mixing-2** consumption reports
- **Opening Balance**, Monthly reports, Final Monthly Usage
- **Admin Panel** — master data, approvals, custom sheets
- **Offline Voucher AI Agent**
  - Camera → Capture voucher/challan
  - Local OCR (English + Bengali)
  - Auto-detect Date, RM Item, Qty, Note
  - Admin review/edit → Approve → add to Daily Entry
- Full offline: Tesseract.js + models bundled in `lib/tesseract/`
- Backup / Restore (JSON) + CSV export

## Quick Start

### Option 1 — Local test
```bash
# Open index.html in a browser (Chrome recommended)
# Camera & Service Worker work best on HTTPS or localhost
```

### Option 2 — Install as PWA (recommended)
1. Host the folder on any HTTPS site (GitHub Pages, Netlify, Vercel, your server).
2. Open in Chrome → **Install** / Add to Home Screen.
3. Open once so Service Worker caches everything (including OCR models).
4. After that the app works **fully offline**.

### Option 3 — Android APK
Use [WebIntoApp](https://www.webintoapp.com/) or similar tool pointing to your hosted URL (or local files). The APK keeps data in the app’s private WebView storage — like a normal Play Store app.

## Data Storage (App-like)

All data is stored in the **installed app’s localStorage**:
- Receives, batches, masters, corrections, audits, custom sheets
- Survives browser restarts
- Not shared with other websites
- Cleared only if the app is uninstalled or its storage is cleared
- Always use the in-app **Backup** before changing devices

## Voucher AI Agent

1. Go to **RM Daily Entry**
2. Tap **📷 Scan Voucher (Offline AI)**
3. Open Camera → point at voucher → **Capture & Detect**
4. Review detected fields (Admin can edit)
5. **Admin only**: Approve → adds to Daily Entry

OCR models are local:
```
lib/tesseract/
  eng.traineddata
  ben.traineddata
  tesseract.min.js
  worker.min.js
  tesseract-core-simd-lstm.wasm.js
  tesseract-core-simd-lstm.wasm
```

## Project Structure

```
rm_stock_app/
├── index.html          # Main app (single-file UI + logic)
├── sw.js               # Service Worker (offline cache)
├── manifest.json       # PWA manifest
├── icon-192.png
├── icon-512.png
├── lib/tesseract/      # Offline OCR engine + eng/ben models
├── README.md
└── .gitignore
```

## GitHub Pages Deploy

1. Push this repo to GitHub.
2. Settings → Pages → Source: Deploy from branch `main` / root (or `/docs`).
3. Wait for the site to build.
4. Open the Pages URL once online → Install as PWA.

## Important Notes

- Login is **local-only** (not secure cloud authentication). Suitable for personal / single-device use.
- No Google Sheets / server backend in this build.
- Core calculation & data relationships were left unchanged when the Voucher AI feature was added.
- Keep regular JSON backups.

## License

Personal / internal use. Modify as needed for your factory/store.
