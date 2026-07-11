# Changelog

## v3.0.8 — Scene wallpapers are flagged, not silently hidden (2026-07-09)
Selector-only — no re-install needed, just re-open the selector.
- **The picker now tells you when it skips Scene wallpapers.** Scene-type wallpapers aren't supported (only Video and Web are), and the picker used to just hide them — so if you downloaded new Scene wallpapers, they'd quietly not show up and it looked like a refresh/cache bug. Now a note at the top of the gallery says how many were hidden and why.
- No plugin change; the `.zip` is v3.0.7 with a version bump.

## v3.0.7 — Large videos load fast now (2026-07-09)
- **Big speed-up for large video wallpapers.** Baked videos used to be embedded whole and had to be fully decoded before anything showed — slow, and large ones could fail to load. Now the selector writes your baked video as a real file and the plugin **streams** it locally (the same way the per-game library already worked), so it starts almost immediately, even for large videos. **Re-bake with the updated selector to get this.**
- Rolls in the v3.0.6 fixes (hero bleed-through + the earlier large-video load failure).
- No settings reset.

## v3.0.6 — Fix: hero bleed-through + faster first load (2026-07-09)
- **Fixed game background art showing through the wallpaper on some games.** Games with custom artwork or non-Steam-game shortcuts can have *two* hero-image layers stacked; the plugin only hid one, so the second painted over your wallpaper. Now every game hero image is disabled while a wallpaper is active — no more bleed-through. Also clears the "Wallpaper Engine capsule shows no wallpaper" case.
- Capsule tiles, icons, and logos are untouched — only the full-screen hero art is hidden, and only while a wallpaper is on.
- **Faster first appearance after a reload.** The baked video is now decoded early at startup and cached, instead of being processed only once the background slot is found — so the wallpaper shows sooner.
- Lighter, too: the hero hide is a single CSS rule instead of a per-frame scan.
- Re-bake to apply (the plugin engine changed). **No settings reset** — saved tweaks and per-game library preserved.

## v3.0.5 — Status pill + Steam-themed selector (2026-07-06)
- **New "Status pill" toggle** in the Quick Access Menu — hide the on-screen status popup entirely. Turning it off removes the pill immediately (the diagnostic box still appears if the wallpaper ever fails to mount, so you can still troubleshoot).
- **Restyled pill** — the status pill is now a small, always-on readout pinned to the **top-left** corner (compact white, square corners) instead of a large centered pill that faded after a few seconds. It stays put so you can glance at the active wallpaper / focus / on–off state anytime.
- **Selector opens in the Steam theme by default** — the desktop gallery/selector now defaults to the Steam-blue look (was light). Cosmetic only; you can still switch to light or dark.
- **The desktop selector is now named `video-wallpaper-selector.html`** (was `live-wallpaper-selector.html`). One consistent name everywhere — same tool.
- Re-bake to apply (the plugin engine changed). **No settings reset** — your saved tweaks and per-game library are preserved.

## v3.0.4 — Smooth per-game crossfade (2026-07-04)
- **Per-game wallpaper switching is now a smooth crossfade.** When you scroll between games that have different wallpapers, the video dissolves in place instead of flashing — no black blink. Turning a game's wallpaper **Off** cleanly shows that game's own art. Re-bake to apply (the plugin engine changed this time).

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