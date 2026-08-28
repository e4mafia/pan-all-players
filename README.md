**# Pan All Players

A tiny Foundry VTT module that lets the GM pan every connected player's
camera to a chosen point, a selected token, or a clicked location on the
canvas — with zero action required from players. Built on
[socketlib](https://github.com/manuelVo/foundryvtt-socketlib).

## Requirements

- Foundry VTT v11–v13
- The [socketlib](https://foundryvtt.com/packages/socketlib) module (install
  from the normal Foundry package browser — it's on the official list)

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
******
