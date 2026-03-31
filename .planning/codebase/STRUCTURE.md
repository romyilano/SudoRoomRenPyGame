# Structure

## Directory Tree

```
SudoRoomRenPyGame/
├── game/                          # All Ren'Py game content
│   ├── script.rpy                 # Main narrative script — all scenes, dialogue, logic
│   ├── script.rpyc                # Compiled bytecode (auto-generated)
│   ├── options.rpy                # Game configuration (title, version, display settings)
│   ├── options.rpyc               # Compiled options bytecode
│   ├── screens.rpyc               # Compiled UI screens (no source .rpy present)
│   ├── bytecode.rpyb              # Ren'Py bytecode cache
│   ├── images/                    # All visual assets
│   │   ├── backgrounds/           # Scene backgrounds organized by location
│   │   │   ├── artmurmur/         # Art Murmur event backgrounds
│   │   │   │   ├── cars.png
│   │   │   │   ├── gallery.png
│   │   │   │   ├── crowd.png
│   │   │   │   └── sign.png
│   │   │   ├── mainroom/          # SudoRoom main room backgrounds
│   │   │   │   ├── meeting.jpg
│   │   │   │   └── workshop3dprinting.png
│   │   │   ├── sudoroom/          # SudoRoom interior backgrounds
│   │   │   │   ├── 3dprinterroom.jpg
│   │   │   │   ├── frontdoor.jpg
│   │   │   │   └── darksudoroom.jpg
│   │   │   ├── outdoors/          # Outdoor scene backgrounds
│   │   │   │   └── piano.png
│   │   │   └── startpage.png      # Title/start screen background
│   │   └── characters/            # Character sprites organized by character
│   │       ├── sudocat/           # Sudocat sprite variants (11 expressions/poses)
│   │       ├── greene/            # Greene the dog sprites (3 expressions)
│   │       └── boxybox/           # Boxybox sprites (6 poses/directions)
│   └── assets/                    # Non-image media assets
│       ├── audio/                 # Sound and music files
│       │   ├── bgmusic/           # Background music loops
│       │   │   └── 209643__speedenza__sombre-ambiance.wav
│       │   ├── meetingmusic/      # Meeting scene music
│       │   │   └── 173148__ducksingel__a-company-s-reception.aiff
│       │   ├── crowd-laughter.wav # Sound effects
│       │   ├── crowd-drums.wav
│       │   └── organ-loop.wav
│       └── movies/                # Video assets
│           ├── snakeparty-drummers.mp4
│           ├── snakeparty-painting.mp4
│           ├── latenight.mp4
│           ├── ccnight.mp4
│           └── dancing-hackerhappyhour.mp4
├── images/                        # Project-level images (not game assets)
│   └── SudoRoom_A_Love_Story.png  # Promotional/README image
├── README.md                      # Project documentation
├── README.html                    # HTML version of README
├── errors.txt                     # Ren'Py error log (auto-generated on crash)
├── .gitignore
└── .gitattributes
```

## Key File Locations

| Purpose | File |
|---------|------|
| All game narrative/scenes | `game/script.rpy` |
| Game configuration | `game/options.rpy` |
| UI/screens | `game/screens.rpyc` (compiled only) |
| Error log | `errors.txt` |
| Background images | `game/images/backgrounds/` |
| Character sprites | `game/images/characters/` |
| Background music | `game/assets/audio/bgmusic/` |
| Sound effects | `game/assets/audio/*.wav` |
| Video cutscenes | `game/assets/movies/` |

## Naming Conventions

| Asset Type | Convention | Example |
|-----------|------------|---------|
| Background images | `kebab-case.ext` | `frontdoor.jpg` |
| Character sprites | `charname-descriptor-descriptor.png` | `sudocat-rightfacing-eyesclosed.png` |
| Audio files | `kebab-case.ext` | `crowd-laughter.wav` |
| Video files | `kebab-case.mp4` | `snakeparty-drummers.mp4` |
| Ren'Py labels | `snake_case` | `label art_murmur:` |
| Ren'Py image tags | space-separated tokens | `image sudocat normal` |

## Where to Add New Content

| New Content | Location |
|-------------|----------|
| New scene/chapter | Add `label scene_name:` block in `game/script.rpy` |
| New character | Add `define x = Character(...)` at top of `game/script.rpy` + sprites in `game/images/characters/charname/` |
| New background | Add image to `game/images/backgrounds/location/` + declare in `script.rpy` |
| New background music | Add to `game/assets/audio/bgmusic/` |
| New sound effect | Add to `game/assets/audio/` |
| New video cutscene | Add to `game/assets/movies/` |
| UI screen changes | Requires adding/editing `game/screens.rpy` (currently only compiled version exists) |
| Tutorial branches | Add stub labels in `script.rpy` (currently 4 empty stubs exist) |

## Generated vs. Committed Files

- **Committed (source):** `*.rpy`, all assets (PNG, JPG, WAV, AIFF, MP4)
- **Committed (compiled):** `*.rpyc`, `*.rpyb` — unusual but common for Ren'Py distribution
- **Not committed:** Ren'Py SDK itself, `traceback.txt` (runtime crash logs)
