# Changelog

All notable changes to WR Editor Fix. Versions below v1.0.0 mean known
issues still exist (see the README's "Known issues" section) — v1.0.0 is
reserved for once everything currently known is actually fixed.

## v0.6.0 — WR loading screens, ERR_STR_INFO fix, every game build

- **New, on in the shipped `.ini`: WR loading screens (`[Editor Loading
  Screen]`).** `LaunchScreen` shows the WR screen the moment you press
  "Rockstar Editor" + Yes in FiveM's main menu: live load progress, a
  "Running now" list of what's on in your `.ini`, and the GitHub update log
  with an "Update available" box when a newer version is out. `ClipScreen`
  shows a minimal WR screen while a clip loads or an export starts. Both close
  by themselves when the editor is ready (double-click to close early) and stay
  out of the way at the main menu and on server joins. Needs the Microsoft
  Edge WebView2 Runtime (built into Windows 11, comes with Edge on Windows
  10). Tested on Windows 11; `LaunchScreen = 0` / `ClipScreen = 0` bring back
  FiveM's own screens. `UpdateCheck = 0` stops the GitHub request.
- **New, on in the shipped `.ini`: fix for `RAGE error: ERR_STR_INFO_2` and
  `ERR_STR_INFO_3` (`[Crash Fix] GrowStreamingList`).** The game keeps a fixed
  list of 32768 streaming entries; on heavy servers the world alone uses
  about 28000, so a teleport, a cutscene loading or an editor export fills
  the rest and the game stops. When the list runs full, the plugin adds more
  room instead. Works in game and in the editor. Game build b3258 only.
- **The plugin now loads on every game build FiveM supports** (b1604 to
  b3889). Before, FiveM refused to load it on b1604-b2612 and
  b3751/b3788/b3889. Only b3258 is tested; on the other builds the players are
  the testers, and parts built for b3258 still switch themselves off. The
  log's `Game build:` line names the GTA V update and how far that build is
  tested, and the README has the full table.
- The `.asi` is bigger (~1 MB): the WebView2 loader and the two screens, with
  their fonts and logo, are built in.

## v0.5.0 — Record GTA V cutscenes, free camera on blocked clips

- **New, on in the shipped `.ini`: `[Recording] AllowCutsceneRecording`.**
  The Rockstar Editor keeps recording while a real GTA V cutscene plays or
  loads. Normally the game stops recording the moment you aren't in control
  of your character, and the clip fails with "Clip must be at least longer
  than 3 seconds". The plugin changes only that one decision, so scripts that
  block recording on purpose still work. The cutscene's actors, camera and
  audio all end up in the clip. Game build b3258 only.
- **New, on in the shipped `.ini`: `[Editor Camera] FreeCameraOnBlockedClips`.**
  Clips recorded during a cutscene ("You cannot edit camera properties as this
  clip contains a blocked cutscene") and clips recorded in first person get
  a free camera in the editor: the marker's Cameras menu unlocks and the
  camera moves. Game build b3258 only.
- **Fixed** a crash when loading another clip after the first one: one of the
  plugin's own built-in guards was handed a broken pointer that looked
  valid, and the crash happened inside the guard where the safety net didn't
  look. It now returns "nothing" like the guard does for any bad pointer.
- **Fewer crashes on clips with lots of players** (more than 32,
  `cold-cardinal-mountain` and its b3095 versions): the editor no longer loops
  forever over a player slot it never filled in. The editor itself is built
  for 32 players, so very big clips can still crash later or show wrong faces.
- When the game raises its own fatal error (`RAGE error: ERR_...`), FiveM now
  reports it cleanly instead of the plugin turning it into a second crash.
- The log says which game build you're on. Parts built for b3258 switch
  themselves off on other builds.
- The shipped `.ini` now turns the **Editor Theme on** (`MenuText = FF0000`,
  `MenuTextGreyed = 8000FF`, `EditorFont = Font2_cond`). Set
  `EditorTheme = 0` and `EditorFont =` (empty) for the stock look.
- `[Stuck Downloads] SkipStuckDownloads` now ships **off**: it could release
  slow but healthy downloads on heavy servers and end in a game error.
  Turn it on only if you hit the endless "Downloading assets" hang.
- Known limit: recording doesn't continue while a script camera flies over a
  cutscene (a server's own cutscene camera tool).

## v0.4.0 — Editor Theme: your own colours and font

- **New, off by default: `[Editor Theme]`.** Recolour and re-font the
  Rockstar Editor from the `.ini`, no files replaced, nothing streamed.
- **Colours** (`EditorTheme = 1` plus `MenuText` / `MenuTextGreyed`, plain
  `RRGGBB` hex): menu labels and values, the timeline playhead, greyed-out
  rows, the timeline's played region and the second timecode. The editor
  reads these from the game's own HUD colour table; the plugin changes those
  entries only while the editor is open and restores the stock values the
  moment you leave, so the rest of the game's UI is untouched. Hot-reloads.
- **Font** (`EditorFont`): swap the editor's UI font for one of the game's
  built-in fonts - `Font5` (handwriting), `Font2_cond` (condensed),
  `RockstarTAG` (all caps, a few symbols missing), `gtaCash` (Pricedown).
  Every font the game ships was tested in-game; `Taxi_font`,
  `GTAVLeaderboard` and `FixedWidthNumbers` only contain symbols/digits and
  are listed as unusable. Works without `EditorTheme` turned on. Needs a
  relaunch. The editor's own main menu (project list) keeps the stock font
  for now. Game build b3258 only - on other builds the plugin logs that the
  font isn't supported and leaves it stock.
- The crash handler no longer tries to "rescue" faults inside FiveM's own
  startup stub pages at the very start of the game executable - those are
  passed straight on to FiveM, as they should be.
- No changes to the core crash fix or the camera features.

## v0.3.0 — duplicate-archetype crash fixed, smarter logs, cleaner config

- **Fixed the `diet-queen-carbon` / `india-connecticut-arizona` crash**
  (`GTA5_b3258.exe+4EA1E0` / `GTA5_b3095.exe+4E7BDC`). On servers with
  many duplicate/conflicting map archetypes, the editor walks a lookup
  table that was never filled in and crashed on the first read. The fix
  hands that read a real, empty table instead and lets the walk finish.
  Field-confirmed on a 60+-duplicate-archetype server where the clip had
  crashed on every attempt. The affected props may look missing in the
  editor preview only.
- **Fixed a crash our own fix could cause**: after recovering a read from
  an unloaded asset, the game occasionally divided by the value we'd just
  zeroed (`STATUS_INTEGER_DIVIDE_BY_ZERO`). Now caught and treated as 0.
- The loop breaker (which stops a genuinely stuck loop from eating all
  memory) is now also rate-based across the whole game, so multi-site
  loops get cut before they can corrupt the heap.
- **New, experimental, off by default: `[Vehicle Meta] SkipBrokenVehicleMeta`.**
  Some servers ship a vehicle with a broken `carvariations`/`handling`
  file; the game fails to read it, then loops forever the moment a clip
  using that car is added to a project ("can watch clips but not add them
  to a project", ends in "Out of game memory"). This remembers any such
  file the game reports as malformed and skips it from then on
  (`WR_BrokenVehicleMeta.txt`). Learns on first failure - the very first
  attempt on a fresh install can still crash once.
- **Logs reorganised**: everything now lands in `WR Editor Fix\Logs\`
  (that's the folder to send with a crash report). The old separate
  `WR_CameraFeatures.log` is folded into the main log as `[Camera]` lines.
  Developer diagnostics moved to an optional second config file that the
  release doesn't ship - the user config is now half the length.
- Crash-report log lines can now name the resource file being mounted when
  the crash happens during a data-file load (`... (resources:/pack/file.meta)`).
- Known issue still open: on very heavy servers, editing a clip and then
  exporting in the same session can still crash on export
  (`alabama-twenty-hawaii`); exporting an already-edited clip straight
  after launching works. Actively being investigated.

## v0.2.0 — Stuck Downloads exposed

- Exposed the experimental "Stuck Downloads" fix in the shipped config
  (`[Stuck Downloads]` section, `SkipStuckDownloads` / `SkipStuckLocalAssets`
  / `TimeoutMs`). Fixes the editor hanging forever on "Downloading assets
  (0 of N)" when a server references an asset that 404s. Off by default —
  it was built before v0.1.0 but deliberately held back from the public
  config until now; still less battle-tested than the core crash fix, so
  only turn it on if you actually hit that hang.
- Fixed a real install-layout bug: the plugin only ever looked for its
  `.ini` next to a `.asi` placed directly in `plugins\` root, with the
  `WR Editor Fix` folder as a sibling. If the `.asi` ended up placed
  *inside* that folder instead (a natural result of dragging the whole
  downloaded folder into `plugins\` as one unit), the plugin silently
  fell back to hardcoded defaults with no warning - editing the `.ini`
  appeared to do nothing. Now it checks both layouts and uses whichever
  one actually has a real `.ini` file.
- Added a permanent log line (`WR_Editor_Fix.log`) reporting which
  config file path was resolved and whether it was actually found - so
  "my settings aren't applying" is now a 2-second log check instead of
  a guessing game.
- No changes to the core crash fix or camera features from v0.1.0.

## v0.1.0 — first public release

- Core Rockstar Editor crash fix: stops the editor crashing when a clip
  references a custom asset (vehicle / MLO / prop / ytyp) that got
  unloaded, and the same crash pattern in streaming/asset-unload code.
- Editor free camera tweaks, on by default: unlimited camera distance,
  uncapped zoom/FOV, no camera collision, adjustable free-cam move speed
  (live-reloads from the `.ini` while flying).
- Known issue: a crash tied to malformed custom vehicle data on some
  heavily modded servers is not yet fixed — actively being investigated.
