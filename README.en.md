# YaChanger 0.7

Read exact player coordinates from I Wanna Maker and find jump sequences that reach a target **ya**, the fractional part of Y.

## Start

Extract the entire Windows portable ZIP before running `YaChanger.exe`. Keep `_internal` next to the executable. Run `YaChanger-English.cmd`, launch `YaChanger.exe --lang en`, or choose **English** in the header. You can switch languages without losing the captured origin or selected solution.

1. Open a level in I Wanna Maker. Stand still on ordinary static block ground and release movement/jump keys.
2. Click **Capture position**. Capture again after moving, respawning or changing rooms.
3. Enter target ya and click **Analyze**. The target starts blank each time. Current ya, last-digit adjustments and target history are available.
4. Select a solution to inspect, copy or export it while the search continues. A manually selected solution stays selected as new results arrive.
5. Follow the instructions. **Only stable landing Y values appear in the instructions.** Airborne Y, including its changing integer part, remains available in Trajectory and Input details.
6. Click **Stop** to keep the displayed results. You can immediately enter another target and start again.

The tool only reads game memory. It does not remap keys, send inputs, write memory or change saves. Offline demos are explicitly marked and do not replace live coordinates.

## Multiple releases

If your remapping software maps several physical keys independently to jump, holding them together and releasing them separately may trigger repeated jump cancellation. Each release during ascent applies the release factor again before native gravity, float32 position storage and collision.

- A/B/C/D in instructions mean your remapped jump keys, not literal letter keys.
- `2f+2` uses jtool counting for the first release. It means hold A and B for one kernel frame, release A on the next frame, then release B two frames later.
- The reference solver's default **0f** notation calls this `1+2`. `+N` is the interval between releases, not another jump.
- For origin `Y=309.399993896484375`, this model predicts stable landing `Y=309.327239990234375`.
- Two to four mapped keys, air jumps and combinations across landings are supported. Releasing an extra key is not treated as another press or another game jump.

The event model has been checked using independent speed formulas and scalar/vector native replay. Real remapping hardware/software sequences have **not** been certified in-game. Compare your stable landing Y against the prediction.

## Filters and ranking

Ground-jump and air-jump frame checkboxes are independent. Counts use jtool conventions. For multiple releases, they filter the first release count before `+`. Full jumps are measured from the actual ascent.

Use the reference-0f pattern selector for preferences such as `4+4` (displayed as jtool `5f+4`). Choose **Prioritize**, **Allow only**, or **Exclude**. Adding a priority again moves it to the front. Allow/exclude rules apply to every multiple-release jump in a solution; ordinary jumps remain available. Priorities follow the order shown in the list.

The main sort applies immediately to solutions already found:

- **Recommended:** by default, ordinary jumps first, then fewer jumps. Among multiple-release solutions with the same jump count, shorter first holds come first, so `1+2` or `1+3` precede `16+2`. You can choose multiple releases first, balanced error/count scoring, fewer mapped keys, or accuracy as the cancellation preference.
- **Best accuracy:** smallest target error, then fewer jumps.
- **Fewest jumps:** fewest game jumps, then smallest error.

Custom pattern priorities and cancellation preferences apply to Recommended. Explicit accuracy/fewest modes retain their stated primary metric. Air jumps normally need at least 70% fewer game jumps than the known shortest ground-only solution to enter the recommended group. Changing feasibility rules stops the old search; changing ranking does not.

## Tolerance

Automatic absolute tolerance is one unit of the final entered decimal place: `0.43` allows ±`0.01`; `0.3912` allows ±`0.0001`. Trailing zeros matter. You can set a custom tolerance, including zero, and accept either side, only at/above, or only at/below the target. ya errors do not wrap around between 0 and 1. Up to 24 decimal places are accepted. Full-Y matching is also available.

## Responsiveness

There is no total game-frame, elapsed-time or landing-round limit. Each search runs in its own lower-priority process. Stop retains the last displayed results and reclaims the old process and caches in the background.

By default, after 500 matches the search continues at a nominal **15% work/rest duty cycle**, with less frequent UI updates. Adjust the threshold and choose 5%, 15% or 30%. This is not a promise of a particular Task Manager CPU percentage. The default 500-result list capacity is independent of the background threshold.

Native batch simulation and complete grounded-state caching share physical transitions while retaining different input sequences. A bounded A* working frontier prevents exponential path-queue growth; when it fills, lower estimated-cost paths are retained. The tool does not guarantee exhaustive enumeration or prove a target impossible. Stopping a search does not imply no solution exists.

Long instruction lists show 24 cards per page; use the bottom ‹/› controls to change pages. Long trajectory verification runs in the background and can be cancelled by selecting another solution or starting a new search.

Supports in-place adjustment on ordinary static block ground. Unsupported nearby mechanics are rejected. Original supplied iwbot sources and DLLs are unchanged.

## Shortcuts, export and updates

F6 captures, F7 starts/stops, F8 copies, Escape stops. Shortcuts apply while the tool has focus. Settings are stored in portable `preferences.json`; disable Remember settings or use Reset if needed. Target history never auto-fills the startup target.

JSON uses `yachanger-recipe/2`, input encoding `held-release-press/v2`: bit 0 held, bit 1 independent release, bit 2 same-frame press/release event. It preserves raw trajectories, metadata, alternatives, tolerance and ranking. `show_coordinate` identifies landing rows. English exports contain English player instructions; event encoding and numerical results are identical in both languages. Old 0/1-only readers cannot interpret multiple releases correctly.

Stable releases are checked in the background through [GitHub Releases](https://github.com/frredomerror91-netizen/YaChanger/releases). Updates open a download page; nothing is installed silently. Offline/network errors do not block local use. Errors are written to `logs/app.log`.

For source development, use 64-bit Python 3.12+ with tkinter, install `requirements.txt`, retain the required iwbot runtime files, and run `python -m yachanger --lang en`. Run `python -X utf8 -m unittest discover -s tests -q`, `python -X utf8 tools/ui_smoke.py`, and `python -m yachanger --self-test` to verify. Build via `python -X utf8 tools/release.py`. Version 0.4 remains withheld from publication.
