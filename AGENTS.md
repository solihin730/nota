# AGENTS.md — Base44 Dev Environment

## Project Overview
Single-file static HTML app: an Indonesian invoice/faktur generator for "RS. PADI" (a rice merchant). No build step, no backend, no dependencies — just one self-contained HTML file with inline CSS/JS. Uses CDN resources (Google Fonts, jsPDF, html2canvas) at runtime.

## Running the App
```bash
docker compose -f docker-compose.base44.yml up -d
```
- Served on **port 3000** via `nginx:alpine`.
- The source file is `faktur_rs_padi (2).html` (note: spaces and parentheses in filename). The compose startup command copies it to `index.html` and fixes directory permissions so the nginx worker can read it.
- No live-reload server needed — nginx serves static files directly. After editing the HTML, refresh the preview (or call `reload_preview`).

## No Secrets Required
This app has no backend, no database, and no external service credentials. Everything runs client-side in the browser.

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` should return `200`.
- The page title is "Faktur Penjualan - RS. PADI".
