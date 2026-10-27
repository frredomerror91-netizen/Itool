# YaChanger 0.8

Read exact player coordinates from I Wanna Maker and find jump sequences that reach a target **ya**, the fractional part of Y.

## Start

Extract the entire Windows portable ZIP before running `YaChanger.exe`. Keep `_internal` next to the executable. Run `YaChanger-English.cmd`, launch `YaChanger.exe --lang en`, or choose **English** in the header. You can switch languages without losing the captured origin or selected solution.

1. Open a level in I Wanna Maker. Stand still on ordinary static block ground and release movement/jump keys.
2. Click **Capture position**. Capture again after moving, respawning or changing rooms.
3. Enter target ya and click **Analyze**. The target starts blank each time. Current ya, last-digit adjustments and target history are available.
4. Select a solution to inspect, copy or export it while the search continues. A manually selected solution stays selected as new results arrive.
5. Follow the instructions. **Only stable landing Y values appear in the instructions.** Airborne Y, including its changing integer part, remains available in Trajectory and Input details.
6. By default, analysis stops automatically after **100 distinct input solutions**. Set **Stop after solutions** to another number, or 0 to stop manually. You can also click Stop at any time and immediately start another target.

Before connecting to the game, Current ya displays the default `0.399993896484375`; full X/Y remain unavailable. This is a display default, not a fabricated live sample or captured origin.

The tool only reads game memory. It does not remap keys, send inputs, write memory or change saves. Offline demos are explicitly marked and do not replace live coordinates.

## Multiple releases

If your remapping software maps several physical keys independently to jump, holding them together and releasing them separately may trigger repeated jump cancellation. Each release during ascent applies the release factor again before native gravity, float32 position storage and collision.

- A/B/C/D in instructions mean your remapped jump keys, not literal letter keys.
- `2+2` uses jtool counting for the first release. All filters, priorities, solutions and copied instructions now use this same `X+N` notation without an f suffix. It means hold A and B for one kernel frame, release A on the next frame, then release B two frames later.
- `1+4` is the same-frame first press/release followed by another release four frames later. The old sidebar called it `0+4`. Old preferences are migrated by adding 1 to the first number, preserving the physical input (old `4+4` becomes `5+4`). New choices are shown identically on both sides. `+N` is the interval between releases, not another jump. Legacy 0f notation remains only in compatibility metadata.
- For origin `Y=309.399993896484375`, this model predicts stable landing `Y=309.327239990234375`.
- Two to four mapped keys, air jumps and combinations across landings are supported. Releasing an extra key is not treated as another press or another game jump.

The event model has been checked using independent speed formulas and scalar/vector native replay. Real remapping hardware/software sequences have **not** been certified in-game. Compare your stable landing Y against the prediction.

## Filters and ranking

Ground-jump options are 1–23f plus Full; air-jump options are 1–19f plus Full. The two sets are independent. Counts use jtool conventions. For multiple releases, they filter the first release count before `+`. Full jumps are measured from the actual ascent.

Use the unified pattern selector for preferences such as `4+4`, which is also displayed as `4+4` in solutions. Choose **Prioritize**, **Allow only**, or **Exclude**. Adding a priority again moves it to the front. Allow/exclude rules apply to every multiple-release jump in a solution; ordinary jumps remain available. Priorities follow the order shown in the list.

The main sort applies immediately to solutions already found:

- **Recommended:** by default, ordinary jumps first, then fewer jumps. Among multiple-release solutions with the same jump count, shorter first holds come first, so `1+2` or `1+3` precede `16+2`. You can choose multiple releases first, balanced error/count scoring, fewer mapped keys, or accuracy as the cancellation preference.
- **Best accuracy:** smallest target error, then fewer jumps.
- **Fewest jumps:** fewest game jumps, then smallest error.

Custom pattern priorities and cancellation preferences apply to Recommended. Explicit accuracy/fewest modes retain their stated primary metric. Air jumps normally need at least 70% fewer game jumps than the known shortest ground-only solution to enter the recommended group. Changing feasibility rules stops the old search; changing ranking does not.

## Tolerance

Automatic absolute tolerance is one unit of the final entered decimal place: `0.43` allows ±`0.01`; `0.3912` allows ±`0.0001`. Trailing zeros matter. You can set a custom tolerance, including zero, and accept either side, only at/above, or only at/below the target. ya errors do not wrap around between 0 and 1. Up to 24 decimal places are accepted. Full-Y matching is also available.

## Responsiveness

There is no total game-frame, elapsed-time or landing-round limit. A separate automatic stop defaults to 100 distinct solutions; set it to 0 for continuous manual-stop analysis. Each search runs in its own lower-priority process. Stop retains the last displayed results and reclaims the old process and caches in the background.

If automatic stop is disabled or set above 500, after 500 matches the search continues at a nominal **15% work/rest duty cycle**, with less frequent UI updates. Adjust the threshold and choose 5%, 15% or 30%. This is not a promise of a particular Task Manager CPU percentage. The default 500-result list capacity, 500-match background threshold and 100-solution automatic stop are independent.

Native batch simulation and complete grounded-state caching share physical transitions while retaining different input sequences. A bounded A* working frontier prevents exponential path-queue growth; when it fills, lower estimated-cost paths are retained. The tool does not guarantee exhaustive enumeration or prove a target impossible. Stopping a search does not imply no solution exists.

Multiple-release instructions show the compact pattern (such as `1+3`) and landing Y instead of frame-by-frame descriptions. Necessary air-jump timing is retained. Long instruction lists show 24 cards per page; use the bottom ‹/› controls to change pages. Long trajectory verification runs in the background and can be cancelled by selecting another solution or starting a new search.

Supports in-place adjustment on ordinary static block ground. Unsupported nearby mechanics are rejected. Original supplied iwbot sources and DLLs are unchanged.

The compact window starts at 1180×780 and supports 1060×700. Selected options fill the entire button; no x/check glyph is used. Hover, press and selection states use short nonblocking color transitions. Disable **Interaction animations** to remove them; the Windows client-area animation preference is respected.

## Shortcuts, export and updates

F6 captures, F7 starts/stops, F8 copies, Escape stops. Shortcuts apply while the tool has focus. Settings are stored in portable `preferences.json`; disable Remember settings or use Reset if needed. Target history never auto-fills the startup target.

JSON uses `yachanger-recipe/2`, input encoding `held-release-press/v2`: bit 0 held, bit 1 independent release, bit 2 same-frame press/release event. It preserves raw trajectories, event checkpoints, metadata, alternatives, tolerance and ranking. `jtool-multi/v1` identifies unified pattern naming, and `stop_reason` records automatic or manual stopping. `show_coordinate` identifies landing rows. English exports contain English player instructions; event encoding and numerical results are identical in both languages. Old 0/1-only readers cannot interpret multiple releases correctly.

Stable releases are checked in the background through [GitHub Releases](https://github.com/frredomerror91-netizen/YaChanger/releases). Updates open a download page; nothing is installed silently. Offline/network errors do not block local use. Errors are written to `logs/app.log`.

For source development, use 64-bit Python 3.12+ with tkinter, install `requirements.txt`, retain the required iwbot runtime files, and run `python -m yachanger --lang en`. Console solvers default to 100 solutions too; use `--stop-after 0` for manual stopping. Run `python -X utf8 -m unittest discover -s tests -q`, `python -X utf8 tools/ui_smoke.py`, and `python -m yachanger --self-test` to verify. Build via `python -X utf8 tools/release.py`. Version 0.4 remains withheld from publication.
