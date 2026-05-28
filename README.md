# XC Tracker

A single-page, static cross-country runner-tracking and progression-analysis tool. Designed for a high school XC coach managing 20–50 athletes. No backend, no database — all data lives in the browser's `localStorage`, with one-click JSON export/import for backup and device transfer.

Built to be deployed free on **GitHub Pages**.

## Features at a glance

- **Roster management** with Boys / Girls / All tabs
- **Run logging** with smart defaults (under 15 seconds per entry)
- **Race logging** with 5K-equivalent normalization (Riegel formula)
- **Intake form + auto-generated starting prescription** (Jack Daniels VDOT, 10% rule, 50% post-injury, conservative new-runner volumes)
- **Charts**: weekly mileage + ACWR overlay, effort distribution vs. 80/20, pace trends by workout type, cumulative season mileage with prior-year overlay, race progression scatter
- **Coaching / Data mode toggle** — recommendation cards and colored zones in Coaching mode, bare charts in Data mode
- **Strong backup nudge** — modal at 7+ days or 20+ unsynced entries since last export
- **Units toggle** — Miles (default) or Kilometers

## Files

- `index.html` — the entire app (HTML + CSS + vanilla JS in one file). Chart.js loads from CDN.
- `README.md` — this file.

That's it. No build step. No dependencies to install.

---

## Deploy to GitHub Pages

### 1. Create a new GitHub repository

1. Go to https://github.com/new
2. Name it whatever you like — e.g. `xc-tracker`.
3. Set it to **Public** (GitHub Pages is free on public repos; private repos require a paid plan).
4. **Do not** initialize with a README, .gitignore, or license — keep it empty so the push below is clean.
5. Click **Create repository**.

### 2. Push these files to the repo

From the folder that contains `index.html` and `README.md`, in a terminal:

```bash
git init
git add index.html README.md
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/xc-tracker.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your actual GitHub username and `xc-tracker` with whatever you named the repo.

### 3. Enable GitHub Pages

1. In your repo on github.com, click **Settings** (top tab).
2. In the left sidebar, click **Pages**.
3. Under **Source**, pick **Deploy from a branch**.
4. Set **Branch** to `main` and the folder to `/ (root)`.
5. Click **Save**.

GitHub will build the site within a minute or two.

### 4. Visit your live site

Your URL will be:

```
https://YOUR-USERNAME.github.io/xc-tracker/
```

Bookmark it on your phone and on your laptop. Same code, separate localStorage per device — use the Export / Import buttons in Settings to keep them in sync.

---

## First-time setup checklist

1. Open the live site in your browser.
2. Click **Add Runner** and add your first athlete. The intake form will generate a conservative starting prescription based on their background.
3. Repeat for the rest of the team.
4. From **Log a Run**, start logging daily runs. Defaults pre-fill from your last entry to keep entry under 15 seconds.
5. Go to **Settings** and export a JSON backup. **Do this regularly** — the app will remind you after 7 days or 20 new entries.

## Backing up and moving between devices

- **Export**: Settings → "Export to JSON" downloads `xc-tracker-backup-YYYY-MM-DD.json`. Save it to your cloud drive (iCloud, Google Drive, Dropbox) or email it to yourself.
- **Import**: Settings → "Import from JSON…" lets you upload a previous backup. This **replaces** all current data, so use it for restore or to set up a new device.
- The backup pill in the top-right shows the days since your last export and turns yellow at 7+ days, red at 30+.

## How the analytics work

- **ACWR (Acute:Chronic Workload Ratio)** — the ratio of last 7 days' mileage to the average weekly mileage over the last 28 days. Coaching-mode zones: green 0.8–1.3, yellow 1.3–1.5, red >1.5 or <0.8.
- **80/20 effort rule** — Easy runs (easy + long workout types) should be ≥80% of weekly volume. The dashed line on the effort distribution chart shows the target.
- **Jack Daniels VDOT** — easy pace ranges are computed from VDOT (65–74% intensity band) using a recent race time. If no recent race is on file, the app falls back to "conversational pace" guidance.
- **Riegel race equivalency** — race times are normalized to a 5K equivalent (T₂ = T₁ × (D₂/D₁)^1.06) so you can compare a 2-mile and an 8K side by side.

## Update or modify the app later

Edit `index.html` locally, then:

```bash
git add index.html
git commit -m "Tweak <thing>"
git push
```

GitHub Pages will redeploy automatically within a minute.

## Troubleshooting

- **Site shows a 404 right after enabling Pages** — wait 1–2 minutes and refresh; the first build takes a moment.
- **Charts don't render** — check your browser console; the app loads Chart.js from `cdn.jsdelivr.net`. If your network blocks the CDN, charts won't draw but everything else still works.
- **Data disappeared** — localStorage was cleared (browser settings, "Clear cookies", different browser/profile, private window). Restore from your most recent JSON export via Settings → Import.
- **Want to start fresh** — Settings → Danger zone → "Wipe all data".
