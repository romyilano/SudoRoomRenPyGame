# Testing

## Testing Approach
**No automated test framework detected.** There are no test files, no jest/pytest/vitest config, and no CI pipeline configuration in the repository.

QA is entirely **manual / playthrough-based** — the developer runs the game and plays through scenes to validate behavior.

## Ren'Py Built-in Error Reporting
- `errors.txt` — Ren'Py writes parse/runtime errors here automatically on game load failure
- `game/bytecode.rpyb` — compiled bytecode cache; stale bytecode can cause issues after script changes
- The in-game **developer console** (backtick key) enables:
  - Jumping to labels
  - Inspecting variables
  - Testing individual scenes without full playthrough

## Developer Mode
- `config.developer = True` in `game/options.rpy` enables:
  - Developer console
  - Shift+D debug overlay
  - Reload on file change (Shift+R)
- This should be set to `False` or `config.developer = "auto"` for distribution builds

## Known Broken State (from errors.txt)
- Hyphenated label names (e.g., `label art-murmur:`) caused **Ren'Py parse errors** that broke game loading
- These are a critical class of bug — Ren'Py does not support hyphens in label identifiers
- Fix: rename all hyphenated labels to `snake_case`

## Recommended QA Checklist
Since there's no automated testing, manual QA should cover:
- [ ] Game launches without parse errors (check `errors.txt` is empty after launch)
- [ ] `label start:` executes and first scene loads
- [ ] All scene transitions work (no missing background images)
- [ ] All character sprites display correctly (no missing sprite errors)
- [ ] Audio plays in scenes with music/sound effects
- [ ] Video assets play in scenes using `movie` directive
- [ ] All `menu:` choices lead to valid labels
- [ ] Game reaches an end state (no infinite loop or dead-end labels)
- [ ] No missing image/audio errors in developer console

## Asset Validation
- Missing assets produce pink/error sprites in Ren'Py — visually obvious during playthrough
- Audio errors are logged but may not visually break game flow
- All assets (PNG, WAV, MP4, AIFF) are committed to the repo, so asset availability is tied to git checkout state
