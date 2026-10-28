<!-- MADE BY WR | WARRAA_ -->
# Crash Fixes and Reports - what's fixed, and what to send

WR Editor Fix started as one crash fix and still is one first. This guide
explains what the crash fixes do, the switches, the reports it writes for you,
and exactly what to send when something still crashes.

> **Tested:** Every fix is built from a real crash; most were confirmed on the reporter's own clip (the README says which ones weren't forced to happen again, like `ERR_GEN_MAP`). NVE + EVE: several sessions of 4 exports in a row.
>
> **Not tested yet:** Crashes nobody has reported yet; game builds other than b3258, b3095 and b3407.
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## What the crash fix does

The Rockstar Editor crashes when it reads a custom asset (vehicle, MLO, prop,
ytyp) that the server already unloaded. The plugin catches that crash pattern
safely and lets the editor keep running. A prevented crash may make a custom
prop look missing in the editor **preview only** - your recorded clips and
exports are fine.

On top of that it fixes many specific crashes found from real logs and dumps:
exports on heavy servers (`ERR_STR_INFO_2` / `_3`, `ERR_GEN_MAP`), clips with a
ped whose body never loaded, duplicate map archetypes, loading a second clip,
clips with more than 32 players, items with no name, the game's clean-up
walking a list that was never set up (`yankee-alpha-may`), a freeze when a
car part's list looped back on itself, and the NVE + EVE export freeze and
ReShade `.addon` crash. The README's Features list names each one.

**It does not remove 100% of editor crashes.** Most crashes come from one
server's broken custom files, so a fix for one server's crash often does
nothing for another's. Fixes get built crash by crash, from real reports.

## The switches - `[Crash Fix]` (need a relaunch)

| Key | What it does |
|---|---|
| `ExceptionHandler = 1` | The core crash fix. Leave it on. |
| `InlineGuards = 1` | Extra checks placed right at the known crash spots. Recommended. |
| `WholeGameProtection = 1` | Guards the whole game, not only the editor code - also catches the same bug in the streaming / asset-unload code on heavy servers. 0 = editor code only. |
| `GrowStreamingList = 1` | Adds room to the game's streaming lists when they run full (`ERR_STR_INFO_2` / `_3`, `ERR_GEN_MAP`). |
| `NveExportFreezeFix = 1` | No "FiveM has stopped responding" when an EVE export starts with NVE. Only active while NVE.asi is loaded. |
| `EveSwapChainFix = 1` | Fixes NVE's ReShade `.addon` crashing a few seconds after launch with EVE. |
| `EmptyNameLookupFix = 1` | Fixes an export crash on a clip with an item that has no name. |

Plus `[Vehicle Meta] SkipBrokenVehicleMeta = 1` (on in the shipped `.ini`):
the plugin remembers any vehicle file the game reports as malformed and skips
it from then on (`WR_BrokenVehicleMeta.txt`; delete it to forget everything
learned). The first attempt can still crash once - relaunch and it's skipped.
That vehicle may lose its custom colours / kits in the preview only.

And `[Stuck Downloads]`: `ReportStuckDownloads = 1` (on) lists server downloads
that never finish; `SkipStuckDownloads = 1` (experimental, off) releases them
when the editor hangs forever on "Downloading assets". It only acts inside the
editor - while you play on a server it only reports.

## The reports it writes for you

All next to the `.asi`, in the `WR Editor Fix` folder:

| File | What's in it |
|---|---|
| `Logs\WR_Editor_Fix.log` | Everything the plugin did this session, your game build, what was caught. |
| `Logs\WR_BrokenAssets.log` | Server downloads that never finished: resource + file. A list to send to your server owner (`[Stuck Downloads] ReportStuckDownloads = 1`). |
| `WR_BrokenVehicleMeta.txt` | Broken vehicle files the plugin learned to skip. |
| `Dev Logs\` | Only appears when a specific crash shape is caught - the most useful thing you can send. |

## Broken files on the server - I can't fix those

If your logs name a broken server file (a download that never finishes, a
broken `vehicles.meta` / `carvariations.meta`, a broken map / MLO / ytyp /
ymap), that file has to be fixed by the **server owner / developer**. Send them
the log and the file name. If the editor still crashes after they fixed it,
send me the new logs.

## Found a new crash? What to send

**Please use Discord, not GitHub Issues** - https://discord.com/invite/FKJ27bhqfJ
(contact **Warraa_**, open a support ticket). Send:

1. **The crash dump** - the `.zip` FiveM saves when it crashes (the crash
   window tells you where, and has a copy-to-upload option).
2. **A screenshot** of the crash window.
3. **Everything in `WR Editor Fix\Logs\`**.
4. **Everything in `WR Editor Fix\Dev Logs\`**, if that folder exists.

The more of that you send, the faster it can be fixed - missing logs usually
mean the crash can't be reproduced.

## Game builds

Everything is built and tested on game builds **b3258, b3095 and b3407** -
the build-specific crash fixes are matched to each of the three. The plugin
loads on every game build FiveM supports and the log names yours, but on
other builds some fixes may not apply and the editor tools switch
themselves off. Your logs and dumps are what gets other builds working.

## Windows Defender says "Trojan"?

A false positive - the plugin patches the game's memory while it runs (like
every `.asi`), and the file is new and unsigned. Only download it from the
official GitHub release or the Discord. If Defender removed it: Windows
Security -> Virus & threat protection -> Protection history -> the entry ->
Actions -> Restore / Allow on device. The README has the details.
