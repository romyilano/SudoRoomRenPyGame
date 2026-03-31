# Concerns

## Critical: Syntax Errors Preventing Game Launch
8 syntax errors in `game/script.rpy` confirmed by `errors.txt`. The root cause is **hyphenated label names** — Ren'Py does not allow hyphens in label identifiers.

Examples of broken labels:
- `label art-murmur:` → must be `label art_murmur:`
- Any other labels using hyphens

**Impact:** Game cannot launch until all hyphenated labels are renamed to `snake_case`.

## Critical: Stale/Corrupt Bytecode
`traceback.txt` confirms a `.rpyc` bytecode issue. Compiled bytecode (`.rpyc`, `.rpyb`) is out of sync with source `.rpy` files.

**Fix:** Delete all `.rpyc` and `.rpyb` files and let Ren'Py recompile from source on next launch.

## High: Very Outdated Ren'Py Version
The project targets **Ren'Py 6.16.5 (circa 2013)** — over a decade old. Current Ren'Py is 8.x.

**Risks:**
- Missing modern Ren'Py features and APIs
- Security/compatibility issues on modern OS versions
- Limited community support for debugging

## High: Developer Mode Left Enabled
`config.developer = True` in `game/options.rpy` is appropriate for development but must be disabled for any distribution build.

**Fix:** Set to `config.developer = "auto"` or `False` before packaging.

## Medium: Empty Stub Labels
4 empty tutorial stub labels and at least 1 empty party scene stub exist in `game/script.rpy`. These are placeholders with no content.

**Impact:** If any story path routes to these labels, the game will hit an empty scene and potentially crash or hang.

## Medium: Story Flow Issues
- Some scenes are **unreachable** — no label jumps or menu choices lead to them
- Some story paths do **not rejoin** the main narrative — dead ends that don't lead to an ending
- This creates incomplete playthroughs and potential soft-locks

## Low: Dialogue Typos/Copy Errors
6 specific typos or copy errors identified in dialogue text in `game/script.rpy`. These are cosmetic but affect game quality.

## Low: Unused/Unreferenced Assets
Some assets in `game/images/` and `game/assets/` are not referenced in `game/script.rpy`. These inflate repo size without contributing to the game.

**Candidates for cleanup:** Audit image and audio references in script vs. files on disk.

## Low: Large Binary Assets in Git
All media assets (PNG, WAV, MP4, AIFF, JPG) are committed directly to the git repo. This is common for Ren'Py projects but:
- Makes the repo large
- Slows clones
- No Git LFS in use

**Recommendation:** Consider Git LFS for video files (`.mp4`) which are the largest assets.

## Info: Compiled Files Committed
`.rpyc` and `.rpyb` compiled files are committed to the repo. This is a common Ren'Py practice for projects distributed without the SDK, but it means:
- Binary diffs in git history
- Potential stale bytecode issues (see above)
- Both source and compiled versions must be kept in sync
