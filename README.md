# WR Editor Fix

**Version: v0.9.0**

Discord: https://discord.com/invite/FKJ27bhqfJ  |  YouTube: https://www.youtube.com/@Warraa__

![The WR loading screen shown while the Rockstar Editor opens](.github/media/loadscreen.gif)

A FiveM `.asi` plugin that fixes the Rockstar Editor crashing when a clip
references a custom asset (vehicle / MLO / prop / ytyp) that got unloaded,
plus editor tools: a free camera without limits, time + weather per clip and
per marker, WR loading screens, recording real GTA V cutscenes, fixes for
clips with a player whose body never loaded, a list of broken server files you
can send to your server owner, and NVE (NaturalVision Evolved) + EVE
(ExtendedVideoExport) support.

**New in v0.9.0:** WR Automate builds the camera edit for you, WR Garage tunes
the car (for the whole clip or per marker), WR blend and WR shake give marker
cameras smooth on-time paths and real handheld shake (saved with your
project), time + weather per marker, the WR Neon editor theme with 10 fonts
and live colours, and Director Mode - fly the camera live and the take becomes
markers (first version).

## ⚠️ Important — read before you install

**This does not remove 100% of Rockstar Editor crashes.** It fixes the most
common crashes found and confirmed so far. There are almost certainly other
crashes out there that haven't been found yet, or that have been found but
don't have a safe fix yet (see "Known issues" below). Installing this
should mean you crash a lot less, not that you'll never crash again.

**Not every fix applies to every server.** Most of these crashes are caused
by a specific server's custom assets — a duplicated map archetype, a
malformed vehicle file, a broken clothing model. The fix for one server's
crash often does nothing for another server's, because it's a different
broken file on a different code path. That's why this gets built crash by
crash, from real logs and dumps, rather than one blanket "fix everything"
switch. If your server hasn't had its crash looked at yet, it may still
crash exactly as before.

**Tested on game build b3258.** Everything in this plugin was built and
tested on FiveM's game build **b3258** (Legacy). The plugin knows and loads on every
game build FiveM supports (table below) and the log names yours, but only b3258 is
tested. On the others, **you are the tester**: it may work, some fixes may
not apply (the game's code sits at different places), and parts built for
b3258 switch themselves off. If you're on another build, your logs and crash
dumps are what gets it working there — see **"Found a new crash?"** below.

Your game build is the number in the crash window (`GTA5_b3258.exe`) or the
`Game build:` line near the top of `WR_Editor_Fix.log`.

**Feature by feature** - what's supported, what's tested (Windows 10, AMD,
add-on cars, the stock export, controllers ...) and what isn't yet:
[Guides/00 - Support and Testing](Guides/00%20-%20Support%20and%20Testing.md).

| Build | GTA V update | Status |
|---|---|---|
| b1604 | Arena War | community testing |
| b2060 | Los Santos Summer Special | community testing |
| b2189 | Cayo Perico Heist | community testing |
| b2372 | Los Santos Tuners | community testing |
| b2545 | The Contract | community testing |
| b2612 | The Contract (mpg9ec) | community testing |
| b2699 | The Criminal Enterprises | community testing |
| b2802 | Los Santos Drug Wars | community testing |
| b2944 | San Andreas Mercenaries | community testing |
| b3095 | The Chop Shop | partly checked (one editor session) |
| **b3258** | **Bottom Dollar Bounties** | **tested** |
| b3323 | title update after Bottom Dollar Bounties | community testing |
| b3407 | Agents of Sabotage | community testing |
| b3570 | Money Fronts | community testing |
| b3751 | A Safehouse in the Hills | community testing |
| b3788 | 2026 patch 1 | community testing |
| b3889 | The Kortz Center Heist | community testing |

Good to know: on servers running current FiveM, a build **lower** than b3258
(for example `sv_enforceGameBuild 3095`) still runs the **b3258 game exe**
with that build's content, so everything here applies as on b3258. Only
servers on old FiveM versions put you on the real older exe. Builds
**higher** than b3258 always run their own exe. GTA V Enhanced is not
supported.

If you hit a crash this doesn't catch, see **"Found a new crash?"** near the
bottom — I do want to know about it and will try to fix it.

## What it fixes

The Rockstar Editor crashes when it tries to read a custom asset that's
already been unloaded from memory (a freed pointer read). This plugin
catches that specific crash pattern safely and lets the editor keep running
instead of closing. A prevented crash may make a custom prop look missing
in the editor **preview only** — your recorded clips and exports are
unaffected.

## Guides - how every feature works

Step-by-step guides for every feature - where to find it, every row, tips and
limits - are in the `Guides` folder (in the release zip, and here on GitHub):

| Guide | What's in it |
|---|---|
| [00 - Support and Testing](Guides/00%20-%20Support%20and%20Testing.md) | what's supported and what's tested, feature by feature - and what isn't yet |
| [01 - WR Options](Guides/01%20-%20WR%20Options.md) | the editor's own WR page - every row, what saves where |
| [02 - WR Automate](Guides/02%20-%20WR%20Automate.md) | the editor builds the camera edit for you, obstacle checks, Clear Timeline |
| [03 - WR Garage](Guides/03%20-%20WR%20Garage.md) | paint, livery, lights, plate, body parts, wheels, randomise |
| [04 - Car Look per marker](Guides/04%20-%20Car%20Look%20per%20marker.md) | a new car look from a marker on, cut on the beat |
| [05 - WR Blend and WR Shake](Guides/05%20-%20WR%20Blend%20and%20WR%20Shake.md) | on-time camera paths and real camera shake, saved with the project |
| [06 - Time and Weather](Guides/06%20-%20Time%20and%20Weather.md) | per clip and per marker, cut or smooth time-lapse |
| [07 - Director Mode](Guides/07%20-%20Director%20Mode.md) | fly the camera live, the take becomes markers - all controls |
| [08 - Editor Look](Guides/08%20-%20Editor%20Look.md) | Neon theme, 10 fonts, every colour, header art |
| [09 - Free Camera](Guides/09%20-%20Free%20Camera.md) | no leash, no collision, any zoom and speed, cutscene clips, no seek freeze |
| [10 - Loading Screens](Guides/10%20-%20Loading%20Screens.md) | the WR launch and clip screens, Windows 10 note |
| [11 - Crash Fixes and Reports](Guides/11%20-%20Crash%20Fixes%20and%20Reports.md) | what the fixes do, the reports, what to send when it crashes |

## Features (v0.9.0)

**Crash fix — on by default:**
- Fixes the crash after an export or when leaving the
  export screen (`+373EA6`, `+3E541F`, `+12E4D71` / `floor-north-enemy`): a
  replay object kept an entity that had already been removed from the world.
  The plugin keeps that entity out and treats its leftover data as empty.
- Fixes the crash when an export loads a clip with an item
  that has no name (`arizona-beryllium-river`, `[Crash Fix]
  EmptyNameLookupFix`, game build b3258).
- The safety net no longer stops a working export
  (`berlin-golf-wyoming`): it now measures recoveries per second instead of
  counting until a pause.
- Fixes the crash when a clip dresses a ped
  that was never loaded (`king-yankee-east` and the crashes that followed it:
  `social-nuts-colorado`, `fifteen-princess-double`, `thirteen-johnny-low`,
  `saturn-robert-lactose`). Seen with custom hands/body models on an RP
  server: one ped's model never loaded, and the editor kept writing its
  clothing, checking it and saving it into nothing. The plugin now skips that
  ped's look and answers "nothing here" for it, so the clip loads, the free
  camera works and saving (F5) works. That ped may look default in the
  preview. Confirmed by the tester who reported it.
- With that same broken ped in a clip, moving the editor
  camera near it could freeze the game ("FiveM has stopped responding"): the
  game walked the ped's missing skeleton forever. The plugin now stops that
  walk and skips the ped's bones. In rare cases the clip can still crash a
  bit later on that ped; that last step is being tested.
- Fixes the crash when you load a second clip right after
  the first (`music-arkansas-vermont`): the editor looped over a table that
  was already gone. The plugin now finishes that loop as "nothing found".
- Fixes `RAGE error: ERR_GEN_MAP` when an export starts
  on a heavy server (`[Crash Fix] GrowStreamingList`, game build b3258): the
  game's list of things waiting to load ran full during the export's reload,
  and the plugin now adds room to it too. Built from a real crash; it hasn't
  come back since, but it hasn't been forced to happen again either.
- Fixes the `RAGE error: ERR_STR_INFO_2` and
  `ERR_STR_INFO_3` game errors (`[Crash Fix] GrowStreamingList`, game build
  b3258). The game keeps a fixed list of 32768 streaming entries. On heavy
  servers the world alone uses about 28000 of them, so a teleport, a cutscene
  loading or an editor export fills the rest and the game stops. When the
  list runs full, the plugin adds more room to it instead. Works in game and
  in the editor.
- Stops the Rockstar Editor crashing when switching, editing, or exporting
  clips that reference a custom asset (vehicle, MLO, prop, ytyp) which got
  unloaded. This is the core fix and covers every known variant of this
  crash found so far.
- Also catches the same crash pattern in FiveM's streaming/asset-unload
  code on heavy custom-asset servers, not just the editor itself.
- Fixes the crash on servers with many duplicate or
  conflicting map archetypes (`diet-queen-carbon` /
  `india-connecticut-arizona`), where the editor walked a lookup table that
  was never filled in. Field-confirmed on a server where the clip had
  crashed on every single attempt.
- Catches a divide-by-zero that the recovery itself
  could trigger, and stops multi-site runaway loops before they corrupt
  memory.
- Fixes a crash when loading another clip after the first one, where one of the plugin's own built-in guards was handed a broken
  pointer that looked valid.
- Fewer crashes on clips with lots of players (more than 32): the editor no longer loops forever over a player slot it never filled
  in (`cold-cardinal-mountain` and its b3095 versions). The editor itself is
  built for 32 players, so very big clips can still crash later or show
  wrong faces on the extra players.
- When the game raises its own fatal error
  (`RAGE error: ERR_...`), FiveM now reports it cleanly instead of the plugin
  turning it into a second, confusing crash.
- The log says which game build you're on, and parts built for b3258
  switch themselves off on other builds. The plugin loads
  on every game build FiveM supports (it used to refuse to load on some), and
  the log names the GTA V update and how far that build is tested.

**Experimental, on in the shipped `.ini` — `[Vehicle Meta] SkipBrokenVehicleMeta`:**
- For servers that ship a vehicle with a broken `carvariations`/`handling`
  file. Symptom: clips play fine but the moment one using that car is added
  to a project the editor hangs and dies with "Out of game memory". Turn
  this on and the plugin remembers any vehicle file the game itself reports
  as malformed and skips it from then on (saved in `WR_BrokenVehicleMeta.txt`).
  It learns on the first failure, so the very first attempt can still crash
  once - relaunch and it's skipped.
- It finds the spot it hooks into by itself, so FiveM updates don't switch
  it off.

**NVE (NaturalVision Evolved) + EVE (ExtendedVideoExport), on by default —
`[Crash Fix] NveExportFreezeFix` and `EveSwapChainFix`:**
- No more "FiveM has stopped responding" when an EVE
  export starts with NVE. The export's video encoder, NVE and ReShade waited
  on each other forever; the plugin makes them take turns in the same order
  ReShade does. Only active while NVE.asi is loaded.
- NVE's ReShade .addon file
  (`ReshadeEffectShaderToggler.addon64`) no longer crashes the game a few
  seconds after launch with EVE (`d3d11.dll+5BFEC`). EVE's throw-away swap
  chain made ReShade build and drop a second effects runtime, which broke the
  .addon. EVE now gets the game's own swap chain, so your ReShade / NVE look
  is still in the export. Only active with EVE + ReShade.
- **WR Editor Fix shows up in ReShade's Add-ons section** (Home
  key -> Add-ons). That's how it finds the game's swap chain for the fix
  above - leave it ticked.
- NVE, EVE, ReShade and the .addon aren't changed. Tested with full NVE + EVE
  + Voukoder on a server: several sessions of 4 exports in a row, no crash.

**Broken-asset report, on by default —
`[Stuck Downloads] ReportStuckDownloads`:**
- Lists server downloads that never finish in `WR_BrokenAssets.log` (resource
  + file) - a plain list to send to your server owner. It only lists them,
  nothing is skipped, so it's safe while you play. Set it to 0 to turn it
  off. See "Broken files on the server" below for what to do with it.

**Time + weather in the editor, on by default —
`[Editor Time Weather]` (game build b3258):**
- Marker menu -> **WR Options** (Enter) -> Hour / Minute / Weather / Default.
  Pick any minute of the day and any GTA weather (Extra Sunny, Clear, Clouds,
  Smog, Foggy, Overcast, Rain, Thunder, Clearing, Neutral, Snow, Blizzard,
  Light Snow, Xmas, Halloween). It changes live in the preview, the lighting
  follows, and the export renders exactly what you see.
- The rows show the clip's own recorded time and weather until you change
  them. **Default** (Enter) puts everything back to what was recorded.
- Your pick stays for every clip until you press Default or restart FiveM -
  it isn't saved with the project yet. Nothing is written into your clips.
- `TimeWeatherOverride` / `Time` / `Weather` in the `.ini` set it without the
  menu (live, applies within a second of saving). `MenuRows = 0` hides the
  menu row.
- **New in v0.9.0: per marker.** Cameras -> **WR Marker Options** -> Time &
  Weather On, Hour, Minute, Weather, Change. From that marker on the clip plays
  with its own time and weather until the next marker that has one. Change =
  Cut switches right at the marker; Smooth changes gradually toward it (a
  time-lapse). It wins over the WR Options pick and works in the export. Not
  saved with the project.

**No seek freeze, on by default — `[Editor Playback] NoSeekStall` (game
build b3258):**
- After every seek, cut or marker move the editor waited until the whole game
  had finished streaming. On a busy server that never happens, so it froze
  for about 7 seconds every time. Now it waits at most `NoSeekStallWaitMs`
  (default 100 ms) and plays on; anything still loading pops in a moment
  later.
- Exports keep the full wait, so the rendered video is fully loaded.
- Too much popping in? Raise `NoSeekStallWaitMs` (6600 = the stock wait) or
  set `NoSeekStall = 0`.

**Editor free camera — on by default, each independently toggleable:**
- Remove the distance leash that pulls the free-cam back when it flies far
  from the subject (custom max distance).
- Uncap the zoom/FOV range past the stock ~10-100° (up to 1-130°).
- Disable camera collision: it really goes through anything - walls and the
  map, the car or ped it's attached to or looking at, and objects between two
  markers (no "Unable to apply camera blend due to object collision" jump).
- Scale the free-cam's move speed (adjustable multiplier, updates live
  while flying — no relaunch needed). **New in v0.9.0:** also in the editor,
  marker menu -> WR Options -> Camera Speed (x0.25 to x20), saved back to the
  `.ini`.

**New in v0.9.0: WR Options — the editor's own WR page (game build b3258):**
the last row of the marker menu. Hour / Minute / Weather / Default, Camera
Speed, Header Style, Header Motion, Font, Colors, **WR Garage**, **Director
Mode**, **WR Automate** and **Clear Timeline** - everything below lives there.

**New in v0.9.0: WR Automate — the editor builds the camera edit for you —
`[WR Automate]` (game build b3258):**
- WR Options -> **WR Automate**: Follow (the car the recorded player drives,
  or the player), Length (the whole clip or 5 - 60 s), Markers (3 - 30),
  Style (Mixed / Orbit / Chase), Shake (Auto / Off / one preset), then
  **Automate**.
- The timeline starts fresh, the clip is scouted, and WR Automate places its
  own markers with free cameras in a ring of cinematic shots around the car
  (chase, high rear, sides, low front, front) - WR blend and a shake on every
  one, and the car stays centred on screen the whole time.
- Then it plays the clip again with the game's own camera collision test and
  moves any camera that would touch or look through a car, ped, prop or wall.
  Close to the ground is fine, under it isn't. `AvoidObstacles = 0` skips it.
- The help line shows the progress, Back stops it, and everything stays
  editable afterwards. Works best right after recording, on a fresh clip.
- **Clear Timeline** (WR Options, Enter twice) puts a clip back to a fresh
  one: every marker gone, the default start and end markers, every setting
  default. No undo.

**New in v0.9.0: WR Garage — tune the car inside the editor (game build b3258):**
- WR Options -> **WR Garage** tunes the car the recorded player drives, live:
  Livery (Off or any livery the car has, by its name), Primary / Secondary
  paint (22 colours), Finish (Normal / Metallic / Pearl / Matte / Metal /
  Chrome), Neon, Xenon colour, Lights (On / On + Full Beam / Off), Window
  Tint, Plate Text (typed in the game's own keyboard, up to 8 characters),
  Plate Style, Body Parts (every part slot the car has, wheel type and rims),
  Randomise Colors / Randomise All / Randomise Parts, Clean and Reset.
- Every row starts at "As recorded"; Reset puts the car back exactly as it
  was recorded.
- **Per marker:** Cameras -> **WR Marker Options** -> **Car Look** opens the
  same page for that marker. From that marker on, the car wears its look until
  the next marker that has one - a new paint, livery or body kit on a cut.
  Before the first one, the clip's look shows.
- Works in the export too. Not saved with the project yet: the looks stay
  until you restart FiveM.
- Add-on cars can map their paint slots their own way (for example the
  second colour on the headlight glass); vanilla cars do what the rows say.

**New in v0.9.0: WR blend + WR shake for marker cameras (game build b3258):**
- **WR blend** (Cameras -> Blend -> **WR**, after Smooth): the stock Smooth
  lets a spring chase the camera, so it always lags behind what you film. WR
  blend passes every marker exactly on time with the speed flowing through
  them - position, rotation and zoom - and the export matches the preview.
  For free-camera markers; attached and look-at markers keep the stock Smooth
  for now.
- **WR shake** (Cameras -> Shake -> **WR**, after Explosion): Handheld, Walk,
  Run, Car, Helicopter and Earthquake, each with its own motion, plus Custom
  (Turn / Slide / Shiver / Steps), with Strength and Speed. It fades into the
  next marker's shake over a blend and looks the same in the export.
- **Saved with your project:** every marker's WR blend and WR shake goes into
  `WR Editor Fix\Projects\<project name>.json` right after a change and
  comes back when the project opens. Trimming, moving or deleting other clips
  doesn't move them.

**New in v0.9.0, first version: Director Mode — fly the camera live, the take
becomes markers (game build b3258):**
- WR Options -> **Director Mode**: Look Assist (keeps the car or player
  centred), Follow (the camera rides along with the car), Record Speed (100 /
  50 / 35 / 20 % - fly in slow motion, it plays back at normal speed), Detail,
  **START**.
- 3-2-1, the clip plays and you fly. When it ends, the take becomes markers -
  the fewest that still reproduce your move - and the playhead goes back to
  the start.
- Controller: sticks move / look, LT / RT down / up, LB / RB zoom, D-pad speed
  / roll, hold A = precise, hold L3 = fast, X assist, Y follow, B stop. Mouse +
  keyboard works too (WASD, mouse look, Q / E, Shift, Ctrl, F, G, Backspace
  stops), but a controller is much smoother.
- First version: no obstacle checks on a take yet, no re-recording one part.

**New in v0.9.0: the editor's look — `[Editor Look]` (game build b3258):**
- **Theme = Neon** (on in the shipped `.ini`): the WR Neon Glass look on the
  clip edit screen - a frosted glass menu with a neon pill on the selected
  row, one glass panel for the time and the playback buttons, a slim timeline
  with a red played line, a glowing playhead and diamond markers. The game
  draws it (our own built-in editor movie), it's not an overlay. `Theme =
  Default` gives the stock editor.
- **Font:** 10 fonts built in - Chakra Petch, Spicy Rice, Bagel Fat One,
  Oswald, Carter One, Ubuntu Mono, Permanent Marker, Germania One, Kavoon,
  Sriracha - or Default (the original Rockstar Editor font). Every editor
  text uses it.
- **Colors:** WR Options -> **Colors** recolours every part live from a
  palette (Neon: Glass, Selection, Buttons, Icons, Time, Timeline, Markers,
  Help Box; Default theme: Menu Text, Greyed Text). Default Colors puts them
  back.
- **Header:** the logo at the top of the editor menu - Stock, WR, Meme (on in
  the shipped `.ini`), Retro or Cinematic, animated or still.
- Font, Colors, Header Style, Header Motion and Camera Speed change live in WR
  Options, and the pick is saved back into the `.ini`.
- **Replaces `[Editor Theme]`** from v0.8.0 and older (`EditorTheme`,
  `EditorFont` and the GTA font list are gone). Take the new `.ini`.

**Record GTA V cutscenes (game build b3258), on by default:**
- **`[Recording] AllowCutsceneRecording`:** the Rockstar Editor keeps
  recording while a real GTA V cutscene plays or loads (for example one a
  server script starts). Normally the game stops the recording the moment you
  aren't in control of your character, and the clip fails with "Clip must
  be at least longer than 3 seconds". The cutscene's actors, camera and audio
  all end up in the clip. Scripts that block recording on purpose still work.
- **`[Editor Camera] FreeCameraOnBlockedClips`:** the editor normally locks the
  camera on such clips ("You cannot edit camera properties as this clip
  contains a blocked cutscene"), and on clips recorded in first person. This
  unlocks the marker's Cameras menu and lets the free camera move on them.
- Known limit: recording doesn't continue while a script camera flies over
  the cutscene (a server's own cutscene camera tool).
- On other game builds both switch themselves off, and the log says so.

**WR loading screens, on in the shipped `.ini` —
`[Editor Loading Screen]`:**
- **Editor launch screen (`LaunchScreen`):** press "Rockstar Editor" + Yes in
  FiveM's main menu and the WR screen shows at once, instead of FiveM's own
  one. It shows live load progress, a "Running now" list of what's on in
  your `.ini`, and the update log from GitHub - with an "Update available"
  box when a newer version is out. It closes by itself when the editor is
  ready; double-click it to close it early. It stays out of the way at the
  main menu and when you join a server.
- **Clip screen (`ClipScreen`):** a minimal WR screen while a clip loads
  (Edit) or an export starts, instead of the stock "Preparing clip" screen.
  It closes the moment the editor is ready.
- `UpdateCheck = 0` stops the GitHub request (the built-in update log is
  shown instead).
- Both need the **Microsoft Edge WebView2 Runtime**: built into Windows 11, and
  on Windows 10 it comes with Microsoft Edge. If it's missing, the log says so
  and FiveM's own screens are used. Works best with the game in
  "Windowed Borderless".
- **Tested on Windows 11.** On Windows 10, or if anything looks wrong while the
  editor opens (black / white / frozen screen, flickering, the game
  minimising, a missing or double mouse cursor), set `LaunchScreen = 0` and
  `ClipScreen = 0`. FiveM's own screens come back and nothing else changes.
  Please send your logs on Discord so it can be fixed.

## Known issues / what's being worked on

- **The WR loading screens are only tested on Windows 11** (see above).
  Pressing Export a second time in the same session can show the clip
  screen a few seconds late.
- **Only tested on game build b3258.** Every other build in the table above
  is tested by the people who play on it. A crash already fixed on b3258 can
  still happen on another build, because the fix has to be matched to each
  build's code separately.
- **On very heavy servers, editing a clip and then exporting in the same
  session can still crash on export** (`alabama-twenty-hawaii`,
  `GTA5_b3258.exe+600FB30`). Leaving the edit screen makes the game reload
  its replay content, and on some servers that reload trips over a freed
  object. Workaround that works today: edit and save your project, relaunch
  FiveM, open the already-edited clip and export it without editing again.
  Actively being investigated - the cause is now understood, the safe fix
  isn't finished.
- **Opening a project and then exporting can crash on some clips** (the clip
  loads twice: once for the project preview, once for the export, and the
  second load can trip over a map object that's already gone; seen as
  `butter-batman-nuts`, `yellow-november-arkansas`, and with several renders
  in a row). Being worked on. Until then: restart FiveM between
  big renders.
- An experimental fix for the editor hanging on "Downloading assets" is
  in the config (`[Stuck Downloads] SkipStuckDownloads`), off by default. Less
  battle-tested than the core crash fix above — only turn it on if you
  actually hit that infinite hang. Since v0.8.0 it only acts inside the
  Rockstar Editor; while you play on a server it only reports, so it can stay
  on.
- **No seek freeze is tested on one big server so far.** If the preview
  pops in too much on yours, raise `NoSeekStallWaitMs` or set
  `NoSeekStall = 0`, and tell me on Discord.
- **Director Mode is a first version.** It doesn't check for obstacles on a
  take yet, and you can't re-record just one part. Works best with a
  controller.
- **Not saved with the project yet:** WR Garage looks (clip and per marker)
  and time + weather (WR Options and per marker). They stay until you restart
  FiveM. WR blend and WR shake are saved.
- **A crash while editing some clips with add-on cars**
  (`ERR_MEM_EMBEDDEDALLOC_GUARD_1`, or a crash at `+176B0BB`): a car keeps a
  removed part in its parts list. A guard for it is in, but it came back once
  more on the same clip. Being worked on - send the crash dump and logs on
  Discord if you hit it.
- **The `.asi` is about 7.8 MB now** (the editor art and fonts are built in).

## Rockstar Editor+ (RE+) — not supported, and it won't be

WR Editor Fix will not support Rockstar Editor+ (RE+), not in this version
and not later. I tested RE+ properly next to WR Editor Fix on game build
b3258 and decided against it:

- **Both plugins change the same editor camera code.** Two plugins fighting
  over the same thing breaks easily, and every update on either side could
  break the other again.
- **Some RE+ features don't work on b3258** (camera collision, free camera on
  first-person clips).
- **It froze my game while editing.** RE+'s "no wait after seeking" makes the
  game do blocking model loads much more often, and one stuck load froze
  everything.
- **RE+ on its own still crashed on export** on my server
  (`ERR_STR_INFO_2`), a Rockstar Editor crash WR Editor Fix already catches.
- **Its renderer was far too slow for my renders** (about 10% in 5 minutes),
  so I stay with EVE for exporting.

Instead, the editor features people use RE+ for are built into WR Editor Fix
itself, from my own research and my own code: no freeze after seeking,
time + weather that stays in the export (per clip and per marker), no camera
collision, unlimited camera distance, uncapped zoom, free camera on blocked
clips, free-cam speed, and since v0.9.0 WR blend (smooth marker blending that
stays on time) and WR shake presets, saved with your project.

**Using RE+ anyway?** It isn't supported together with WR Editor Fix. If RE+
has its own camera distance, zoom or fast-precache options switched on, WR
Editor Fix leaves those parts to RE+ (one line in the log says so) so the two
don't fight over them. But if you crash or freeze, remove RE+ and test again
before reporting. Nothing against RE+ or its developer - I just want one
plugin that's built and tested for FiveM.

## What might come in future updates

No promises on timing — solo project, worked on as time allows:
- Save WR Garage looks and time + weather with the project.
- Director Mode: obstacle checks, re-record one part, its own `.ini` section.
- WR Garage for the other cars (and peds) in a clip, not only the player's.
- A fix for the vehicle-data crash mentioned above, if a safe one is found.
- Camera roll/tilt control unlock.
- Export resolution/framerate unlock.
- Auto-save while editing, so a crash never loses your work.

Check back on this repo for updates — new versions will be numbered v0.10.0,
v0.11.0, and so on as they ship. Full version history: `CHANGELOG.md`.

## Install

1. Download `WR_Editor_Fix.asi` and the `WR Editor Fix` folder (with its
   `.ini` inside) from this release.
2. Copy **both** into your FiveM `plugins` folder:
   `%LOCALAPPDATA%\FiveM\FiveM.app\plugins\`
3. Relaunch FiveM.

That's it — the crash fix and the main features are already on in the
shipped `.ini`. Open `WR_Editor_Fix.ini` if you want to turn anything on, off
or adjust it.

**Already on v0.8.0 or older?** Replace the `.asi` **and** take the new
`.ini`: `[Editor Look]` replaces `[Editor Theme]`, and `[WR Automate]` is new.
If you had your own menu colours, copy them into `[Editor Look]` `MenuText` /
`MenuTextGreyed`.

**Verifying your download:** the SHA256 checksum for `WR_Editor_Fix.asi` is
in `WR_Editor_Fix.asi.sha256`. If you're ever unsure a copy is genuine
(re-shared somewhere other than the official release page), check it
matches.

**Note:** this plugin does not create its own folder or config file. If you
skip step 2, it will just run on its built-in defaults with no log file —
make sure the `WR Editor Fix` folder actually ends up next to the `.asi`.

## Configuration

Open `WR Editor Fix\WR_Editor_Fix.ini` in a text editor. Every option has a
comment explaining what it does. (Developer/diagnostic settings are kept in a
separate file that isn't part of the release — you don't need it.) The
`[Editor Camera]` section and the `[Editor Time Weather]` time / weather keys
reload live while FiveM is running — edit, save, and it applies within a
second, no relaunch needed. `[Editor Look]` is read every time the editor
opens, and WR Options changes its Font, Colors and Header live. The plugin
only writes back what you change in the editor itself (WR Options: Font,
Colors, Header Style / Motion, Camera Speed and the WR Automate page), each
into its own line. Everything else (including `FreeCameraOnBlockedClips`,
`[Recording]`, the `[Crash Fix]` switches such as `GrowStreamingList` and
`EveSwapChainFix`, `[Editor Playback]`, `MenuRows`, `[WR Automate] Enabled`
and `[Editor Loading Screen]`) needs a relaunch to take effect.

## ⚠️ Windows Defender says "Trojan" / "malware"? (known issue, I'm working on it)

Some people get a Windows Defender popup saying `WR_Editor_Fix.asi` is a
trojan or malware. **It's a false positive**, and I know about it.

**Why it happens:** to stop the crashes, the plugin patches the game's own
memory while it runs, catches the game's crashes and checks GitHub for
updates. That's exactly how every `.asi` crash fix / mod works, but to an
antivirus it can look like a cheat or an injector. The file is also new and
not code-signed, so Windows has no "reputation" for it yet and its automatic
cloud check guesses "trojan" (often a name ending in `!ml` = a
machine-learning guess, not a real virus signature).

**What I'm doing:** I'm working on it for the next updates - making the file
look less suspicious to antivirus and reporting every release to Microsoft as
a false positive so Defender stops flagging it.

**What you can do right now:**
- Only download WR Editor Fix from the official GitHub release page or my
  Discord - never from anywhere else.
- If Defender removed it: Windows Security → Virus & threat protection →
  **Protection history** → open the entry → **Actions → Restore / Allow on
  device**.
- If FiveM says "Couldn't load WR_Editor_Fix.asi": right-click the `.asi` →
  Properties → tick **Unblock** at the bottom → OK.
- If you want to help: send me a screenshot of the Protection history
  details (the threat name) on Discord, it helps me get it cleared faster.

## Found a new crash?

**Please don't open a GitHub Issue for this — use Discord instead**, it's
the only place support requests actually get seen.

If you hit a Rockstar Editor crash that this plugin doesn't already catch,
I want to know — I'll try to build a fix for it. Please:

1. Contact **Warraa_** on Discord: https://discord.com/invite/FKJ27bhqfJ
2. Open a support ticket.
3. Send:
   - The crash dump file (the `.zip` FiveM saves when it crashes — the crash
     window itself tells you where it saved it, and gives a copy-to-upload
     option).
   - A screenshot of the actual crash window/error message.
   - **All** the log files from `WR Editor Fix\Logs\` (next to the `.asi`,
     in your FiveM `plugins` folder) — `WR_Editor_Fix.log` and anything else
     in that `Logs` folder.
   - If a `WR Editor Fix\Dev Logs\` folder exists, send everything in it
     too. Those files only appear when the plugin catches a specific crash
     shape, and they're the most useful thing you can send — they're what
     solved the duplicate-archetype crash.

The more of that you send, the faster I can actually find and fix it —
missing pieces (especially the logs) usually means I can't reproduce it.

### Broken files on the server — I can't fix those

WR Editor Fix stops the editor from crashing when a clip uses things that are
no longer loaded. It **cannot repair files that are broken on the server
itself**. If your logs show a broken server file, for example:

- `WR_BrokenAssets.log` lists a resource + file (a download that never
  finishes, like `tstudio_zmapdata / el_burro_heights.ymt`),
- `WR_BrokenVehicleMeta.txt` lists a broken `vehicles.meta` /
  `carvariations.meta`,
- or a map / MLO / ytyp / ymap from a server resource that is broken,

then that file has to be fixed by the **server owner / developer**, not by
me. Please send them the log and the file name. I'm not able to fix broken
server assets or server scripts through the `.asi`. If the editor still
crashes after the server has fixed the file, send me the new logs and I'll
look again.

YouTube: https://www.youtube.com/@Warraa__

## Disclaimer

Not affiliated with or endorsed by Rockstar Games, Take-Two Interactive, or
Cfx.re. Use at your own risk.

## License

Closed source. You're free to download and use this for personal or server
use. Do not redistribute, resell, decompile, or repackage it. Source is not
published.

Third-party components used are credited in `THIRD-PARTY-NOTICES.txt`. The
editor fonts built into the plugin are free Google Fonts; their licences are in
the release's `Fonts` folder.
