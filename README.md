# WR Editor Fix

**Version: v0.4.0**

Discord: https://discord.com/invite/FKJ27bhqfJ  |  YouTube: https://www.youtube.com/@Warraa__

A FiveM `.asi` plugin that fixes the Rockstar Editor crashing when a clip
references a custom asset (vehicle / MLO / prop / ytyp) that got unloaded,
plus a few optional quality-of-life tweaks for the editor's free camera -
and, new in v0.4.0, your own colours and font for the editor's menus.

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

If you hit a crash this doesn't catch, see **"Found a new crash?"** near the
bottom — I do want to know about it and will try to fix it.

## What it fixes

The Rockstar Editor crashes when it tries to read a custom asset that's
already been unloaded from memory (a freed pointer read). This plugin
catches that specific crash pattern safely and lets the editor keep running
instead of closing. A prevented crash may make a custom prop look missing
in the editor **preview only** — your recorded clips and exports are
unaffected.

## Features (v0.4.0)

**Crash fix — on by default:**
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

**Experimental, off by default — `[Vehicle Meta] SkipBrokenVehicleMeta`:**
- For servers that ship a vehicle with a broken `carvariations`/`handling`
  file. Symptom: clips play fine but the moment one using that car is added
  to a project the editor hangs and dies with "Out of game memory". Turn
  this on and the plugin remembers any vehicle file the game itself reports
  as malformed and skips it from then on (saved in `WR_BrokenVehicleMeta.txt`).
  It learns on the first failure, so the very first attempt can still crash
  once - relaunch and it's skipped.

**Editor free camera — on by default, each independently toggleable:**
- Remove the distance leash that pulls the free-cam back when it flies far
  from the subject (custom max distance).
- Uncap the zoom/FOV range past the stock ~10-100° (up to 1-130°).
- Disable free-cam collision with world geometry.
- Scale the free-cam's move speed (adjustable multiplier, updates live
  while flying — no relaunch needed).

**New in v0.4.0 — Editor Theme, off by default — `[Editor Theme]`:**
- **Colours:** `MenuText` recolours the menu labels, values and the
  timeline playhead; `MenuTextGreyed` recolours greyed-out rows, the
  timeline's played region and the second timecode. Plain `RRGGBB` hex
  (`E01234` = WR red). Applied only while the editor is open and put back
  the moment you leave it, so the rest of the game's UI is never changed.
  Hot-reloads - edit, save, see it within a second.
- **Font:** `EditorFont` swaps the editor's UI font for one of the game's
  own built-in fonts:
  - `Font5` - handwriting / script
  - `Font2_cond` - condensed
  - `RockstarTAG` - all caps (a few symbols like `%` `.` `:` are missing)
  - `gtaCash` - Pricedown, the GTA logo font
  - empty / `Font2` - stock

  Needs a FiveM relaunch after changing it. The Rockstar Editor's own
  main menu (the project list) keeps the stock font for now - everything
  inside the editor gets the new one.

## Known issues / what's being worked on

- **On very heavy servers, editing a clip and then exporting in the same
  session can still crash on export** (`alabama-twenty-hawaii`,
  `GTA5_b3258.exe+600FB30`). Leaving the edit screen makes the game reload
  its replay content, and on some servers that reload trips over a freed
  object. Workaround that works today: edit and save your project, relaunch
  FiveM, open the already-edited clip and export it without editing again.
  Actively being investigated - the cause is now understood, the safe fix
  isn't finished.
- An experimental fix for the editor hanging on "Downloading assets" is
  now exposed in the config (`[Stuck Downloads]`), off by default. Less
  battle-tested than the core crash fix above — only turn it on if you
  actually hit that infinite hang.

## What might come in future updates

No promises on timing — solo project, worked on as time allows:
- More of the editor themeable: the selected-row highlight, headers,
  timeline strip colours, and the new font on the editor's main menu too.
- A fix for the vehicle-data crash mentioned above, if a safe one is found.
- Camera roll/tilt control unlock.
- Export resolution/framerate unlock.
- Camera position/speed presets (bookmarks).
- Auto-save while editing, so a crash never loses your work.

Check back on this repo for updates — new versions will be numbered v0.4.0,
v0.5.0, and so on as they ship. Full version history: `CHANGELOG.md`.

## Install

1. Download `WR_Editor_Fix.asi` and the `WR Editor Fix` folder (with its
   `.ini` inside) from this release.
2. Copy **both** into your FiveM `plugins` folder:
   `%LOCALAPPDATA%\FiveM\FiveM.app\plugins\`
3. Relaunch FiveM.

That's it — everything in the `.ini` is already on by default. Open
`WR_Editor_Fix.ini` if you want to turn anything off or adjust it.

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
`[Editor Camera]` section and the `[Editor Theme]` colours reload live
while FiveM is running — edit, save, and it applies within a second, no
relaunch needed. Everything else (including `EditorFont`) needs a relaunch
to take effect.

## A heads-up about antivirus / Windows Defender

This plugin works by reading and patching the game's own memory at runtime
(the same category of technique every `.asi` crash-fix/mod uses). Some
antivirus software flags this behavior heuristically even when nothing
malicious is happening. If it gets quarantined or blocked, you may need to
add an exclusion for it. Use your own judgement — only download this from
the official release page.

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

YouTube: https://www.youtube.com/@Warraa__

## Disclaimer

Not affiliated with or endorsed by Rockstar Games, Take-Two Interactive, or
Cfx.re. Use at your own risk.

## License

Closed source. You're free to download and use this for personal or server
use. Do not redistribute, resell, decompile, or repackage it. Source is not
published.

Third-party components used are credited in `THIRD-PARTY-NOTICES.txt`.
