ROAD RUSH: OUTLAW CIRCUIT — Cloudflare multiplayer racing game

PACKAGE
- worker.js: complete game page + WebSocket room server
- wrangler.toml: Worker and Durable Object configuration
- .github/workflows/deploy.yml: deploy automatically from GitHub Actions
- index.html: standalone client preview/source copy (the deployed Worker serves the HTML embedded in worker.js)

GAMEPLAY
- Up to 5 riders in one private room; use the same room code on every phone
- Pseudo-3D road with moving lane markings, roadside scenery, skyline and hills
- Motorcycle paint choices and rider names
- Steering, throttle, brake, blaster, kick, nitro boost and temporary shield
- Nitro, repair, shield and ammo pickups
- Bike health, off-road damage, knockouts, race timer, position and finish screen
- Generated sound effects using Web Audio; no external audio files required
- Touch controls for phones; keyboard controls for desktop

DEPLOY USING ONLY A PHONE (GitHub Actions route)
1. Create a new GitHub repository from your phone.
2. Upload worker.js, wrangler.toml, README.txt, index.html, and the .github/workflows/deploy.yml file, preserving the folders exactly.
3. In Cloudflare Dashboard, create an API token with permission to edit Workers scripts and manage/create Durable Objects for the target account. Copy the token.
4. In GitHub mobile/browser, open the repository Settings → Secrets and variables → Actions → New repository secret. Add:
   - CLOUDFLARE_API_TOKEN = your Cloudflare API token
   - CLOUDFLARE_ACCOUNT_ID = your Cloudflare account ID
5. Push/commit the files to the main branch. GitHub Actions will run Wrangler deploy and create the SQLite-backed RaceRoom Durable Object namespace from wrangler.toml. You can also run the workflow manually from Actions → Deploy Road Rush to Cloudflare Workers.
6. Open the successful deployment log and copy the workers.dev URL. Open it on every phone.
7. Create a Wi-Fi hotspot, connect all phones to it, and ensure the hotspot phone has mobile data/internet. Everyone enters the same room code and taps JOIN RACE. The room host taps START RACE.

IMPORTANT HOTSPOT DETAIL
This build uses Cloudflare Durable Objects as the authoritative multiplayer server. A hotspot provides the shared Wi-Fi connection, but it does not make this an offline LAN game. The hotspot's upstream internet connection must work so all phones can connect to Cloudflare. If you need completely offline hotspot-only play with no mobile data/internet, that requires a different local-host architecture and cannot be provided by a Cloudflare Worker alone.

TEST STATUS / LIMITS
- JavaScript syntax was checked for both the Worker and embedded browser client.
- No live Cloudflare deployment or 2–5 physical-phone multiplayer test has been performed.
- This is a playable prototype foundation, not a finished commercial-grade game. Test it with friends before public release.
- Each room code creates a separate room; use a fresh code for another race.
