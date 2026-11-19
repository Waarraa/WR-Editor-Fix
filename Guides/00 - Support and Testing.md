<!-- MADE BY WR | WARRAA_ -->
# Support and Testing - what's supported, what's tested

WR Editor Fix is a solo project. Everything is built and tested on **one PC**
(Windows 11, an NVIDIA RTX graphics card, FiveM game builds **b3258, b3095
and b3407**) on **one big RP server** with many custom cars, maps and clothes,
plus the testers who send their logs on Discord. This page says honestly what
that covers and what it doesn't.

**Supported** = it is meant to work there, and a problem there is a bug I want
to hear about. **Tested** = it was actually run and checked there.

## Game builds

| Game build | Supported | Tested |
|---|---|---|
| **b3258** (Bottom Dollar Bounties) | Yes - every feature | **Yes** - everything on this page |
| **b3095** (The Chop Shop) | Yes - every feature | **Yes** - every editor tool, WR Automate, Director Mode with a controller, cutscene clips, WR Export |
| **b3407** (Agents of Sabotage) | Yes - every feature | **Yes** - WR Options, WR Garage, WR Automate + Beat Sync, Timeline Size, WR Export. Not yet: Director Mode, cutscene clips |
| Every other FiveM build (b1604 - b3889) | The plugin loads and the log names your build; the crash fixes may not apply; the editor tools switch off | No - community testing |
| GTA V Enhanced | **No** | No |

Good to know: on servers running current FiveM, a build **lower** than b3258
can still run the b3258 game with that build's content, so everything applies.
The README has the full build table.

**Which build am I really on?** FiveM runs the **higher** of the build you
start it with (`-b3095`) and `[Game] DefaultBuild` in
`FiveM.app\CitizenFX.ini` - and a server you join can raise DefaultBuild. So
FiveM's main menu can say b3095 while the game is b3258 (b3095's map content,
b3258's game). The WR log tells the truth:

- `Running game build: b3258 (this FiveM run's game process: FiveM_b3258_GTAProcess.exe)`
- `FiveM's CitizenFX.ini [Game] DefaultBuild=3258 ...` - the rule above.
- `[Clips] ...` - the build every clip was **recorded** on (read from the clip
  file itself), and a note when you open a clip from another build.

**Edit clips on the build they were recorded on.** On another build marker
jumps can get slow, the clip can load or look different, a short black flash
can show right after the clip opens and some clips can crash - that is the
build difference, not a WR bug. To edit a b3095
clip: set `DefaultBuild=3095` in CitizenFX.ini (FiveM closed), start FiveM on
b3095, open the editor from FiveM's main menu.

**The editor tools run on b3258, b3095 and b3407:** WR Options, WR Automate,
Beat Sync, WR Garage, Car Look, WR blend, WR shake + Shake Options, time +
weather, Director Mode, the editor look + Timeline Size, WR Export, the Export
Watermark, No seek freeze, cutscene recording, free camera on blocked clips.
On other builds they switch themselves off and the log says so.

**Since v1.1.0 everything switches on only when the Rockstar Editor opens** -
nothing is written into the game at FiveM start or while you play on a
server. `11 - Crash Fixes and Reports.md` explains it and the log lines.

## Windows, hardware, other plugins

| | Supported | Tested |
|---|---|---|
| Windows 11 | Yes | **Yes** |
| Windows 10 | Yes | **No** - the loading screens especially: if they misbehave, turn them off (`10 - Loading Screens.md`) |
| NVIDIA graphics | Yes | **Yes** (RTX 5070 Ti) |
| AMD / Intel graphics | Yes | No |
| WR Export on NVIDIA (NVENC) | Yes | **Yes** - HEVC, H.264 and AV1, CQP and bitrate |
| WR Export on AMD (VCN) / Intel (Quick Sync) | Yes | No |
| WR Export on the CPU encoder | Yes (H.264, bitrate) | **Yes** |
| Controller (Director Mode) | Yes | **Yes** (Xbox-style pad through XInput) |
| Mouse + keyboard (Director Mode) | Yes, but clunky | **Yes** - works, a controller is much smoother |
| EVE (ExtendedVideoExport) | **No** (not supported anymore) - remove it, WR Export does your exports. The loading screen shows a red warning | Tested until v1.1.0 |
| The editor's own stock export (`[WR Export] Enabled = 0`) | Yes | Not separately for the new tools (same playback, so it should match) |
| NVE (NaturalVision Evolved) + ReShade | Yes | **Yes** |
| CoreFX | Yes | **Yes** |
| RenoDX DLSS 5 (ReShade add-on) | Yes | **Yes** (`renodx-dlss5.addon64`; DLSS 5 in the WR Export video) |
| QuantV | Yes | **Yes** |
| ReShade in WR Export videos | **Only ReShade with full add-on support** - the standard download isn't supported. Don't have it? Download it from [reshade.me](https://reshade.me) | **Yes** (ReShade 6.8.0 with full add-on support) |
| Rockstar Editor+ (RE+) | **No** - never supported | Remove it if you crash, then test again |
| ENB | **No** - never tested | Remove it if you crash, then test again |
| ModsHub mods / plugins | **No** - never supported | Remove them if you crash, then test again |

## The editor tools (v1.1.0)

| Feature | Tested | Not tested yet |
|---|---|---|
| **Editor-only switch-on** (v1.1.0) | b3095: nothing on at FiveM's main menu or while playing on a server; everything on in the editor opened from the main menu and from a server (ESC -> Rockstar Editor), crash fixes catching on a clip load there, WR Export + WR shakes in that export | b3258 and b3407; joining a server after using the editor (everything switches off again) |
| **WR Options** page | Every row, live, saving back to the ini | - |
| **WR Automate** | Open-road, city and drift clips, Follow = Main car, Style = Mixed, WR Blend + Hard Cut, Distance / Height, Checks On, calm follow, obstacle checks | Follow = Main ped, Orbit / Chase on their own, Length = Timeline, Checks = Ground only, very long clips, projects with several clips |
| **Beat Sync** | mp3 songs, Cut every Bar, the song playing in the editor, the edit sheet | Other song formats, very long songs |
| **Clear Timeline** | Yes | - |
| **WR Garage** (rebuilt in v1.1.0) | A vanilla car: every row incl. Pearl + Wheel Colour, Body Parts, wheels + rims, Randomise Colors / Everything, Reset, plate texts from the ini; the look saved with the project | Motorbikes, boats, aircraft |
| **WR Garage on add-on cars** | Add-on drift cars: works, but their paint slots are mapped their own way | Many add-on cars. One add-on car clip has hit a crash while editing (see Known issues) |
| **Car Look per marker** | 5 marker looks: preview playback and an export, switching at every marker | Projects with several clips |
| **WR blend** | Preview + export | Attached / look-at markers (they keep Smooth on purpose) |
| **WR shake** | Every style live, preview == export | - |
| **WR Shake Options** (v1.1.0) | The 5 new styles, every Shake Options row, Copy / Paste Shake (also the Paste row on a marker without WR shake), Shake Presets save + load, a WR Export with WR shakes | Apply To All Markers on very big clips, b3258 and b3407 |
| **Export Watermark** (v1.1.0) | WR, Custom (long lines too), Off and Stock with WR Export on b3095 - from the main menu and from a server | EVE / the stock export, b3258 and b3407 |
| **Saved with the project** | WR blend + shake, Garage look, Car Look, time + weather: save, restart FiveM, reopen - all back | Trimming / moving clips in a big project |
| **Time + weather** (WR Options) | 5 exports with 5 different looks, all correct | - |
| **Time + weather per marker** | Preview + export (cut and smooth markers) | Snow on the ground (not supported) |
| **Director Mode** | A take at 50 % record speed with a controller (18 Smart markers); mouse + keyboard | Very long takes, Follow on peds |
| **Editor look** (Neon, fonts, colours, header) | Both themes, fonts, colours and headers, live switching, saved to the ini | Other screen resolutions / UI scales |
| **Timeline Size** | Neon theme, 50 - 300 %, live + saved, on all three builds | The Default theme |
| **WR Export** | Every Export screen row, the four presets + Save Preset, HEVC / H.264 / AV1, CQP + bitrate, Screen / 1440p / 4K, motion blur 4 - 64 samples, Blur Shape, ReShade, Sound off | AMD / Intel encoders; sound with motion blur (known issue) |
| **WR Export: motion blur + sound** (v1.1.0) | One export: 1 - 3 clips, a moved Start Point, Matrix Freeze, slow motion, ReShade, the watermark, cancelling (the WR testers) | AMD / Intel encoders |
| **WR Export: your own logo** (v1.1.0) | A PNG with transparency in a real export, every corner | - |
| **WR Quick Menu** (v1.1.0) | b3407 (Warraa) + the WR testers: J / L3, mouse, arrows, pad, slots, tile picker, glass, Quick Menu Key | Other screen resolutions / UI scales |
| **WR Buddy** (v1.1.0) | b3407 (Warraa) + the WR testers: every screen of the editor, reactions, WR Automate + export commentary, click-through, never in an export | - |
| **WR Discord Presence** (v1.1.0) | In game with the Discord desktop app, on top of FiveM's own card | The Discord web / store app versions |
| **WR Languages** (v1.1.0) | b3095: German, French, Polish, Turkish, Russian menus; Finnish + Russian help; loading screens (Guide 08) | Native speakers checking every language |
| **WR World** (v1.1.0) | b3095: Road Wetness, Car Lights, Empty City, Clean Cars + Repair, Tyre Marks - preview + WR Export (Guide 17) | b3258 / b3407 in game |
| **WR Lights** (v1.1.0) | b3095: every light type, attach, presets, beams in WR Export (Guide 15) | b3258 / b3407 in game; 10+ shadowed lights |
| **WR Matrix Freeze** (v1.1.0) | b3095 + b3258: every Freeze Camera move, WR Export with and without motion blur (Guide 16) | b3407 in game; several freezes in one clip |
| **WR Face Camera** (v1.1.0) | b3095: every view on a drift clip, WR Automate Story inserts | b3258 / b3407 in game |
| **WR Undo** (v1.1.0) | b3095: Ctrl + Z / Ctrl + Y, the WR Undo row, adding + deleting markers (Guide 14) | b3258 / b3407 for adding / deleting markers |
| **WR Longer Recordings** (v1.1.0) | 3-minute recordings straight into the editor, two 3-minute WR Exports in a row; b3407 long clips (Guide 21) | Under 8 GB RAM (it stays off there) |
| **WR Wallpapers + Camera Range + Map Detail** (v1.1.0) | b3095: every wallpaper, Camera Range live, Map Detail at 3 km | - |

## Older features

| Feature | Tested | Not tested yet |
|---|---|---|
| Core crash fix + specific crash fixes | Each built from a real crash; most confirmed on the reporter's own clip | Crashes nobody has reported yet; `ERR_GEN_MAP` hasn't been forced to happen again |
| No seek freeze | One big server, 225+ seeks, no stall | Other servers |
| Free camera (leash, zoom, collision, speed) | Yes | - |
| Cutscene recording + free camera on blocked clips | Yes (b3258, b3095) | Script cameras over a cutscene (known not to work); b3407 |
| WR loading screens (+ Game build card, Plugins card, RE+ / EVE warnings) | Windows 11, windowed borderless | Windows 10, exclusive fullscreen, a second PC |
| NVE export freeze fix | Several sessions of 4 exports in a row, no crash | - |

## Known issues

- The editor opened from a server (ESC -> Rockstar Editor) keeps the stock
  editor look and the R* logo on the export watermark - open the editor from
  FiveM's main menu for those.
- Joining a server **after** you used the editor switches the editor tools off
  for the rest of that FiveM run - restart FiveM to edit again.
- Edit clips on the game build they were recorded on - on another build they
  load slower, a short black flash can show after the clip opens and some clips
  can crash.
- A crash while editing some clips with add-on cars
  (`ERR_MEM_EMBEDDEDALLOC_GUARD_1`) can still happen - a guard is in, the cause
  is still being chased.
- Opening a project and then exporting can crash on some clips - restart FiveM
  between big renders.
- The README's "Known issues" section has the full list.

## Help it get tested

Running something from a "not tested yet" column - another game build,
Windows 10, an AMD or Intel card, add-on cars, big projects? Tell me how it
went on Discord (https://discord.com/invite/FKJ27bhqfJ), working or not, and
send your `WR Editor Fix\Logs` folder. That's how a "No" turns into a "Yes"
here.
