# CYBERDAWGS

A web-based tactical bullet-hell roguelite. Top-down, single-file, runs in any modern browser. Built with Pixi.js v7.

> A reimagining of the 1996 Activision shooter, with squad-coordinated AI inspired by F.E.A.R., procedurally generated maps, and a Frutiger Aero / Y2K cyber visual aesthetic.

**▶ [Play in browser](https://MrCarter421.github.io/cyberdawgs/)

---

## Controls

**Desktop**
- `WASD` — move
- `Space` or `Left Click` — fire
- `G` — toggle debug overlay (drone behavior labels, A* paths, cover slots, dead zones)
- `R` — restart current mission

**Mobile**
- Drag anywhere on the left half to spawn a virtual joystick
- Hold the magenta `FIRE` button (bottom-right) to shoot

---

## What's in here

- **Tactical squad AI** — drones use cover, peek-and-shoot, suppressive fire, and flanking maneuvers. A central squad coordinator assigns roles (HOLD / SUPPRESS / FLANK) every 0.35s and drones execute them with A* pathfinding and a per-unit FSM (`PATROL → ALERT → MOVE_TO_COVER → COVER → SEARCH`).
- **Callouts** — drones broadcast intent (`TARGET SPOTTED`, `FLANKING`, `MAN DOWN`) on state transitions, F.E.A.R.-style.
- **Procgen levels** — BSP partition → rooms → corridors → interior cover blocks. New seed every mission.
- **Mission loop** — play → score tally → black-market shop → deploy. Difficulty scales 15% per mission.
- **Loadout** — 4 weapons (PROTOTYPE pistol, AERO-9 SMG, SCATTER shotgun, ION LANCE plasma), 4 upgrade tracks (HP, damage, speed, fire rate), full-heal consumable.
- **Pickups** — health orbs, data chips (+40cr), and rare caches (+200cr).

---

## Deploy to GitHub Pages

The whole game is a single `index.html`. Pixi.js loads from a CDN, no build step.

1. **Create a new public repo** on GitHub. Suggested name: `CyberDawgs` (or `cyberdawgs`).
2. **Upload `index.html`** (and this `README.md`) to the root of the repo.
3. **Enable Pages**:
   - Repo → **Settings** → **Pages** (left sidebar)
   - **Source**: *Deploy from a branch*
   - **Branch**: `main` / folder: `/ (root)`
   - **Save**
4. Wait ~1 minute. Your game will be live at:
   ```
   https://<your-username>.github.io/CyberDawgs/
   ```
5. **Add a link from yuccabucca.com** — anywhere a `<a href="...">PLAY</a>` will work, since GitHub Pages serves over HTTPS and supports CORS-free embedding.

### Optional: embed in an iframe on yuccabucca.com

```html
<iframe
  src="https://<your-username>.github.io/CyberDawgs/"
  style="width:100%;height:100vh;border:0;display:block"
  allow="fullscreen"
  title="CyberDawgs">
</iframe>
```

The game is responsive and uses `position: fixed` with `viewport-fit=cover`, so it'll fill the iframe edge-to-edge.

### Optional: use a custom subdomain

If you want `cyberdawgs.yuccabucca.com` instead of the github.io URL:

1. In your domain registrar (GoDaddy), add a `CNAME` DNS record:
   - **Name/Host**: `cyberdawgs`
   - **Value/Points to**: `<your-username>.github.io`
2. In the repo, create a file at the root named `CNAME` containing exactly:
   ```
   cyberdawgs.yuccabucca.com
   ```
3. In GitHub repo Settings → Pages, enter `cyberdawgs.yuccabucca.com` in the "Custom domain" field and save. Wait for the SSL certificate to provision (a few minutes).

---

## Tech

- **Pixi.js 7.4** (CDN: `cdnjs.cloudflare.com`)
- Vanilla JS, no build step, no bundler
- Uses `ColorMatrixFilter` for the desaturated out-of-sight layer
- Visibility cone via Red Blob's corner-cast algorithm (3 rays per wall corner ±epsilon)
- A* pathfinding capped at 600 nodes per call, repath max once per 0.6s per drone
- HTML/CSS shop overlay (not Pixi) for cleaner styling and click delegation
- Storage in-memory only — no `localStorage` (loadout resets on tab close, easy to add later)

---

## Build by

[yuccabuccA](https://yuccabucca.com) · 2026
