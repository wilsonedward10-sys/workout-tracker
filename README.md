# Workout Tracker

A personal workout-tracking web app (PWA) for strength training and cardio, hosted on GitHub Pages and installable on iPhone, iPad, and Mac.

**App URL:** https://wilsonedward10-sys.github.io/workout-tracker/

## Features

- **Strength logging** — exercise name (with autocomplete), any number of sets, reps and weight (lbs) per set
- **Cardio logging** — exercise name, duration in minutes, optional machine setting number
- **Workout templates** — save a routine ("Leg Day") and start future sessions pre-filled
- **Personal records** — automatic PR detection with a 🏆 toast when you beat a record, plus a PR list per exercise
- **Progress charts** — per-exercise trend charts and weekly/monthly stats
- **History** — full log of past workouts with edit and delete
- **Export** — CSV (opens in Google Sheets / Numbers / Excel) and JSON backup/restore
- **Cross-device sync** — history is stored in the private [`workout-data`](https://github.com/wilsonedward10-sys/workout-data) repo; every device reads and writes the same file
- **Offline-capable** — works without a signal in the gym; syncs when back online

## Install on your devices

- **iPhone / iPad:** open the app URL in Safari → Share button → **Add to Home Screen**
- **Mac:** open the app URL in Safari → **File → Add to Dock** (or in Chrome: install icon in the address bar)

## Set up sync (one time)

1. Create a fine-grained personal access token at github.com → Settings → Developer settings → Fine-grained tokens
   - Repository access: **Only select repositories → workout-data**
   - Permissions → Repository permissions → **Contents: Read and write**
2. In the app, go to **Settings**, paste the token, and tap **Save & Sync Now**
3. Repeat the paste on each device (the token is stored only in that device's browser storage)

## Architecture

- `index.html` — the entire app (vanilla JS, no build step)
- `sw.js` — service worker for offline caching
- `manifest.webmanifest` + icons — PWA install metadata
- Data lives in `data/workouts.json` in the **private** `workout-data` repo, synced via the GitHub Contents API with last-write-wins merging per workout and tombstones for deletions
