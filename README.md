# MineWatch — ThingSpeak Mine Subsidence Monitor

A static, mobile-friendly dashboard for viewing **public** ThingSpeak channel metadata and feeds. It can be hosted on GitHub Pages, Netlify, or another static HTTPS host. It uses no backend and requires no API keys.

## Features

- Login-style entry page with an operator display name and a ThingSpeak channel ID or public channel name.
- Reads public channel metadata and up to 800 recent feed entries directly from the ThingSpeak public API.
- Shows all configured channel fields (up to eight), latest values, gauge-style meters, a recent-feed table, and historical charts.
- Automatic refresh with a selectable interval, manual refresh, and browser-local threshold examples.
- Site-location panel using channel coordinates when supplied; opens OpenStreetMap.
- Printable dashboard report, which can be saved as PDF from the browser print dialog.
- Three admin pages: Admin dashboard, Channel management, and System settings.
- PWA manifest, install prompt where supported, and a small offline shell cache. Live ThingSpeak data still requires an internet connection.
- Responsive layout for phones, tablets, and desktops.

## Run locally

The files are self-contained, with Chart.js loaded from jsDelivr and Google Fonts loaded from Google Fonts. You can open `index.html` directly for basic use; for service-worker installation behavior, serve the folder over localhost. For example, use the VS Code Live Server extension or Python's built-in HTTP server.

## Deploy to GitHub Pages

1. Create a GitHub repository and add the contents of this folder to its root (including `index.html`).
2. In the repository, open **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select the default branch and `/ (root)`, then save.
4. Wait for GitHub Pages to publish, then open the provided HTTPS URL. A static host is required for PWA installation and service-worker caching.

## Deploy to Netlify

Drag this project folder into Netlify Drop, or connect the GitHub repository. No build command or publish directory is required when the files are in the repository root.

## Connect a channel

Enter the numeric ThingSpeak channel ID or its public channel name on the login screen, then select **Open monitoring console**. To change the channel later, use the channel input on Overview or **Administration → Channel management**. The channel must be publicly readable without a read API key. Names containing unsupported characters may not be resolvable by ThingSpeak's public API; a numeric channel ID is the most reliable option.

The application requests channel metadata from `https://api.thingspeak.com/channels/{channel}.json` and public feeds from `https://api.thingspeak.com/channels/{channel}/feeds.json?results=800`. It never sends a write key or writes to a channel. Do not put private read/write keys in static frontend code.

## Login and settings limitations

The login screen only stores the display name in page memory and creates no protected account or session. Anyone can inspect or modify static frontend code, so this is **not secure authentication** and must not be used to protect private monitoring data or administrative actions. Thresholds and refresh preferences are saved in the current browser's local storage; they are not shared with other users.

## Safety and interpretation

The dashboard presents values published by a channel; it does not validate sensor calibration, units, sampling, placement, data integrity, or site context. Threshold coloring is a user-configured visual aid only. **A public-channel reading cannot, by itself, guarantee that a mine or ground area is safe or dangerous.** Establish limits with qualified site engineers using calibrated equipment and an approved monitoring and emergency-response plan. Never rely on this demo as a safety system.

## Files

- `index.html` — app pages and controls
- `styles.css` — responsive dashboard and print layout
- `app.js` — ThingSpeak reads, rendering, charts, refresh, thresholds, navigation, and report action
- `manifest.webmanifest`, `sw.js`, `assets/icon.svg` — install/offline shell support

## Third-party assets

Chart.js is loaded from jsDelivr and fonts from Google Fonts. For fully self-hosted deployments, download and serve those assets locally in accordance with their license terms.
