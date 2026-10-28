# Itool 1.3

Extract the Windows archive and run **Itool.exe**. Keep `_internal` beside it. Choose a language on first launch, or change it from the top bar. English and Japanese launchers are included.

Supported: the adapted I Wanna Maker build, jtool 1.3.6 GMS1 VM, and tuhkakuppi 5.2 GM8.1/GMS support coordinates, ordinary-floor ya solving and step checks. Standard 32-bit GMS1 VM I-wanna games, including I wanna Lap Around 1.1, also support ordinary-floor solving after passing the app's compatibility checks, including integer-scaled rectangular blocks. Custom physics/scripts, generic GMS2, other YYC/64-bit games and uncalibrated GM8 builds are not guaranteed. Follow the message shown after capturing your position.

Start your game and enter a level. Itool selects one detected game automatically or asks you to choose between multiple candidates. You can also use **Choose process…**. The active engine appears beside the feature tabs.

Stand still on an ordinary floor, **Capture position**, enter **Target ya**, and **Analyze**. Select a solution and follow its steps. After each jump, stand still: matching landing ya turns the step green and advances the view; a mismatch turns it red. After R, a respawn at a completed landing preserves that green prefix and continues with the next step; returning to the initial position starts over. Wait for the character to settle. For repeated completed landing values, the latest matching step is used. **Start over** clears progress manually. Recapture after changing to a position outside the plan or another level. This checks landing values, not the entire input sequence.

Without a connected game, entering a target automatically uses offline solving from Y=309.399993896484375. Offline solutions do not mark live steps complete.

`4f` uses jtool frame counting; land between ground jumps. `1+3` means the first cancellation at the displayed count, followed by another mapped-key release 3 frames later. Prepare multiple mapped jump keys before using these solutions. Air-jump steps specify airborne waiting.

Ground/air frame filters are separate. Choose preferred/allowed/excluded multi-release patterns, error tolerance and direction, and immediate ranking. The default auto-stop is 100 solutions; 0 means manual stopping. Wheel input scrolls settings without editing them. Stop to change your target. Water, vines, moving platforms, special gravity/masks, ceilings and hazards may be unsupported; follow the app's message.
For recognized stationary blocks or spikes overhead in standard GMS games, only jumps that stay clear are listed; unsafe air jumps may be excluded.

Copy coordinates, copy a selected solution or export it. F6 captures, F7 analyzes/stops, F8 copies while Itool has focus. Themes, language and always-on-top are at the top. The map solver tab is still in development.
Open the Acknowledgements tab to view contributors and their support.
