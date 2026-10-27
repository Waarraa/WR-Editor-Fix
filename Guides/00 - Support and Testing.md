# Support and Testing - what's supported, what's tested

WR Editor Fix is a solo project. Everything is built and tested on **one PC**
(Windows 11, an NVIDIA RTX graphics card, FiveM game build **b3258**) on
**one big RP server** with many custom cars, maps and clothes, plus the testers
who send their logs on Discord. This page says honestly what that covers and
what it doesn't.

**Supported** = it is meant to work there, and a problem there is a bug I want
to hear about. **Tested** = it was actually run and checked there.

## Game builds

| Game build | Supported | Tested |
|---|---|---|
| **b3258** (Bottom Dollar Bounties) | Yes - every feature | **Yes** - everything on this page |
| b3095 (The Chop Shop) | Crash fixes load; the editor tools switch off | Partly (one editor session) |
| Every other FiveM build (b1604 - b3889) | The plugin loads and the log names your build; fixes may not apply; the editor tools switch off | No - community testing |
| GTA V Enhanced | **No** | No |

Good to know: on servers running current FiveM, a build **lower** than b3258
still runs the b3258 game, so everything applies. The README has the full
build table.

**All the editor tools are b3258 only:** WR Options, WR Automate, WR Garage,
Car Look, WR blend, WR shake, time + weather, Director Mode, the editor look,
No seek freeze, cutscene recording, free camera on blocked clips. On other
builds they switch themselves off and the log says so.

## Windows, hardware, other plugins

| | Supported | Tested |
|---|---|---|
| Windows 11 | Yes | **Yes** |
| Windows 10 | Yes | **No** - the loading screens especially: if they misbehave, turn them off (`10 - Loading Screens.md`) |
| NVIDIA graphics | Yes | **Yes** |
| AMD / Intel graphics | Yes | No |
| Controller (Director Mode) | Yes | **Yes** (Xbox-style pad through XInput) |
| Mouse + keyboard (Director Mode) | Yes, but clunky | **Yes** - works, a controller is much smoother |
| EVE (ExtendedVideoExport) | Yes | **Yes** - the export tests below were EVE exports |
| The editor's own stock export | Yes | Not separately for the new tools (same playback, so it should match) |
| NVE (NaturalVision Evolved) + ReShade | Yes | **Yes** (with EVE + Voukoder) |
| QuantV | Yes | Yes (tested before v0.9.0) |
| Rockstar Editor+ (RE+) | **No** - and it won't be | Tested side by side once; that's why it's not supported |

## The editor tools (v0.9.0)

| Feature | Tested | Not tested yet |
|---|---|---|
| **WR Options** page | Every row, live, saving back to the ini | - |
| **WR Automate** | An open-road clip and a dense city clip, Follow = Main car, Style = Mixed, obstacle checks + the 20 cm ground rule | Follow = Main ped, Style = Orbit / Chase on their own, very long clips, projects with several clips |
| **Clear Timeline** | Yes | - |
| **WR Garage** | A vanilla car: paint, finish, livery (8 liveries), neon, xenon, lights, tint, plate text + style, Body Parts (13 slots), wheels + rims, all three randomise buttons, Reset | Clean (the test car was already clean), motorbikes, boats, aircraft |
| **WR Garage on add-on cars** | One add-on car: works, but its paint slots are mapped its own way | Many add-on cars. One add-on car clip has hit a crash while editing (see Known issues) |
| **Car Look per marker** | 5 marker looks: preview playback and an EVE export, switching at every marker | Projects with several clips |
| **WR blend** | Preview + EVE export (markers 1 - 9 driven) | Attached / look-at markers (they keep Smooth on purpose) |
| **WR shake** | Every style live, preview == export | - |
| **WR blend + shake saved with the project** | Save, reopen: 12 marker settings back | Trimming / moving clips in a big project |
| **Time + weather** (WR Options) | 5 EVE exports with 5 different looks, all correct | - |
| **Time + weather per marker** | Preview + EVE export (cut and smooth markers) | Snow on the ground (not supported) |
| **Director Mode** | A take at 50 % record speed with a controller (18 Smart markers); mouse + keyboard | Very long takes, Follow on peds |
| **Editor look** (Neon, fonts, colours, header) | Both themes, fonts, colours and headers, live switching, saved to the ini | Other screen resolutions / UI scales |

## Older features

| Feature | Tested | Not tested yet |
|---|---|---|
| Core crash fix + specific crash fixes | Each built from a real crash; most confirmed on the reporter's own clip | Crashes nobody has reported yet; `ERR_GEN_MAP` hasn't been forced to happen again |
| No seek freeze | One big server, 225+ seeks, no stall | Other servers |
| Free camera (leash, zoom, collision, speed) | Yes | - |
| Cutscene recording + free camera on blocked clips | Yes | Script cameras over a cutscene (known not to work) |
| WR loading screens | Windows 11, windowed borderless | Windows 10, exclusive fullscreen, a second PC |
| Broken-asset report | Yes | - |
| SkipStuckDownloads (experimental, off) | Partly - it can release slow but healthy downloads | Most servers |
| NVE + EVE fixes | Several sessions of 4 exports in a row, no crash | - |

## Known issues

- WR Garage looks and time + weather aren't saved with the project yet.
- A crash while editing some clips with add-on cars
  (`ERR_MEM_EMBEDDEDALLOC_GUARD_1`) can still happen - a guard is in, the cause
  is still being chased.
- Opening a project and then exporting can crash on some clips - restart FiveM
  between big renders.
- The README's "Known issues" section has the full list.

## Help it get tested

Running something from a "not tested yet" column - another game build,
Windows 10, an AMD card, add-on cars, big projects? Tell me how it went on
Discord (https://discord.com/invite/FKJ27bhqfJ), working or not, and send your
`WR Editor Fix\Logs` folder. That's how a "No" turns into a "Yes" here.
