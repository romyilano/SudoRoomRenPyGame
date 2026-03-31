# Technology Stack

**Analysis Date:** 2026-03-31

## Languages

**Primary:**
- RenPy Script (`.rpy`) — core visual novel game logic, character definitions, scene transitions, branching dialogue
- Python — embedded directly in `.rpy` files via `init python hide:` and `$ variable =` blocks for game state variables
- JavaScript (ES2015+, strict mode) — isometric town map in `town.html`, animated landing page in `index.html`
- HTML5 / CSS3 — web entry points for the project (`index.html`, `town.html`)

**Secondary:**
- RenPy Compiled Bytecode (`.rpyb`, `.rpyc`) — pre-compiled Ren'Py script files; `game/bytecode.rpyb`, `game/options.rpyc`, `game/screens.rpyc`, `game/script.rpyc`

## Runtime

**Environment:**
- Ren'Py SDK — confirmed version **6.16.5.525** (from `traceback.txt` stack trace referencing `/Users/romyilano/Developer/python/renpy-6.16.5-sdk/`)
- Python 2.x — embedded Python runtime bundled with Ren'Py 6.x (Ren'Py 6 uses Python 2)
- Browser / HTML5 Canvas — required for `index.html` and `town.html` (no Node.js runtime; pure client-side)

**Package Manager:**
- None — no `package.json`, `requirements.txt`, `Cargo.toml`, or `go.mod` detected
- Lockfile: Not applicable

## Frameworks

**Core:**
- Ren'Py 6.16.5 — visual novel engine handling scene rendering, dialogue, menus, save/load, audio playback, transitions
  - Screen Language (used in `game/screens.rpy`) — Ren'Py's declarative UI system for menus, preferences, save/load screens
  - `theme.bordered()` — Ren'Py built-in theme applied in `game/options.rpy` with a "Basic Blue" color scheme

**Build/Dev:**
- Ren'Py SDK launcher — used directly to run and build the game; no separate build script detected
- IntelliJ IDEA / PyCharm — `.idea/` project files present, indicating IDE used for development

## Key Dependencies

**Critical:**
- Ren'Py 6.16.5 SDK — the entire game engine; must be installed locally to run the `.rpy` game. Developer's SDK path: `/Users/romyilano/Developer/python/renpy-6.16.5-sdk/`

**Web Components (no external CDN dependencies):**
- `index.html` — self-contained; uses only native browser APIs (Canvas 2D, CSS animations, vanilla JS)
- `town.html` — self-contained; uses only native browser Canvas 2D API, no external libraries

## Configuration

**Game Configuration (`game/options.rpy`):**
- Window title: `"SudoRoom: a Love Story"`
- Game name: `"SudoRoom: a Love Story"`
- Version: `"0.0"` (pre-release)
- Screen resolution: `800 × 600`
- Developer mode: `config.developer = True` (not yet set to False for release)
- Audio: music enabled (`config.has_music = True`), sound effects enabled (`config.has_sound = True`), voice disabled (`config.has_voice = False`)
- Default fullscreen: `False`
- Default text speed: infinite (`config.default_text_cps = 0`)
- Save directory: `"SudoRoom: a Love Story-1390591801"` (set in `python early:` block)
- Help file: `README.html`

**Theme Colors:**
- Widget idle: `#003c78`
- Widget hover: `#0050a0`
- Widget text: `#c8ffff`
- Frame: `#6496c8`
- Main menu background: `game/images/backgrounds/startpage.png`
- Game menu background: `#dcebff`

## Platform Requirements

**Development:**
- macOS (confirmed — `Darwin-13.0.0-x86_64` from traceback, `.idea/` config present)
- Ren'Py 6.16.5 SDK installed locally at `/Users/romyilano/Developer/python/renpy-6.16.5-sdk/`
- Modern web browser (for `index.html` / `town.html` prototypes)

**Production:**
- Ren'Py distributable build (Windows, macOS, Linux via Ren'Py SDK export)
- Web demo hosted on itch.io: `https://romyilano.itch.io/sudoroom-a-love-story` (referenced in `README.md`)
- Static HTML files (`index.html`, `town.html`) deployable to any web host with no server-side requirements

---

*Stack analysis: 2026-03-31*
