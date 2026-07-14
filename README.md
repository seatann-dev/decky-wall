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
  <img alt="deck" src="https://img.shields.io/badge/Steam%20Deck%20OLED-confirmed%20working-brightgreen">
</p>

<p align="center">
  <img alt="video wallpapers" src="https://img.shields.io/badge/video%20wallpapers-supported-brightgreen">
  <img alt="web wallpapers" src="https://img.shields.io/badge/web%20wallpapers-partial-yellow">
  <img alt="scene wallpapers" src="https://img.shields.io/badge/scene%20wallpapers-not%20supported-red">
</p>

---

## Demo

![Decky.wall demo — live wallpapers behind Game Mode Home](./Decky.wall_demo.gif)

## What it is

Every "live wallpaper on Steam Deck" answer out there is **desktop mode**. Decky.wall puts a live **Wallpaper Engine** wallpaper behind the **Game Mode** Home screen — the real gamepad-UI background you see behind your game capsules, not the KDE desktop. You pick a wallpaper **you already own**, it bakes into the plugin, and it plays behind your games.

**Video wallpapers work reliably. Web wallpapers are experimental** (many work, some don't yet). **Scene wallpapers aren't supported** — only Video and Web can be baked, and the picker will tell you if it skips any Scene ones. It ships no wallpaper files of its own — it only bakes wallpapers from *your own* Workshop folder, on your own device. Open source (MIT).

> **Heads up:** built and tested on a **ROG Xbox Ally X (Bazzite)** — the same Game Mode stack (gamescope + gamepad UI + Decky) as a Steam Deck. I don't own a Steam Deck myself, but a user has **confirmed it working on a Steam Deck OLED** — more testers still welcome (see [Testing](#testing-help-wanted)).

### How this differs from the KDE Wallpaper Engine plugin

[`catsout/wallpaper-engine-kde-plugin`](https://github.com/catsout/wallpaper-engine-kde-plugin) does the **KDE desktop**; Decky.wall does **Steam Game Mode** (behind your game capsules). Use the KDE plugin for your desktop, this for Game Mode — they coexist.

## ⚠️ Before you start — please read

- **This only works in Steam _Game Mode_ on Bazzite or SteamOS** (a Steam Deck, or a handheld like the ROG Ally running **Bazzite**). Decky plugins run on the Linux / Game-Mode side, so **it does _not_ run on Windows.** If you dual-boot, do everything below on the **Bazzite** side.
- You need **[Decky Loader](https://github.com/SteamDeckHomebrew/decky-loader)** installed. This is a plugin *for* Decky.
- You need **Wallpaper Engine** installed (from Steam) with the wallpapers you own already downloaded.
- The desktop tool needs a **Chromium browser — Chrome, Edge, Brave, or Vivaldi. Firefox will _not_ work** (no File System Access API).
- **Use only wallpapers you own.** This plugin ships no wallpaper files — it just bakes your own.

## Install & first wallpaper (step by step)

> 📄 Latest version: **v3.1.0** — web wallpapers now **serve their whole folder locally** and mount the real files, so complex ones that used to show black now render (inline is kept as an automatic fallback). New **Video / Web / Scene tabs** in the picker, and **Web options** (fake audio, fake mouse, and a music track that plays behind Home and drives visualizers). Re-bake your web wallpaper to switch it over — no settings reset. See the [changelog](./CHANGELOG.md).

> 📺 **Prefer to watch?** A community walkthrough by **NotAGameAddict** covers the whole setup on a Steam Deck OLED: [How to Use Wallpaper Engine wallpapers in Gaming Mode](https://youtu.be/ToB_G86eptU). *(Not made by me — external video, so it may change over time.)*

### 1 · One-time setup
1. Install **Decky Loader** if you don't have it ([install guide](https://github.com/SteamDeckHomebrew/decky-loader#installation)).
2. Turn on **Developer mode** in Decky: in **Game Mode**, press the **⋯ Quick Access** button → the **plug icon (Decky)** → **⚙ Settings** → **General** → toggle **Developer mode ON**. *(This unlocks "Install from ZIP".)*
3. Install **Wallpaper Engine** from Steam and let it finish downloading the wallpapers you subscribed to.

### 2 · Download the two files
From the **[latest release](../../releases/latest)**, download:
- **`Live-Wallpaper-vX.Y.Z.zip`** — the plugin.
- **`video-wallpaper-selector.html`** — the desktop tool you bake wallpapers with.

Save both somewhere easy to find (Desktop or Downloads).

### 3 · Install the plugin (in Game Mode)
1. Press **⋯ Quick Access** → **Decky (plug icon)** → **⚙ Settings** → **Developer** tab → **Install Plugin from ZIP File**.
2. Pick `Live-Wallpaper-vX.Y.Z.zip`. **"Live Wallpaper"** should now show up in your Decky plugin list.

> ⚠️ Install from the **ZIP** — don't just copy the folder into `~/homebrew/plugins/`. A plain copy often won't load.

### 4 · Bake your first wallpaper (in Desktop mode)
1. Switch to **Desktop mode** (**Steam button → Power → Switch to Desktop**).
2. Open **`video-wallpaper-selector.html`** in **Chrome / Edge / Brave** (not Firefox).
3. The first time, it asks for **two folders** — click each and grant access:
   - **Wallpaper Engine Workshop folder** — usually `~/.local/share/Steam/steamapps/workshop/content/431960` *(read)*.
   - **Your plugin folder** — `~/homebrew/plugins/Live Wallpaper` *(read/write)*.

   It remembers both, so you only do this once.
4. Pick a wallpaper → click **Use this**. Big videos show a **%** while they bake.

### 5 · See it
1. Switch back to **Game Mode** — returning reloads the plugin, and your wallpaper plays behind the Home screen.
2. Nothing showing? Open **⋯ → Decky → Live Wallpaper → Reload wallpaper**.

**That's it.** To change your wallpaper later, go back to Desktop mode and repeat **step 4**.

## Everyday use

![How to use Decky.wall](./Decky.wall_howto.png)

- **Change your wallpaper:** go to Desktop mode, open the selector, pick a new one → **Use this**, then return to Game Mode. (Same as install step 4.)
- **Tweak the look without re-baking:** open the **Live Wallpaper** plugin in the Quick Access Menu — Fit, Dim, Brightness, Zoom, Position X/Y, and **Reset position** for video.
- **Turn it off / on:** the **Enabled** toggle in the same menu. (Turning it off instantly removes the wallpaper — handy if anything ever looks off.)
- **Hide the status pill:** the **Status pill** toggle in the same menu turns off the small on-screen readout.

### Per-game wallpapers

![Per-game wallpapers — a different wallpaper behind each game](./Decky.wall_pergame_demo.gif)

Want a different wallpaper behind each game?

1. In the gallery, click **＋ Library** on the wallpapers you want to use (video or web). They copy into the plugin and show up in a **Per-game library** list.
2. Back in **Gaming Mode**, hover a game → open **Live Wallpaper** in the Quick Access Menu → use the **"Wallpaper for this game"** dropdown to pick **Default**, one of your library wallpapers, or **Off** (show the game's own art).
3. Scroll Home — the background swaps to each game's assigned wallpaper. Everything else stays on your Default.

Both your Default and your library wallpapers are stored as files inside the plugin folder (`dist/wp/`) and streamed locally — so they start quickly (even large videos), and adding a library wallpaper never re-bakes your Default.

**Assignments getting stuck?** Open **Live Wallpaper** in the Quick Access Menu and tap **Reset per-game assignments** to clear them all and start clean.

## Good to know

- **The Wallpaper Engine app's own capsule won't show a wallpaper.** Wallpaper Engine is an *app*, not a game, so its Home tile doesn't have the standard background layer the plugin mounts wallpapers onto — so it stays on its own art no matter what you assign. This only affects that one tile; every actual game works normally.

## Known issue — Decky disappearing after re-baking several times

If you switch between **Desktop and Game Mode many times in one session** (for example, re-baking a few different wallpapers back-to-back), the **Decky plug icon can vanish** from the Quick Access Menu.

**This isn't the plugin.** It's a [known Decky Loader bug](https://github.com/SteamDeckHomebrew/decky-loader/issues/799) with reloading plugins on Desktop↔Game-Mode switches — it happens with *any* plugin, and it still happens even with this wallpaper turned off. I chased it hard: even a build that paints nothing at all triggers it, so it's Decky's reload, not the wallpaper.

**Normal use isn't affected** — installing once and baking a single wallpaper works every time. It only shows up under rapid re-baking.

**To recover if it happens:** restart Steam (Steam → Power → Restart), or from Desktop run `sudo systemctl restart plugin_loader`. To change wallpapers several times in a row, restart Steam between bakes.

## Testing (help wanted)

I only have a **ROG Xbox Ally X on Bazzite** to test on. It's been **confirmed working on a Steam Deck OLED** by a user (thank you!) — but the more real-hardware reports, the better. If you run a **Steam Deck** or another handheld on Bazzite/SteamOS, I'd love to hear how it went: what worked, what didn't, and anything that looked off. Open an issue; even a quick "works on mine" helps.
