<!-- MADE BY WR | WARRAA_ -->
# Crash Fixes and Reports - what's fixed, and what to send

WR Editor Fix started as one crash fix and still is one first. This guide
explains what the crash fixes do, the switches, the reports it writes for you,
and exactly what to send when something still crashes.

> **Tested:** Every fix is built from a real crash; most were confirmed on the reporter's own clip (the README says which ones weren't forced to happen again, like `ERR_GEN_MAP`). NVE: several sessions of 4 exports in a row; the editor-only switch-on on b3258, b3095 and b3407 (the WR testers, v1.1.0).
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
car part's list looped back on itself, and the NVE export freeze. The README's Features list names each one.

**It does not remove 100% of editor crashes.** Most crashes come from one
server's broken custom files, so a fix for one server's crash often does
nothing for another's. Fixes get built crash by crash, from real reports.

## Only inside the editor (since v1.1.0)

Nothing is written into the game until the Rockstar Editor opens. At FiveM
start the plugin only reads its `.ini`, shows the WR loading screens and
waits. The crash fixes, the safety net and the editor tools switch on when
the editor opens:

- **From FiveM's main menu:** they switch on while the editor loads.
- **From a server (ESC -> Rockstar Editor):** they switch on as soon as the
  editor's menu is up - before any clip loads, so a clip load that crashes
  there is caught too.
- **While you play on a server:** nothing is switched on.
- **Joining a server after you used the editor:** everything is switched off
  again and the game's own code is put back. Opening the editor again in
  that same FiveM run stays off - restart FiveM to edit again.

The only exception is `[Recording] AllowCutsceneRecording` (opt-in, off by
default): recording happens while you play, so it can't wait for the editor.

### What the log says

| Line | Means |
|---|---|
| `[EditorGate] waiting - nothing is written into the game until the Rockstar Editor opens ...` | FiveM started, nothing switched on yet |
| `[EditorGate] server connect - nothing armed while you play ...` | You joined a server first - nothing is on while you play |
| `[EditorGate] the Rockstar Editor is open (...) - WR Editor Fix arms its editor tools now.` | The editor opened; the reason in brackets says how it was noticed |
| `[EditorGate] editor tools armed.` | The crash fixes and the editor tools are on |
| `[EditorGate] server connect AFTER the editor - disarming every editor tool ...` then `[EditorGate] disarmed.` | You joined a server after editing - everything is off again |
| `[EditorGate] the Rockstar Editor opened again after a server connect - WR Editor Fix stays OFF ...` | Restart FiveM to use the editor tools again |

No `editor tools armed.` line while you were in the editor? Send the log -
that's a bug.

## The switches - `[Crash Fix]` (need a relaunch)

| Key | What it does |
|---|---|
| `ExceptionHandler = 1` | The core crash fix. Leave it on. |
| `InlineGuards = 1` | Extra checks placed right at the known crash spots. Recommended. |
| `WholeGameProtection = 1` | 1 = the safety net watches all game code (best). 0 = only the editor's own code (b3258). It only works while the Rockstar Editor is open, either way - never while you play (since v1.1.0 it isn't even installed before the editor opens). |
| `GrowStreamingList = 1` | Adds room to the game's streaming lists when they run full (`ERR_STR_INFO_2` / `_3`, `ERR_GEN_MAP`). Only while the Rockstar Editor is open. |
| `NveExportFreezeFix = 1` | No "FiveM has stopped responding" when an export starts with NVE. Only active while NVE.asi is loaded. |
| `EmptyNameLookupFix = 1` | Fixes an export crash on a clip with an item that has no name. |

**Removed (safety - switched off in v1.0.1, code removed in v1.1.0):**
- `[Vehicle Meta] SkipBrokenVehicleMeta` - it changed a piece of FiveM's own
  code and ran while you played.
- `[Stuck Downloads] ReportStuckDownloads` / `SkipStuckDownloads` (and
  `[Logging] BrokenAssetsReport`) - they worked through FiveM's streaming code
  while you played.

## The reports it writes for you

All next to the `.asi`, in the `WR Editor Fix` folder:

| File | What's in it |
|---|---|
| `Logs\WR_Editor_Fix.log` | Everything the plugin did this session, your game build, what was caught. You can keep it open in a log viewer while you play - it keeps writing. |

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
3. **The whole `WR Editor Fix\Logs\` folder** - save it before you start FiveM again.

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
