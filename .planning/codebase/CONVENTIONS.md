# Conventions

## Label Naming
- **Rule:** `snake_case` only — hyphens in label names are **invalid** in Ren'Py and cause parse errors
- **Evidence:** `errors.txt` contains parse errors from hyphenated label names (e.g., `label art-murmur:`)
- **Correct pattern:** `label art_murmur:`, `label sudo_room:`, `label start:`

## Character Definitions
- Single-letter variable names: `m` (MC/narrator), `s` (Sudocat), `g` (Greene the dog), `b` (Boxybox), `peeps` (crowd)
- Defined at the top of `game/script.rpy` with hex color codes for name display
- Pattern: `define x = Character("Name", color="#XXXXXX")`

## Image Declaration Tokens
- Space-separated descriptor tokens used in `image` statements
- Sprite variants use descriptors: `faceleft`, `faceright`, `eyesclosed`, `tiltback`, `tiltforward`, `tiltleft`, `tiltright`, `headup`, `lookdown`, `normal`
- Pattern: `image sudocat normal = "game/images/characters/sudocat/sudocat-normal.png"`

## Asset File Naming
- **Sprites:** `kebab-case` — e.g., `sudocat-rightfacing-eyesclosed-tiltdown.png`
- **Audio:** `kebab-case` — e.g., `crowd-laughter.wav`, `organ-loop.wav`
- **Video:** `kebab-case` — e.g., `snakeparty-drummers.mp4`, `dancing-hackerhappyhour.mp4`
- **Backgrounds:** `kebab-case` — e.g., `3dprinterroom.jpg`, `frontdoor.jpg`

## Game Variable Conventions
- Variables use `snake_case`
- Initialized in `label start:` at game beginning
- One-shot boolean flags for tracking story state
- Default values set with Ren'Py `default` statement or in label start

## Scene & Audio Patterns
- Scenes introduced with `scene bg_name` or `scene bg_name with transition`
- Background music: `play music "path/to/file.wav" fadein X`
- Sound effects: `play sound "path/to/file.wav"`
- Transitions: standard Ren'Py transitions (`dissolve`, `fade`)

## Dialogue Style
- Character dialogue: `x "spoken text"`
- Narration: `"narrator text"` (no character prefix)
- Menu choices use `menu:` with indented option strings

## Configuration (`options.rpy`)
- `config.name` — game title
- `config.version` — version string
- `config.developer` — set to `True` for developer console access
- Window size and display settings defined here

## Version Control
- Source `.rpy` files committed
- Compiled `.rpyc` and `.rpyb` files committed (typical for Ren'Py projects shared without SDK)
- Binary assets (PNG, WAV, MP4, AIFF) committed directly to repo
- `.gitattributes` present for binary diff handling
