# Base44 Dev Environment

## What this app is
A Node.js Minecraft AFK bot (mineflayer) that keeps an Aternos server online 24/7, plus an Express status dashboard. Entry point: `index.js` (`npm start`).

## Running it
`docker compose -f docker-compose.base44.yml up -d` — single `bot` service on `node:22`, source bind-mounted at `/app`, deps installed on startup via `npm ci`, then `node index.js`. Dashboard exposed on host port 3000 (`PORT=3000`).

## Environment
- `PORT` — Express listen port (set to 3000 for the preview; app default is 5000).
- `RENDER_EXTERNAL_URL` — optional, only used for Render.com self-ping keep-alive. Gracefully skipped when unset (sandbox).
- All bot config lives in `settings.json` (server IP/port, account, anti-AFK, movement, discord webhook). No external credentials required to boot.
- `launcher_accounts.json` holds Microsoft auth accounts (empty by default; only needed for `online`/premium accounts, not the default `offline` mode).

## Verification
- `GET /ping` → `pong` (used by the compose healthcheck).
- `GET /health` → JSON bot status.
- `GET /` → HTML "AFK Bot Dashboard".
- The bot's core function (connecting to the external Minecraft server in `settings.json`) depends on a reachable Aternos server; in the sandbox it stays "disconnected" and retries — the dashboard still serves. To point it at a different server, edit `settings.json`.
