# Nova Duel Online ✦

A neon, zero-gravity artillery duel for two players — think *Worms* meets *Scorched Earth*, wrapped in a synthwave sci-fi skin. Built as a single self-contained HTML file with real-time peer-to-peer multiplayer, no server, no backend, no install.

Play it live: **[zeekecc.github.io/ndonline](https://zeekecc.github.io/novaduel/)**

![status](https://img.shields.io/badge/status-active-brightgreen) ![type](https://img.shields.io/badge/type-single--file%20HTML5-blueviolet) ![network](https://img.shields.io/badge/multiplayer-P2P%20WebRTC-26e6ff)

---

## What is this?

Two mechs face off across destructible terrain on opposite sides of the screen. On your turn, dial in an angle and power, launch your shot, and watch gravity and wind carry it toward your opponent. Direct hits and near-misses crater the ground and chip away HP. First mech to zero loses.

- 🎯 **Turn-based artillery combat** — classic angle/power/wind mechanics
- 🌌 **Procedurally generated terrain** — a new battlefield every round
- 💥 **Destructible ground** — craters persist and reshape the fight
- 🛰️ **True peer-to-peer multiplayer** — no game server, no lobby backend, no accounts
- ✨ **Full canvas rendering** — stars, nebulae, particle explosions, scanline FX
- 📱 **Fills the whole browser window** — no fixed layout, scales to any screen

## How it works

The game runs entirely client-side in a single `.html` file. Two players connect directly to each other over **WebRTC** using [PeerJS](https://peerjs.com/) — one player **hosts** a match and gets a shareable room code, the other **joins** using that code. Once connected, the host's browser runs the authoritative physics simulation (terrain, projectiles, damage) and streams the results to the guest in real time.

No account system, no matchmaking server, no database — the two browsers talk directly to each other.

## Playing a match

1. Open the game in your browser.
2. One player clicks **Host Match** and shares the generated room code with the other.
3. The other player clicks **Join Match**, enters the code, and connects.
4. Take turns aiming (angle/power) and firing — destroy your opponent's mech first.

**Controls**

| Player | Angle | Power | Fire |
|---|---|---|---|
| Player 1 (Host) | `A` / `D` | `W` / `S` | `Space` |
| Player 2 (Guest) | `←` / `→` | `↑` / `↓` | `Enter` |

You can also use the on-screen sliders and Launch button. Firing is only enabled on your turn.

## Running it yourself

Because the game uses WebRTC, it needs to be served over `http(s)://` — opening the file directly via `file://` will break peer connections (browsers treat local files as isolated origins). To run locally:

```bash
# Python
python -m http.server 8000

# or Node
npx serve -l 8000
```

Then visit `http://localhost:8000/nova_duel_online.html`.

## Cross-network play (TURN)

WebRTC connections between two different networks (e.g. two players in different homes) sometimes can't establish a direct path due to NAT/firewalls, and need a TURN relay server as a fallback. This project fetches short-lived TURN credentials from a small Cloudflare Worker at connect-time, rather than embedding secrets in the client. See the [Wiki](../../wiki) for setup details if you're self-hosting.

## Tech stack

- Vanilla JavaScript, no build step, no framework
- HTML5 Canvas for all rendering
- [PeerJS](https://peerjs.com/) (WebRTC wrapper) for peer-to-peer networking
- Cloudflare Realtime TURN + a Cloudflare Worker for cross-network relay credentials

## Documentation

More detail — architecture notes, networking internals, and troubleshooting — lives on the **[Wiki](../../wiki)**.

## License

MIT — see [LICENSE](LICENSE).
