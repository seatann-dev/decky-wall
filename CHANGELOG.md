# Changelog

## v3.0.3 — Reset per-game assignments (2026-07-04)
- **New "Reset per-game assignments" button** in the plugin's Quick Access Menu — clears all your per-game wallpaper choices in one tap for a clean slate (handy if any got stuck from earlier versions). Re-bake to get the button.

> **Known limitation:** the **Wallpaper Engine app's own capsule** on Home won't show a wallpaper — it's an app, not a game, so it doesn't expose the standard background layer the plugin mounts onto. Every actual game works.

## v3.0.2 — Silent wallpapers (2026-07-04)
Bug-fix release (selector-only — re-bake to apply). No changes to core features.
- **Wallpapers are now completely silent.** Video wallpapers were already muted; web wallpapers could play their own audio behind the Home screen. Every web wallpaper is now muted at bake time — HTML5 `<audio>`/`<video>`, `new Audio()`, and the Web Audio API are all silenced. A wallpaper never makes a sound.
- Added a build-time guard so a web wallpaper cannot be baked without the audio mute in place.

## v3.0.1 — Per-game library reliability (2026-07-03)
Bug-fix release. The plugin itself is unchanged; all fixes are in the desktop selector (rebake to apply).
- **Fixed a crash when building a per-game library** — the selector wrote the library list using character positions but cut the file by byte positions, so a non-ASCII character earlier in the file corrupted `dist/index.js` and Decky failed to load (`SyntaxError: Unexpected token`). Now byte-accurate.
- **Baking a Default wallpaper no longer wipes your library** — Default bakes now preserve the current per-game library instead of resetting it.
- **Hardened web-wallpaper inlining** — inlined scripts containing `</script>` can no longer break the page.
- **Safety guardrail** — the selector now syntax-checks every bake before writing; a bad bake fails on the desktop with a clear message instead of shipping a broken plugin to your device.
- The desktop selector is now named **`live-wallpaper-selector.html`**.

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
- **Streaming bake** in the selector — 