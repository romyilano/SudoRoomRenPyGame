# Architecture

**Analysis Date:** 2026-03-31

## Pattern Overview

**Overall:** Linear visual novel with branching dialogue trees and persistent state flags

**Key Characteristics:**
- Single-file script architecture: all narrative logic lives in `game/script.rpy`
- Label-based scene graph: each story beat is a named `label`, navigated with `jump`
- State tracked via Python variables set inline with `$` assignments
- ADV (adventure) mode dialogue: one character speaks at a time in a dialogue window
- No custom Python classes — all game logic is procedural within the Ren'Py DSL

## Layers

**Narrative / Script Layer:**
- Purpose: Defines all story content, scene transitions, branching menus, and character dialogue
- Location: `game/script.rpy`
- Contains: `label` blocks, `menu` blocks, `scene`, `show`, `play`, `jump`, `$` variable assignments
- Depends on: Image declarations at the top of `script.rpy`, audio file paths under `game/assets/audio/`
- Used by: Ren'Py engine runtime

**UI / Screen Layer:**
- Purpose: Defines all in-game and system menu screens (dialogue box, choice screen, save/load, preferences)
- Location: `game/screens.rpy`
- Contains: `screen` blocks — `say`, `choice`, `nvl`, `main_menu`, `navigation`, `file_picker`, `save`, `load`, `preferences`, `yesno_prompt`, `quick_menu`
- Depends on: Ren'Py screen language, style system
- Used by: Ren'Py engine; `say` screen renders all dialogue, `choice` screen renders all `menu` blocks

**Configuration Layer:**
- Purpose: Declares engine settings, theme, audio capabilities, screen dimensions, save directory
- Location: `game/options.rpy`
- Contains: `init -1 python hide` blocks setting `config.*` and `theme.bordered(...)` values
- Depends on: Nothing (runs at init priority -1, before game script)
- Used by: All other layers

**Asset Layer:**
- Purpose: Provides all visual and audio content referenced by the script
- Location: `game/images/`, `game/assets/`
- Contains: Character sprite PNGs, background PNGs/JPGs, WAV audio loops, MP4 movies
- Depends on: Nothing (static files)
- Used by: `game/script.rpy` via `image` declarations and `scene`/`show`/`play` statements

## Data Flow

**Player Progresses Through Dialogue:**

1. Ren'Py engine executes `label start:` in `game/script.rpy`
2. `scene` statement swaps the background displayable
3. Narration and character dialogue render through the `say` screen in `game/screens.rpy`
4. A `menu:` block pauses execution and renders choices via the `choice` screen
5. Player's selection causes a `jump` to the corresponding label
6. Execution continues from the new label

**State Branching:**

1. Player choices trigger `$ variable = value` assignments inline in the script
2. Later `if/else` blocks in `game/script.rpy` read these variables to show different dialogue lines
3. Variables persist for the current session (not persisted across saves unless in a save slot)

**State Variables (defined in `label start`):**

| Variable | Type | Purpose |
|---|---|---|
| `hackertype` | string | Tracks what kind of hacker the player identifies as (default: `"generic"`) |
| `has_dreams` | bool | Whether the player said they have dreams; branches SudoCat's pitch |
| `first_time` | bool | Controls whether Boxy Box gives the full welcome tour or offers a menu |
| `tour_first_time` | bool | Controls whether the tour scene uses first-visit or repeat-visit dialogue |

## Scene / Label Graph

```
label start
  ├── menu: "What's a hackerspace?" → jump starthackerspace
  └── menu: "Hackers...break into things?" → jump startbadhackers

label startbadhackers
  ├── nested menus (inline, no jumps)
  └── falls through to label starthackerspace (implicit fall-through)

label starthackerspace
  ├── menu: has_dreams branch (sets $ has_dreams)
  └── falls through to label sudoorganscene

label sudoorganscene
  └── falls through to label sudoroommainroom

label sudoroommainroom
  ├── if first_time → jump tour
  └── else menu:
        ├── jump tour
        ├── jump tutorial
        └── jump party

label tour
  └── jump sudoroommainroom (loops back)

label tutorial
  ├── jump tutorial_3DPrinter
  ├── jump tutorial_activism
  ├── jump tutorial_biohacking
  └── jump tutorial_bikes

label tutorial_3DPrinter  → jump tutorial (stub)
label tutorial_activism   → jump tutorial (stub)
label tutorial_biohacking → jump tutorial (stub)
label tutorial_bikes      → jump tutorial (stub)

label party               → jump tutorial (stub)

label end
  (terminal — reached only via explicit jump)
```

## Characters

Characters are defined at the top of `game/script.rpy` using `define`:

| Variable | Display Name | Text Color | Role |
|---|---|---|---|
| `m` | Me | `#c8ffc8` | Player protagonist (unnamed) |
| `s` | SudoCat | `#c8ffc8` | Guide character; introduces SudoRoom at Art Murmur |
| `g` | Greene | `#cccccc` | Supporting character (sprites present, limited script use) |
| `b` | Boxy Box | `#e5eeee` | Guide character; gives physical tour of SudoRoom |
| `peeps` | SudoRoom People | `#c8ffc8` | Crowd voice; delivers group dialogue during tour |

## Character Sprite System

Sprites use Ren'Py's multi-word image tag system. The image name encodes pose metadata as space-separated tokens.

**Pattern:** `image [character] [facing] [expression] [modifier]`

**SudoCat examples:**
- `image sudocat faceleft normal` → `game/images/characters/sudocat/sudocat-normal.png`
- `image sudocat faceright eyesclosed tiltdown` → `game/images/characters/sudocat/sudocat-rightfacing-eyesclosed-tiltdown.png`

**BoxyBox examples:**
- `image boxybox faceright normal headup` → `game/images/characters/boxybox/boxybox-normal-right-headup.png`
- `image boxybox faceleft lookdown` → `game/images/characters/boxybox/boxybox-lookdown-left.png`

**Greene examples:**
- `image greene faceright anxious` → `game/images/characters/greene/doggy-anxious.png`
- `image greene faceright smile` → `game/images/characters/greene/doggy-smile.png`

**Show statement usage:** Characters are positioned with `at left` or `at right` transforms built into Ren'Py. Pose changes are achieved by re-issuing `show` with a different image tag on the same character.

## Entry Points

**Game Start:**
- Location: `label start:` in `game/script.rpy` (line 61)
- Triggers: Player clicks "Start Game" from the main menu
- Responsibilities: Initializes all game variables, fires first scene (`bg artmurmur cars`), plays opening music

**Main Menu:**
- Location: `screen main_menu:` in `game/screens.rpy` (line 175)
- Triggers: Engine launch or `MainMenu()` action
- Responsibilities: Renders Start, Load, Preferences, Help, Quit buttons

## Audio Architecture

Audio is triggered inline in the script with `play music` and `stop music` statements. No audio manager abstraction exists — audio is entirely imperative.

**Active audio files referenced in script:**
- `assets/audio/crowd-drums.wav` — plays during Art Murmur opening
- `assets/audio/organ-loop.wav` — plays during outdoor organ scene

**Additional audio assets (not yet referenced in script):**
- `assets/audio/crowd-laughter.wav`
- `assets/audio/bgmusic/209643__speedenza__sombre-ambiance.wav`
- `assets/audio/meetingmusic/173148__ducksingel__a-company-s-reception.aiff`

**Movie assets (not yet referenced in script):**
- `assets/movies/ccnight.mp4`
- `assets/movies/dancing-hackerhappyhour.mp4`
- `assets/movies/latenight.mp4`
- `assets/movies/snakeparty-drummers.mp4`
- `assets/movies/snakeparty-painting.mp4`

## Error Handling

**Strategy:** None explicit. Ren'Py's engine handles runtime errors by displaying a traceback overlay (developer mode is currently enabled via `config.developer = True` in `game/options.rpy`).

## Cross-Cutting Concerns

**Transitions:** `with dissolve` used on `scene` changes. All menu transitions set to `None` in `options.rpy`.

**Save System:** Standard Ren'Py file-slot saves. Save directory is `SudoRoom: a Love Story-1390591801` (configured in `game/options.rpy`). State variables are serialized automatically by Ren'Py's save mechanism.

**Internationalization:** `_("string")` wrapper used on all UI button labels in `screens.rpy`. Narrative dialogue strings are not wrapped (not i18n-ready).

---

*Architecture analysis: 2026-03-31*
