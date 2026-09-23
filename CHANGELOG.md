# Changelog

All notable changes to WR Editor Fix. Versions below v1.0.0 mean known
issues still exist (see the README's "Known issues" section) — v1.0.0 is
reserved for once everything currently known is actually fixed.

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
