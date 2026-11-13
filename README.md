# Neon Dash

A tiny, **mobile-first endless runner** in one HTML file. Tap to jump, tap again for a double jump, hop the neon blocks, duck under the floaters and grab the coins. No engine, no dependencies, no build step, no network calls — open `index.html` and play.

**License: MIT** (see `LICENSE`). Free to use, fork, remix and ship.

---

## Play

- **Phone / tablet:** open `index.html` in any modern browser. Tap anywhere to jump, tap the ❚❚ button to pause, 🔊 to mute.
- **Desktop:** `Space` / `↑` / `W` to jump, `P` or `Esc` to pause.
- **Host it:** drop `index.html` on GitHub Pages, Netlify, Vercel, Cloudflare Pages, or any static host. It is a single file with zero assets, so it also works fully offline once loaded (and can be added to a phone home screen).

### Run locally

```bash
# any static server works
python3 -m http.server 8080
# then open http://localhost:8080
```

Or just double-click `index.html` — `file://` works too.

## How to play

| Object | Colour | What to do |
| --- | --- | --- |
| Ground block | Cyan | Jump over it |
| Floating block | Pink | Stay on the ground — running under it is safe |
| Coin | Gold | Collect it for +5 points |

Score also climbs with distance, and the world speeds up the longer you survive. Best score is stored in `localStorage` on your device.

## Features

- **True mobile-first**: `viewport-fit=cover`, safe-area insets for notches, `touch-action: none` (no page scrolling or pull-to-refresh), 44 px touch targets, works in portrait and landscape.
- **One-tap controls** with double jump, forgiving hitboxes (6 px inset) and jump physics that scale with screen height, so it feels the same on a small phone and a big tablet.
- **Device-pixel-ratio aware canvas** (capped at 2× for battery), delta-time physics clamped so it survives tab switches and slow frames.
- **Procedural everything**: parallax starfield, neon perspective grid, particles, screen shake, coin arcs — no image or font assets.
- **WebAudio sound effects generated in code**, with a persisted mute toggle, plus `navigator.vibrate` haptics on impact.
- **Auto-pause** when the tab is hidden or the window loses focus.
- **Accessible-ish**: keyboard playable, respects reduced clutter on short screens, high-contrast neon palette on near-black.
- **Zero dependencies**: ~30 KB of HTML/CSS/JS, no frameworks, no analytics, no cookies, no tracking.

## Project structure

```
.
├── index.html   # the whole game: markup, styles, engine, audio
├── LICENSE      # MIT
└── README.md
```

## Tuning the game

Most of the feel lives in two places inside `index.html`:

- `layout()` — physics and geometry: `gravity`, `jumpV` (jump strength), `speedStart`, `speedMax`, `accel`, ground height, player size.
- `spawnObstacle()` / `spawnCoinArc()` — difficulty curve: obstacle sizes, the floater-vs-block mix, and how tightly they are packed.

A debug hook is exposed for automated tests:

```js
window.__neonDash.state()   // { mode, score, best, obs, coins, speed }
window.__neonDash.start()   // start a run
window.__neonDash.jump()
```

## Tested

Played headlessly in Chromium at 390×844 (portrait phone) and 740×360 (landscape), covering start, jump, double jump, coin pickup, collision, game over, best-score persistence, restart, pause and resume — with zero console errors. Not yet verified on real iOS/Android hardware.

## Ideas for a fork

- Boss patterns, power-ups (shield / magnet / slow-mo)
- Daily seeded runs with a shareable score
- Gamepad and tilt controls
- Sprite art or a WebGL renderer
- Online leaderboard (the only thing that would need a backend)

## Contributing

Issues and pull requests are welcome. Keep it dependency-free and single-file, and check that it still runs on a phone in portrait and landscape before opening a PR.

## License

MIT © 2026 Kalu
