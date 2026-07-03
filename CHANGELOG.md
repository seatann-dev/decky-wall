# Changelog

## v3.0.0 — Per-game wallpapers (2026-07-03) 🎮
The big one: **a different wallpaper behind each game.**
- **Per-game library** — in the gallery, add several of your own wallpapers (video *or* web) to a library, then assign any of them to individual games right from the Quick Access Menu. Scroll Home and the background swaps to each game's wallpaper; unassigned games show your Default; **Off** shows the game's own art.
- **Loaded from the plugin folder** — library wallpapers live as files in `dist/wp/` and are served locally (no re-baking your big default when you add one). Video and web both supported.
- **Accurate focus detection** — the plugin reads the *actually-focused* game capsule instead of the lagging background image, so the right wallpaper shows with no off-by-one flicker.
- Settings and saved tweaks are preserved.

## v2.4.2 — Deck bug fixes (2026-07-02)
Fixes from Steam Deck tester reports 🙏
- **Wallpaper no longer covers the Quick Access Menu / whole screen at boot** — the wallpaper layer's z-index was lowered so it stays *behind* the UI instead of painting over it.
- **Flicker when hovering between games significantly reduced** — the hero/game art is now hidden with a persistent CSS rule that survives Steam's re-renders (instead of an inline style Steam kept overwriting), plus a faster re-mount.
- No settings reset.

## v2.4.1 (2026-07-02)
- **"Reset position"** button in the video controls (zoom → 100, X/Y → 0).
- **Streaming bake** in the selector — large video wallpapers install without crashing the browser (the file is streamed to disk in chunks instead of built as one giant string). Confirmed working with a 289 MB video on a ROG Ally X.

## v2.4.0 (2026-07-01)
- Video controls added: **Zoom** and **Position X/Y** (alongside Fit / Dim / Brightness).
- Quick Access panel: "Active wallpaper", Enabled, Reload wallpaper, Pause while playing.

## v2.0 – v2.3.x
- Unified **video + web** Wallpaper Engine baking into one frontend-only plugin (no Python backend; everything lives in `dist/index.js`).
- Resilient mount that survives Steam's UI re-renders; **pauses when a game is running**; FPS-capped for battery.
- Desktop selector to pick and bake a wallpaper you already own.

> Scene (`.pkg`) wallpapers are not supported — they need Wallpaper Engine's own renderer. Video and web only.
