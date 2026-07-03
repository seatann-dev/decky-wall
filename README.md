<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./Decky.wall_logo_ondark.png">
    <img src="./Decky.wall_logo_onlight.png" alt="Decky.wall" width="120">
  </picture>
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

## Demo

![Decky.wall demo — live wallpapers behind Game Mode Home](./Decky.wall_demo.gif)

## What it is

Every "live wallpaper on Steam Deck" answer out there is **desktop mode**. Decky.wall puts a live **Wallpaper Engine** wallpaper behind the **Game Mode** Home screen — the real gamepad-UI background you see behind your game capsules, not the KDE desktop. You pick a wallpaper **you already own**, it bakes into the plugin, and it plays behind your games.

**Video wallpapers work reliably; web wallpapers are experimental** (many work, some don't yet). **It ships no wallpaper files** — it only bakes wallpapers from *your own* Workshop folder, on your own device. Open source (MIT).

> **Heads up:** built and tested on a **ROG Xbox Ally X (Bazzite)** — the same Game Mode stack (gamescope + gamepad UI + Decky) as a Steam Deck. I do **not** own a Steam Deck, so I can't verify real Deck hardware — testers very welcome (see [Testing](#testing-help-wanted)).

## Install

1. Install **Wallpaper Engine** and let it download all the wallpapers you own.
2. Download **`Live-Wallpaper-vX.Y.Z.zip`** from [Releases](../../releases).
3. Download **`video-wallpaper-gallery.html`** and keep it on your desktop for quick access.
4. Open **Big Picture mode** and install the zip via **Decky → ⚙ Developer → Install Plugin from ZIP**. *(A plain folder copy into `~/homebrew/plugins/` will not reliably work — use the ZIP installer.)*

> 📄 **What's new:** see the [changelog](./CHANGELOG.md). Latest is **v2.4.2** (Steam Deck bug fixes).

## Usage

![How to use Decky.wall](./Decky.wall_howto.png)

1. After the plugin installs, **close Big Picture mode** (go to the desktop).
2. Open **`video-wallpaper-gallery.html`** in **Chrome or Edge** — *Firefox won't work*. **First time:** point it at your Wallpaper Engine Workshop folder and your installed **Live Wallpaper** plugin folder — on Bazzite/SteamOS that's `~/homebrew/plugins/Live Wallpaper` (it remembers both).
3. **Choose the wallpaper** you want → **Use this**. It bakes into the plugin (big videos show a streaming %).
4. **Go back to Gaming Mode** — your wallpaper plays behind Home.
5. If it doesn't show up, open the **Live Wallpaper** plugin in the Quick Access Menu and hit **Reload wallpaper**.
6. To change the wallpaper later: go to the desktop and **repeat from step 2**.

*Tip: tweak Fit / Dim / Brightness / Zoom / Position — and **Reset position** — from the plugin's Quick Access Menu.*

> 💡 **Want the see-through look from the demo?** Steam's Home panels are opaque by default. To let the wallpaper show through the UI like in the clip, also install **[CSS Loader](https://github.com/suchmememanyskill/SDH-CssLoader)** (a Decky plugin).

## Features

- 🎬 **Video wallpapers** — played full-screen behind Home. Works reliably for most videos.
- 🌐 **Interactive web wallpapers (experimental)** — wrapped in a self-contained frame with a small shim so their runtime assets and properties load. **Many work, but not all — support is hit-or-miss right now.** (NIKKE's web wallpaper works.)
- 🧩 **Frontend-only** — no Python backend; everything lives in `dist/index.js`. Survives copy-only installs where the backend never runs.
- 🪫 **Battery-aware** — FPS-capped, and **pauses when a game is running**.
- 🎛️ **In-game controls** (Quick Access Menu) — Enable, Reload wallpaper, and for video: Fit, Dim, Brightness, Zoom, Position X/Y, and Reset position.
- 📦 **Streaming bake** — big video wallpapers install without crashing the browser; a 289 MB wallpaper installs and plays on my Ally X.

> ⚠️ **Scene** (`.pkg`) wallpapers are **not** supported — they're a proprietary format. Video and web only.

## How it works (short version)

Decky plugins run in Steam's shared JS context, which is **not** the visible Home window. Decky.wall enumerates the Steam documents, finds the real Home window and its full-screen background layer, and mounts an opaque video/iframe over it — then animates off *that* window's own `requestAnimationFrame`. Steam's UI re-renders and strips injected DOM, so the mount re-asserts itself (interval + MutationObserver) to stay put while you scroll between games.

The wallpaper is embedded directly into `dist/index.js` (base64 for video, self-contained HTML for web). The desktop **selector** does the baking; for large videos it **streams** the file to disk in chunks instead of building one giant string in memory (which is what used to fail).

## Testing (help wanted)

I can't test real Steam Deck hardware. If you have a Deck (LCD or OLED) and are willing to flash a build and report what happens — whether it loads, whether video plays, battery impact, any crashes — that's the single most useful contribution. Open an issue with your hardware + what you saw.

Known unknowns: the exact video-size ceiling on lower-RAM devices (the 289 MB result is Ally X, 24 GB RAM — a Deck has less), older gamescope builds, and SteamOS proper.

## Building from source

The plugin is TypeScript/React built with the Decky toolchain (`@decky/api`, `@decky/ui`, `@decky/rollup`). `pnpm i && pnpm build` produces `dist/index.js`. The selector (`video-wallpaper-gallery.html`, also hosted at https://seatann-dev.github.io/decky-wall/ as `index.html`) is a single self-contained file — no build step.

## Credits

- Built on [Decky Loader](https://github.com/SteamDeckHomebrew/decky-loader) and the Decky plugin toolchain.
- Wallpaper Engine and its wallpapers belong to their respective creators — this project bundles none of them.
- By [seatann-dev](https://github.com/seatann-dev). I'm a hobbyist and a beginner; PRs, corrections, and smarter approaches are all welcome.

## License

[MIT](./LICENSE) © 2026 seatann-dev
