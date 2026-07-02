<p align="center">
  <img src="./Decky.wall_icon-256.png" alt="Decky.wall" width="120">
</p>

<h1 align="center">Decky.wall</h1>

<p align="center">
  Run your own <b>Wallpaper Engine</b> wallpapers behind the Steam <b>Game Mode</b> Home screen.<br>
  A frontend-only <a href="https://github.com/SteamDeckHomebrew/decky-loader">Decky Loader</a> plugin.
</p>

<p align="center">
  <img alt="license" src="https://img.shields.io/badge/license-MIT-blue">
  <img alt="status" src="https://img.shields.io/badge/works%20on-ROG%20Ally%20X%20(Bazzite)-brightgreen">
  <img alt="deck" src="https://img.shields.io/badge/Steam%20Deck-untested%2C%20testers%20wanted-orange">
</p>

---

> **Heads up:** I built and tested this on a **ROG Xbox Ally X running Bazzite**, where Game Mode is the same gamescope + gamepad-UI + Decky stack as a Steam Deck. It works well there. I do **not** own a Steam Deck, so I can't verify real Deck hardware — testers very welcome (see [Testing](#testing-help-wanted)).

## What it is

Every "live wallpaper on Steam Deck" answer out there is **desktop mode**. Decky.wall puts a live wallpaper behind the **Game Mode** Home screen — the actual gamepad-UI background you see behind your game capsules — not the KDE desktop.

You pick a Wallpaper Engine wallpaper **you already own** in a small desktop tool, it bakes the wallpaper into the plugin, and it plays behind Home. Video wallpapers and many interactive web wallpapers both work.

**It ships no wallpaper files.** The plugin only bakes wallpapers from *your own* Wallpaper Engine Workshop folder, on your own device. Nothing is redistributed.

## Demo

<!-- TODO: drop a short screen recording / GIF here -->
`(video coming — a clip of it running behind Home + swapping wallpapers in the selector)`

## Features

- 🎬 **Video wallpapers** — played full-screen behind Home.
- 🌐 **Interactive web wallpapers** — wrapped in a self-contained frame with a small shim so their runtime assets and properties still load. (Got NIKKE's web wallpaper running this way.)
- 🧩 **Frontend-only** — no Python backend; everything lives in `dist/index.js`. Survives copy-only installs where the backend never runs.
- 🪫 **Battery-aware** — FPS-capped, and **pauses when a game is running**.
- 🎛️ **In-game controls** (Quick Access Menu) — Enable, Reload wallpaper, and for video: Fit, Dim, Brightness, Zoom, Position X/Y, and Reset position.
- 📦 **Streaming bake** — big video wallpapers install without crashing the browser; a 289 MB wallpaper installs and plays on my Ally X.

> ⚠️ **Scene** (`.pkg`) wallpapers are **not** supported — they're a proprietary format. Video and web only.

## How it works (short version)

Decky plugins run in Steam's shared JS context, which is **not** the visible Home window. Decky.wall enumerates the Steam documents, finds the real Home window and its full-screen background layer, and mounts an opaque video/iframe over it — then animates off *that* window's own `requestAnimationFrame`. Steam's UI re-renders and strips injected DOM, so the mount re-asserts itself (interval + MutationObserver) to stay put while you scroll between games.

The wallpaper is embedded directly into `dist/index.js` (base64 for video, self-contained HTML for web). The desktop **selector** does the baking; for large videos it **streams** the file to disk in chunks instead of building one giant string in memory (which is what used to fail).

## Requirements

- A handheld/PC in **Steam Game Mode** with **Decky Loader** installed (Steam Deck, or Bazzite on other handhelds/PCs).
- **Wallpaper Engine** (owned, on Steam) if you want to use WE wallpapers — the selector reads your Workshop folder.
- A **Chromium-based browser** (Chrome/Edge) on the desktop side to run the selector. *Firefox is not supported* — the selector uses the File System Access API, which Firefox lacks.

## Install

1. Download the latest `Live-Wallpaper-vX.Y.Z.zip` from [Releases](../../releases).
2. On the device, open **Decky → ⚙ (settings) → Developer → enable Developer mode**.
3. In the Developer tab, choose **Install Plugin from ZIP** and pick the zip.
   *(A plain copy of the folder into `~/homebrew/plugins/` will not reliably work — use the ZIP installer.)*
4. Open **Decky.wall** from the Quick Access Menu.

## Usage

1. On the **desktop side** (Bazzite desktop, or any PC with your WE wallpapers), open the **selector** in Chrome/Edge — either the hosted version at **https://seatann-dev.github.io/decky-wall/** or `index.html` from this repo.
2. Point it at your **Wallpaper Engine Workshop folder** and at your installed **Live Wallpaper** plugin folder (it remembers both).
3. Pick a wallpaper → **Use this**. It bakes into the plugin (big videos show a streaming %).
4. **Return to Game Mode.** It reloads the plugin and your wallpaper plays behind Home.
5. Tweak Fit / Dim / Brightness / Zoom / Position from the Quick Access Menu; **Reset position** restores defaults.

## Testing (help wanted)

I can't test real Steam Deck hardware. If you have a Deck (LCD or OLED) and are willing to flash a build and report what happens — whether it loads, whether video plays, battery impact, any crashes — that's the single most useful contribution. Open an issue with your hardware + what you saw.

Known unknowns: the exact video-size ceiling on lower-RAM devices (the 289 MB result is Ally X, 24 GB RAM — a Deck has less), older gamescope builds, and SteamOS proper.

## Building from source

The plugin is TypeScript/React built with the Decky toolchain (`@decky/api`, `@decky/ui`, `@decky/rollup`). `pnpm i && pnpm build` produces `dist/index.js`. The selector (`index.html`, also hosted at https://seatann-dev.github.io/decky-wall/) is a single self-contained file — no build step.

## Credits

- Built on [Decky Loader](https://github.com/SteamDeckHomebrew/decky-loader) and the Decky plugin toolchain.
- Wallpaper Engine and its wallpapers belong to their respective creators — this project bundles none of them.
- By [seatann-dev](https://github.com/seatann-dev). I'm a hobbyist and a beginner; PRs, corrections, and smarter approaches are all welcome.

## License

[MIT](./LICENSE) © 2026 seatann-dev
