# AGENTS.md — Absensi Siswa MDTM

## Overview
Single-file static HTML app (Indonesian student attendance tracker). No backend, no build step — all data lives in `localStorage`. Uses jsPDF + autotable (CDN) for PDF export and WhatsApp sharing.

## Running the app
```
docker compose -f docker-compose.base44.yml up -d
```
Serves via Vite dev server (live reload) on host port 3000 → container 5173.

## Key facts
- **Entry point**: `index.html` at repo root (Vite serves it directly).
- **No logic changes**: The app's JavaScript (student CRUD, attendance, rekap, PDF, WhatsApp) is untouched from the original. Only CSS responsiveness and a safe-storage wrapper were added.
- **Safe storage**: `_ls` shim at top of `<script>` falls back to in-memory storage when `localStorage` is blocked (sandboxed iframes). Real browsers use native `localStorage` unchanged.
- **Init order**: `let absensi` must be declared before the `if (!siswa)` block because `save()` (hoisted) references `absensi` during first-run seeding.
- `faktur_rs_padi (2).html` is an unrelated legacy file; `index.html` is the served app.

## Responsive design
- Tables wrapped in `.table-wrap` (horizontal scroll on small screens).
- All inputs/selects use `font-size: 16px` (prevents iOS zoom) and `min-height: 46px`.
- Nav buttons `min-height: 52px` (56px on mobile) for easy tapping.
- Status buttons 44px (48px on mobile). Edit/delete buttons enlarged on mobile.
- `clamp()` for header/nav font sizes. Stat grid: 2 cols mobile, 4 cols desktop.
