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

**The editor tools run on b3258, b3095 and b3407:** WR Options, WR Automate,
Beat Sync, WR Garage, Car Look, WR blend, WR shake, time + weather, Director
Mode, the editor look + Timeline Size, WR Export, No seek freeze, cutscene
recording, free camera on blocked clips. On other builds they switch
themselves off and the log says so.

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
| EVE (ExtendedVideoExport) | Yes - **or** WR Export, not both at once (both can crash; the loading screen says so) | **Yes** |
| The editor's own stock export (`[WR Export] Enabled = 0`) | Yes | Not separately for the new tools (same playback, so it should match) |
| NVE (NaturalVision Evolved) + ReShade | Yes | **Yes** (with EVE + Voukoder) |
| QuantV | Yes | **Yes** |
| ReShade in WR Export videos | **Only ReShade with full add-on support** - the standard download isn't supported. Don't have it? Download it from [reshade.me](https://reshade.me) | **Yes** (ReShade 6.8.0 with full add-on support) |
| Rockstar Editor+ (RE+) | **No** - and it won't be | Tested side by side once; that's why it's not supported |

## The editor tools (v1.0.0)

| Feature | Tested | Not tested yet |
|---|---|---|
| **WR Options** page | Every row, live, saving back to the ini | - |
| **WR Automate** | Open-road, city and drift clips, Follow = Main car, Style = Mixed, WR Blend + Hard Cut, Distance / Height, Checks On, calm follow, obstacle checks | Follow = Main ped, Orbit / Chase on their own, Length = Timeline, Checks = Ground only, very long clips, projects with several clips |
| **Beat Sync** | mp3 songs, Cut every Bar, the song playing in the editor, the edit sheet | Other song formats, very long songs |
| **Clear Timeline** | Yes | - |
| **WR Garage** | A vanilla car: every row, Body Parts, wheels + rims, all three randomise buttons, Reset; Clean (also in the export); the look saved with the project | Motorbikes, boats, aircraft |
| **WR Garage on add-on cars** | Add-on drift cars: works, but their paint slots are mapped their own way | Many add-on cars. One add-on car clip has hit a crash while editing (see Known issues) |
| **Car Look per marker** | 5 marker looks: preview playback and an export, switching at every marker | Projects with several clips |
| **WR blend** | Preview + export | Attached / look-at markers (they keep Smooth on purpose) |
| **WR shake** | Every style live, preview == export | - |
| **Saved with the project** | WR blend + shake, Garage look, Car Look, time + weather: save, restart FiveM, reopen - all back | Trimming / moving clips in a big project |
| **Time + weather** (WR Options) | 5 exports with 5 different looks, all correct | - |
| **Time + weather per marker** | Preview + export (cut and smooth markers) | Snow on the ground (not supported) |
| **Director Mode** | A take at 50 % record speed with a controller (18 Smart markers); mouse + keyboard | Very long takes, Follow on peds |
| **Editor look** (Neon, fonts, colours, header) | Both themes, fonts, colours and headers, live switching, saved to the ini | Other screen resolutions / UI scales |
| **Timeline Size** | Neon theme, 50 - 300 %, live + saved, on all three builds | The Default theme |
| **WR Export** | Every Export screen row, the four presets + Save Preset, HEVC / H.264 / AV1, CQP + bitrate, Screen / 1440p / 4K, motion blur 4 - 64 samples, Blur Shape, ReShade, Sound off | AMD / Intel encoders; sound with motion blur (known issue) |

## Older features

| Feature | Tested | Not tested yet |
|---|---|---|
| Core crash fix + specific crash fixes | Each built from a real crash; most confirmed on the reporter's own clip | Crashes nobody has reported yet; `ERR_GEN_MAP` hasn't been forced to happen again |
| No seek freeze | One big server, 225+ seeks, no stall | Other servers |
| Free camera (leash, zoom, collision, speed) | Yes | - |
| Cutscene recording + free camera on blocked clips | Yes (b3258, b3095) | Script cameras over a cutscene (known not to work); b3407 |
| WR loading screens (+ Game build card, Plugins card, RE+ warning, EVE INFO box) | Windows 11, windowed borderless | Windows 10, exclusive fullscreen, a second PC |
| Broken-asset report | Yes | - |
| SkipStuckDownloads (experimental, off) | Partly - it can release slow but healthy downloads | Most servers |
| NVE + EVE fixes | Several sessions of 4 exports in a row, no crash | - |

## Known issues

- WR Export with motion blur: the sound comes out too long - the blur presets
  have Sound off; add music in your video editor.
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
