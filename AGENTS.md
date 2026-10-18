# Base44 Notes

This repo is a Node.js Minecraft AFK bot (`index.js`) that also serves an Express web dashboard on `PORT` (default 5000).

## Running in the sandbox
- `docker compose -f docker-compose.base44.yml up -d` runs the app from source on `node:20-bookworm`, host port 3000 → container 5000.
- Dependencies install on container start (`npm install --omit=dev`); no image rebuild needed for code edits (source is bind-mounted).
- No live-reload dev server (plain `node index.js`); call `reload_preview` after editing server code so the preview picks it up. Static files under `public/` are served directly and refresh on full page reload.

## Candy Crush game
- Route `GET /candy-crush` serves `public/candy-crush.html` (self-contained HTML/CSS/JS, no build step).
- The dashboard at `/` has a "Play Candy Crush" button linking to it.
- Game logic lives in an IIFE in that file; the board is absolutely-positioned candies animated via CSS transitions.

## Verify
- `curl localhost:3000/` → 200 (dashboard)
- `curl localhost:3000/candy-crush` → 200 (game)
- `node --check index.js` validates the server.
