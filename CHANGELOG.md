# Changelog

All notable changes to WR Editor Fix. Versions below v1.0.0 mean known
issues still exist (see the README's "Known issues" section) — v1.0.0 is
reserved for once everything currently known is actually fixed.

## v0.9.0 — WR Automate + WR Garage, Neon editor, WR blend + shake

- **New: WR Options, the editor's own WR page** (the last marker menu row):
  time + weather, Camera Speed, Header Style / Motion, Font, Colors, WR Garage,
  Director Mode, WR Automate and Clear Timeline. Game build b3258.
- **New: WR Automate - the editor builds the camera edit for you.** WR Options
  -> WR Automate: pick what to follow (the player's car or the player), the
  length, how many markers, the style (Mixed / Orbit / Chase) and the shake,
  then Automate. The timeline starts fresh, the clip is scouted, and it places
  its own free-camera markers in a ring of cinematic shots around the car - WR
  blend and a shake on every one, the car centred on screen the whole time.
  Then it runs the clip again with the game's own camera collision test and
  moves any camera that would touch or look through a car, ped, prop or wall.
  Everything stays editable. New `[WR Automate]` section.
- **New: WR Options -> Clear Timeline** (Enter twice): the clip back to a fresh
  one - every marker gone, the default start and end markers, every setting
  default. No undo.
- **New: WR Garage - tune the car inside the editor.** Livery, Primary /
  Secondary paint, Finish (Normal to Chrome), Neon, Xenon colour, Lights, Window
  Tint, Plate Text (the game's own keyboard, up to 8 characters), Plate Style,
  Body Parts (every part slot the car has, wheel type and rims), Randomise
  Colors / All / Parts, Clean and Reset - live, on the car the recorded player
  drives. **Per marker:** Cameras -> WR Marker Options -> Car Look gives a
  marker its own car look: from that marker on, the car wears it until the next
  one. Works in the export. Not saved with the project yet.
- **New: WR blend.** Cameras -> Blend -> WR: the camera passes every marker
  exactly on time with the speed flowing through them (position, rotation and
  zoom) instead of the stock Smooth's spring that always lags behind. The
  export matches the preview. Free-camera markers.
- **New: WR shake.** Cameras -> Shake -> WR: Handheld, Walk, Run, Car,
  Helicopter, Earthquake (each its own motion) and Custom, with Strength and
  Speed. Fades into the next marker's shake, same in the export.
- **New: WR blend + WR shake are saved with your project**
  (`WR Editor Fix\Projects\<project name>.json`), and come back when the
  project opens. Moving or deleting other clips doesn't move them.
- **New: time + weather per marker.** Cameras -> WR Marker Options -> Time &
  Weather: from that marker on, the clip plays with its own time and weather.
  Cut switches at the marker, Smooth changes toward it (a time-lapse). Works in
  the export. Not saved with the project.
- **New, first version: Director Mode.** WR Options -> Director Mode -> START:
  the clip plays and you fly the camera (controller, or mouse + keyboard), and
  the take becomes markers - the fewest that still reproduce your move. Look
  Assist keeps the car centred, Follow rides along with it, Record Speed lets
  you fly in slow motion. No obstacle checks on a take yet.
- **New: the editor's look - `[Editor Look]` replaces `[Editor Theme]`.**
  `Theme = Neon` (on in the shipped `.ini`) gives the clip edit screen the WR
  Neon Glass look: frosted glass menu, neon pill on the selected row, a glass
  panel for the time and the playback buttons, a slim timeline with a glowing
  playhead and diamond markers - drawn by the game itself. 10 built-in fonts
  (Chakra Petch, Spicy Rice, Bagel Fat One, Oswald, Carter One, Ubuntu Mono,
  Permanent Marker, Germania One, Kavoon, Sriracha) or the original one, every
  editor colour from a palette (WR Options -> Colors), and header art at the top
  of the menu (Stock, WR, Meme, Retro, Cinematic, animated or still). Font,
  Colors, Header and Camera Speed change live in WR Options and are saved back
  to the `.ini`. `EditorTheme`, `EditorFont` and the GTA font list are gone -
  take the new `.ini`.
- **New: WR Options -> Camera Speed** (x0.25 to x20), live, saved back to the
  `.ini`.
- **Fixed: WR Options missing from the first marker menu after a launch.**
- **Fixed (guard): a crash while moving or editing a marker camera on some
  clips with add-on cars** (a call to 0 at `+176B0BB`,
  `ERR_MEM_EMBEDDEDALLOC_GUARD_1`): removed parts are cut from the car's parts
  lists before the game touches them. It came back once more on the same clip,
  so it's still being worked on.
- **Changed: the loading screens' tips** point at the new features, and the launch screen's
  "Running now" list shows them from your `.ini` (No seek freeze, WR Automate, Editor theme / header /
  font).
- **New: a `Guides` folder** - a step-by-step guide for every feature (WR Options, WR Automate, WR
  Garage, Car Look, WR blend + shake, time + weather, Director Mode, the editor look, the free camera, the
  loading screens, crash fixes and reports).
- The `.asi` is about 7.8 MB now (the editor art and fonts are built in).

## v0.8.0 — Time + weather in the editor, no seek freeze, other fixes

- **New: change the time of day and the weather of any clip, right in the
  editor.** Marker menu -> **WR Options** (Enter) -> Hour / Minute / Weather /
  Default. Every GTA weather (Extra Sunny to Halloween, snow included) and any
  minute of the day. It changes live in the preview, the lighting follows, and
  the export renders exactly what you see. **Default** puts it back to the
  time and weather the clip was recorded with. Your pick stays for every clip
  until you press Default or restart FiveM (it isn't saved with the project
  yet). Nothing is written into your clips. New `[Editor Time Weather]`
  section, on by default. Game build b3258.
- **New: no more freeze after every seek, cut or marker move.** The editor
  waited until the whole game had finished streaming before it played on. On
  a busy server that never happens, so it sat there for about 7 seconds every
  time. New `[Editor Playback] NoSeekStall` (on by default) waits at most
  `NoSeekStallWaitMs` (default 100 ms); anything still loading pops in a
  moment later. Exports keep the full wait, so your video is fully loaded.
  Game build b3258.
- **Improved: `DisableCameraCollision` now really means no collision.** It
  only switched off the free camera's world collision before. Three more
  checks still pushed the camera: the shove off the car or ped it's attached
  to or looking at (the "Unable to apply camera blend due to object
  collision." message and its jump), world collision for an attached camera,
  and the check that cut marker blends short. All of them follow the switch
  now.
- **Fixed: `RAGE error: ERR_GEN_MAP` when an export starts on a heavy
  server.** The game's list of things waiting to load ran full during the
  export's reload. `[Crash Fix] GrowStreamingList` now adds room to that list
  too, the same way it does for ERR_STR_INFO_2 / _3. Built from a real crash;
  it hasn't come back since, but it hasn't been forced to happen again either.
- **Changed: `[Stuck Downloads] SkipStuckDownloads` only acts inside the
  Rockstar Editor** (editing or exporting). While you play on a server it only
  reports, so you no longer have to turn it off before you play. Still off by
  default. New: when streaming hasn't moved for 20 seconds, the log names the
  files that are still loading.
- **Changed: Rockstar Editor+ (RE+).** If RE+ is installed with its own
  camera distance, zoom or fast precache switched on, WR Editor Fix leaves
  that part to RE+ (one line in the log says so), so the two don't fight over
  it. RE+ itself is not supported and won't be (the README explains why):
  WR Editor Fix does these jobs itself.

## v0.7.0 — NVE support + NVE ReShade .addon fix, other fixes

- **Fixed: "FiveM has stopped responding" when an EVE export starts with NVE
  (NaturalVision Evolved).** When an export starts, the video encoder sets up
  and cleans up a temporary graphics device. With NVE.asi loaded, NVE and
  ReShade then waited on each other forever. New
  `[Crash Fix] NveExportFreezeFix` (on by default, only active while NVE.asi
  is loaded) makes that setup and cleanup happen in the same order ReShade
  uses. NVE itself isn't changed.
- **Fixed: NVE's ReShade .addon file crashed the game a few seconds after
  launch with EVE** (`ReshadeEffectShaderToggler.addon64`,
  `d3d11.dll+5BFEC`). EVE creates a throw-away swap chain to find ReShade's
  Present. ReShade built and dropped a whole second effects runtime for it,
  and the .addon freed textures the game's own runtime still used. New
  `[Crash Fix] EveSwapChainFix` (on by default, only active with EVE +
  ReShade): EVE's request gets the game's own swap chain instead, so EVE hooks
  the same Present as before (your ReShade / NVE look is still in the export)
  and the second runtime is never built. EVE, ReShade, NVE and the .addon
  aren't changed.
- **New: WR Editor Fix shows up in ReShade's Add-ons section** (Home key ->
  Add-ons) whenever EVE and ReShade are loaded. That's how it knows the
  game's swap chain for the fix above - leave it ticked there.
- **Fixed: crash after an export or when leaving the export screen**
  (`GTA5_b3258.exe+373EA6`, `+3E541F`, `+12E4D71` / `floor-north-enemy`). A
  replay object kept an entity that had already been removed from the world.
  The plugin now keeps that entity out of the list and treats its leftover
  data as empty.
- **Fixed: crash when an export loads a clip with an item that has no name**
  (`arizona-beryllium-river`, `GTA5_b3258.exe+184C8B7`). New `[Crash Fix]
  EmptyNameLookupFix` (on by default, game build b3258): only that one lookup
  is allowed to carry on as "no match" - anything else still stops exactly
  as before.
- **Fixed: the safety net could stop a working export**
  (`berlin-golf-wyoming`, `+F51C16`). It counted recoveries until a pause
  instead of per second, so a steady trickle (a vehicle whose model data the
  export's reload had freed) tripped it after about 40 seconds. It now
  measures a real rate.
- Tested with full NVE (incl. its ReShade .addon) + EVE + Voukoder on
  a server: several sessions of 4 exports in a row with no crash or freeze.
- Still known: opening a project and then exporting can crash on some clips
  (the clip loads twice) - being worked on.

## v0.6.2 — Hotfix for the new FiveM update

- **Fixed: `[Vehicle Meta] SkipBrokenVehicleMeta` switched itself off on the
  new FiveM.** FiveM's update of 19 October 2026 moved the spot this feature
  hooks into, so on v0.6.1 the log said "VarHook ... Declining to install" and
  clips with a broken `vehicles.meta` / `carvariations.meta` froze on
  "Preparing clip" ("FiveM has stopped responding") again. The plugin now
  finds that spot by itself on any FiveM version. Confirmed by a tester on a
  real server: the broken car files are skipped and the clip loads.
- Nothing else changed since v0.6.1.

## v0.6.1 — Broken-ped crashes fixed, broken-asset report

- **New, on by default: broken-asset report (`[Stuck Downloads]
  ReportStuckDownloads = 1`).** Server downloads that never finish are listed
  in `WR_BrokenAssets.log` (resource + file) - a plain list to send to your
  server owner. It only lists them, nothing is skipped, so it's safe while you
  play. `SkipStuckDownloads` (the actual skipper) stays off and editor-only.
- **Fixed: freeze when moving the editor camera near a ped whose body never
  loaded** ("FiveM has stopped responding"). The game walked that ped's
  missing skeleton forever; the plugin now stops the walk and skips the ped's
  bones. Seen in the tester's logs. In rare cases that clip can still crash a
  bit later on the same ped - the last step is being tested.
- **Fixed: crash loading a second clip right after the first**
  (`music-arkansas-vermont`, b3407). The editor looped over a table that was
  already gone and the safety net had to give up; the plugin now finishes
  that loop as "nothing found". Matched by the game's code (b3258, b3095,
  b3407).
- **README:** new sections "Broken files on the server - I can't fix those"
  (broken server assets / scripts are the server owner's job) and "Windows
  Defender says Trojan / malware?" (known false positive, being worked on,
  how to restore / allow / Unblock).
- The `.asi` now carries Windows version info (Properties -> Details).
- **Fixed: crash when a clip dresses a ped that was never loaded**
  (`king-yankee-east`, then `social-nuts-colorado`, `fifteen-princess-double`,
  `thirteen-johnny-low`, `saturn-robert-lactose` on the same clip). One ped
  with a custom hands/body model never loaded; the editor still wrote its
  clothing, asked about it thousands of times a second and saved it, all into
  nothing. The plugin now skips that ped's look and answers "nothing here"
  for it in each of those places. The clip loads, the free camera, editing
  and F5 save all work. Matched by the game's code, not by address.
  Confirmed by the tester (Reni).
- Known issue: opening a project and then exporting can crash on some clips
  (the clip loads twice). Being worked on for v0.7.0.

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
