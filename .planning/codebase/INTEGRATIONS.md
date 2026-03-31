# External Integrations

**Analysis Date:** 2026-03-31

## APIs & External Services

**None detected** — the game has no runtime API calls, no SDKs for third-party services, and no network requests in any `.rpy`, `index.html`, or `town.html` file. All content is bundled locally.

## Data Storage

**Databases:**
- None — no database connection of any kind

**Save System (Ren'Py built-in):**
- Ren'Py's native file-based save system
- Save directory: `"SudoRoom: a Love Story-1390591801"` (configured in `game/options.rpy`)
- Ignored by git: `game/saves/` is listed in `.gitignore`
- Supports: save slots, quick save, auto save (via `game/screens.rpy` file picker UI)

**Persistent Data:**
- Ren'Py `persistent` store (built-in) — stores preferences across sessions
- Reset by deleting `game/saves/persistent`

**File Storage:**
- Local filesystem only — all assets are bundled in `game/assets/`, `game/images/`

**Caching:**
- None — Ren'Py handles its own bytecode cache (`.rpyc` files committed to repo)

## Authentication & Identity

- None — no login, accounts, or authentication of any kind

## Audio Assets

All audio is bundled locally in `game/assets/audio/`. Referenced directly in `game/script.rpy` via `play music "assets/audio/..."`.

**Background Music:**
- `game/assets/audio/bgmusic/209643__speedenza__sombre-ambiance.wav` — ambient background music
- `game/assets/audio/meetingmusic/173148__ducksingel__a-company-s-reception.aiff` — meeting scene music

**Sound Effects / Scene Audio:**
- `game/assets/audio/crowd-drums.wav` — used in Art Murmur opening scene (`play music "assets/audio/crowd-drums.wav"`)
- `game/assets/audio/crowd-laughter.wav` — crowd ambiance
- `game/assets/audio/organ-loop.wav` — used in outdoor piano scene (`play music "assets/audio/organ-loop.wav"`)

**Formats:** WAV (primary), AIFF (one file)

**Attribution notes:** Filenames include Freesound.org numeric IDs (`209643__speedenza__`, `173148__ducksingel__`), indicating these are Creative Commons assets sourced from freesound.org.

## Video Assets

All video bundled locally in `game/assets/movies/`. Not yet referenced in `game/script.rpy` — present as assets for future scene use.

- `game/assets/movies/ccnight.mp4`
- `game/assets/movies/dancing-hackerhappyhour.mp4`
- `game/assets/movies/latenight.mp4`
- `game/assets/movies/snakeparty-drummers.mp4`
- `game/assets/movies/snakeparty-painting.mp4`

**Format:** MP4

## Image Assets

**Character Sprites** (`game/images/characters/`):
- `sudocat/` — 11 PNG sprites with directional/expression variants (faceleft, faceright, eyesclosed, tilt variants)
- `boxybox/` — 6 PNG sprites (faceleft/faceright, normal/lookdown/headup)
- `greene/` — 3 PNG sprites (anxious, excited, smile)

**Backgrounds** (`game/images/backgrounds/`):
- `artmurmur/` — 4 PNG backgrounds (cars, crowd, gallery, sign)
- `mainroom/` — 1 JPG (meeting), 1 PNG (workshop3dprinting)
- `outdoors/` — 1 PNG (piano)
- `startpage.png` — main menu background (referenced in `game/options.rpy` `mm_root`)
- `sudoroom/` — 3 JPG backgrounds (3dprinterroom, darksudoroom, frontdoor)

**Formats:** PNG (primary), JPG (some backgrounds)

**Web/Landing Page Images** (`images/`):
- `images/SudoRoom_A_Love_Story.png` — title logo used in `index.html`
- `images/screenshots/` — development screenshots and prototype images (not used in game)
- `images/prototypeRecording.mov`, `images/prototypeRecording_sm.mov` — prototype recordings (referenced in `README.md`)

## Web Components

**`index.html` — Animated Landing Page:**
- Self-contained HTML/CSS/JS, no external dependencies
- Uses `game/images/backgrounds/startpage.png` as parallax background layer
- Uses `images/SudoRoom_A_Love_Story.png` as title logo
- Uses `game/images/characters/sudocat/sudocat-normal.png` for animated cat display
- Links to `town.html` (Explore Oakland Town button) and `README.html` (About link)
- Canvas-based animated sparkle particle system (vanilla JS)

**`town.html` — Isometric Oakland Town RPG:**
- Self-contained HTML5 Canvas game, no external libraries
- Isometric tile-based map (22×18 grid) rendered via Canvas 2D API
- Represents real Oakland geography: Shattuck Ave, 51st St, 48th St, Temescal neighborhood, SudoRoom location
- Player controls: WASD keyboard movement, tile walkability system
- Features: HUD overlay, mini-map canvas, location name popups
- Links back to `index.html`

## External URLs Referenced

- SudoRoom wiki: `https://sudoroom.org/wiki/SudoRoomVisualNovelGame` (in `README.md`)
- itch.io distribution: `https://romyilano.itch.io/sudoroom-a-love-story` (in `README.md`)

## Monitoring & Observability

- None — no error tracking, analytics, or logging services
- Ren'Py writes local error logs: `traceback.txt`, `errors.txt`, `log.txt` (all present in repo root, listed in `.gitignore` via `*.log`)

## CI/CD & Deployment

- No CI pipeline detected
- No deployment scripts detected
- Distribution via Ren'Py SDK's built-in export (produces standalone executables)
- Web demo hosted externally on itch.io

## Webhooks & Callbacks

- None

---

*Integration audit: 2026-03-31*
