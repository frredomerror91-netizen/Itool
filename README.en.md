# Itool 1.0.1

Itool (formerly YaChanger) reads precise player coordinates and finds ya jump recipes. Select **Choose process…** after starting your game; filter by executable name or PID, select the correct instance and click **Connect game**. The default `auto` core recognizes supported IWM, GMS1 VM and calibrated GM8.1 builds. Manual `iwm`, `gms` and `gm8` choices are retained; mismatched choices are rejected. A closed/reused PID requires a fresh selection.

New: tuhkakuppi ver5.2 **GM8 and GMS executables**, original icon, Light/Dark/System themes, persistent theme preference and animated tab/selection feedback. The GM8 model preserves float64 position and speed; GMS preserves float32. Full-Y matching automatically uses the selected model's precision.

Compatibility covers ordinary positive-gravity players on stationary rectangular floors with a clear vertical jump corridor, `Collision` block timing (`stepBlock=0`) and, for GMS, rectangular masks (`preciseMask=0`). Current mode is read from the game. Uncalibrated builds, alternate collision timing, water, vines, platforms, ceilings, hazards, Dotkid and unusual transforms do not silently inherit an approximate model. Coordinates remain recorded when a pose cannot seed the solver. Model/replay checks do not imply every hardware input combination has been tested in-game.

Extract **Itool-v1.0.1-win64.zip**, then run **Itool.exe** or **Itool-English.cmd** with `_internal` beside it. Capture the starting position (also while paused), enter target ya, then Analyze. The default automatic stop is 100 solutions; 0 means manual stopping. Sorting applies immediately; filters and tolerance change the search conditions. Each jump shows its stable full landing Y. Land between successive ground jumps. Multiple releases use unified notation such as `1+3`.

The repository remains private under its existing name. The user explicitly resumed publication for v1.0; this does not change repository visibility. Public update checks cannot authenticate to a private repository: sign in to [Releases](https://github.com/frredomerror91-netizen/YaChanger/releases) to download. No token is included in the program.

## Controls and development

Ground jumps offer 1–23f and Full; air jumps offer 1–19f and Full. Default tolerance is one unit of the target decimal's last place. Accuracy, fewest-jumps and recommended ranking update immediately. Ground/air frame filters and preferred/allowed/excluded multiple-release patterns are independent.

Default retention is 500 solutions; after disabling automatic stopping, searching slows after 500 matches. F6 captures, F7 starts/stops and F8 copies while the tool has focus. JSON retains yachanger-recipe/2 and held-release-press/v2, with numeric_model identifying the physical model.

The window is 1180×780, minimum 1060×700. The System theme is read on startup or when reselected. Animations respect reduced motion and can be disabled. Source launch remains python -m yachanger for compatibility. Build with python -X utf8 tools/release.py; publication uses --publish and optionally --reuse-build. No game files or credentials are distributed.

94 unit tests, bilingual small-window checks, real GM8/GMS coordinate capture, and ordinary/air/multiple-release model replays passed. Every hardware key combination has not been individually tested in the new engines. Runtime inspection is read-only; the game and original iwbot files are unchanged.
