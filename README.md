# Forge

Personal records, properly tracked. A self-contained workout-tracker PWA.

## Files

- `index.html` — the entire app (all CSS + JS inline)
- `manifest.json` — PWA manifest
- `sw.js` — service worker (offline caching)
- `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` — app icons

## Running it

The service worker requires a real HTTP origin — opening `index.html` directly
from the file system (`file://`) won't register it, and Chrome won't show the
"Add to Home Screen" install prompt.

### Easiest: GitHub Pages (free, takes 2 minutes)

1. Create a new GitHub repo, drop these files in.
2. Settings → Pages → deploy from the `main` branch root.
3. Open the URL on your Android phone in Chrome.
4. Chrome menu (⋮) → "Add to Home screen" → "Install".
5. Open the new home screen icon. It launches as a standalone app.

Other free hosts that work the same way: Netlify Drop, Cloudflare Pages,
Vercel.

### For local testing on your phone

If your phone and computer are on the same Wi-Fi:

```
cd forge
python3 -m http.server 8000
```

Then on your phone, visit `http://<your-laptop-ip>:8000`. Note: Chrome may
require HTTPS to show the full install prompt — local-network HTTP works for
"Add to home screen" but not the proper install banner. GitHub Pages is
easier.

## Offline

After the first load on a real network, the service worker caches everything
including the Chart.js CDN script and Google Fonts. Reopen the app
airplane-mode and it still works fully — including charts.

## Backup

Stats tab → Export data (JSON). Import the same file on a new device or after
clearing browser data. Worth doing every couple of weeks.

## Design notes

- 1RM uses the Epley formula (`weight × (1 + reps / 30)`) so 100×8 beats 100×7.
- Weeks start on Monday for streak tracking.
- Default weekly target is 3 sessions.
- A "rest day" warning shows on History if no session has been logged in 5+
  days.
- Exercise names are case-insensitive for grouping but display as you typed
  them most recently.
