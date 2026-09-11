# Flames Music Download 🔥

*Published by S.S. Khoza*

A website (and future app) for streaming and downloading **royalty-free / Creative Commons** music — usable online and offline.

Music is sourced legitimately from the **Jamendo API**, a catalog of tracks that artists have explicitly released under open licenses. No copyrighted/mainstream content is scraped or ripped.

## How it works

- **Backend**: Node.js + Express. Proxies search/download requests to Jamendo so your API key never sits in the browser.
- **Frontend**: Plain HTML/CSS/JS (no build step needed). Works as a normal website and as an installable PWA.
- **Offline downloads**: When a user clicks "Download," the audio file is saved into the browser's IndexedDB as a blob (and also triggers a normal file download to their device). Saved tracks appear under "My Downloads" and play even with no internet connection.
- **Online streaming**: Search results stream directly from Jamendo without needing to download first.

## Setup

### 1. Get a free Jamendo API key
Sign up at https://devportal.jamendo.com/ and create an app to get a `client_id`. It's free for personal/development use — check their commercial licensing terms before you launch this as a paid product.

### 2. Configure the backend
```bash
cd backend
cp .env.example .env
# open .env and paste your JAMENDO_CLIENT_ID
npm install
npm start
```

The server runs on `http://localhost:4000` by default, and also serves the frontend from the same address — so you only need to run one process.

### 3. Open the site
Visit `http://localhost:4000` in your browser. Search for a genre or artist, stream tracks, or hit Download to save them for offline listening.

## Project structure
```
flames-music-download/
├── backend/
│   ├── server.js        # Express API (search, track detail, download proxy)
│   ├── package.json
│   └── .env.example
└── frontend/
    ├── index.html
    ├── style.css
    ├── app.js            # search, playback, IndexedDB offline storage
    ├── sw.js              # service worker (caches the app shell)
    └── manifest.json      # PWA manifest
```

## Turning this into a mobile app later
Since this is plain HTML/CSS/JS hitting a REST API, you have two low-effort paths to a mobile app without rewriting the backend:
1. **PWA install** — users can "Add to Home Screen" from their mobile browser right now; it already behaves like an app.
2. **React Native / Capacitor wrapper** — wrap this same API with a native shell later if you want App Store / Play Store presence.

## Before treating this as a real business
- Read Jamendo's (or whichever source's) commercial licensing terms — free tiers are often personal-use only.
- Decide your monetization model (free + ads, freemium downloads, subscription) before scaling.
- Consider artist attribution requirements — most CC licenses require crediting the artist, which this app already surfaces via `licenseUrl`.
