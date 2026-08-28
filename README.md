# Pan All Players

A tiny Foundry VTT module that lets the GM pan every connected player's
camera to a chosen point, a selected token, or a clicked location on the
canvas — with **zero action required from players**. Built on
[socketlib](https://github.com/manuelVo/foundryvtt-socketlib).

## Requirements

- Foundry VTT v11–v13
- The [socketlib](https://foundryvtt.com/packages/socketlib) module (install
  from the normal Foundry package browser — it's on the official list)

## Installing on The Forge

1. Push this repo to GitHub (see below) so `module.json` is reachable at a
   raw URL.
2. In your Foundry world (running on Forge), go to
   **Setup → Add-on Modules → Install Module**.
3. Paste the manifest URL into the **Manifest URL** field:
   ```
   https://raw.githubusercontent.com/YOURUSERNAME/pan-all-players/main/module.json
   ```
4. Click **Install**, then enable both **socketlib** and **Pan All Players**
   for your world under **Manage Modules**.
5. Reload the world. Players don't need to install or do anything else —
   the listener registers automatically for every connected client.

## Publishing this repo to GitHub

If you don't already have this on GitHub:

```bash
cd pan-all-players
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/pan-all-players.git
git push -u origin main
```

Then edit `module.json` and replace every `YOURUSERNAME` with your actual
GitHub username, commit, and push again so the manifest URLs are correct.

## Usage (GM only)

Three ways to trigger a pan, all via the module's API:

**Scene control button** — a crosshair icon appears in the token controls
toolbar. Click it, then click anywhere on the canvas.

**Macro — pan to a token** (uses your currently selected token if none is
passed):
```js
game.modules.get("pan-all-players").api.panAllToToken();
```

**Macro — pan to a click:**
```js
game.modules.get("pan-all-players").api.panAllByClick();
```

**Macro — pan to exact coordinates** (`x`, `y`, optional `scale`):
```js
game.modules.get("pan-all-players").api.panAllTo(1200, 800, 1);
```

## How it works

`scripts/main.js` registers a socketlib function (`panTo`) on every client
as soon as the module loads via the `socketlib.ready` hook. Only the GM's
API calls actually broadcast a pan, but the *receiving* function exists on
every client automatically — no manual per-player setup, no macro that
players need to run.

## License

MIT — do whatever you want with it.
