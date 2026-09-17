# WR Editor Fix

**Version: v0.2.0**

Discord: https://discord.com/invite/FKJ27bhqfJ  |  YouTube: https://www.youtube.com/@Warraa__

A FiveM `.asi` plugin that fixes the Rockstar Editor crashing when a clip
references a custom asset (vehicle / MLO / prop / ytyp) that got unloaded,
plus a few optional quality-of-life tweaks for the editor's free camera.

## ⚠️ Important — read before you install

**This does not remove 100% of Rockstar Editor crashes.** It fixes the most
common crashes found and confirmed so far. There are almost certainly other
crashes out there that haven't been found yet, or that have been found but
don't have a safe fix yet (see "Known issues" below). Installing this
should mean you crash a lot less, not that you'll never crash again.

If you hit a crash this doesn't catch, see **"Found a new crash?"** near the
bottom — I do want to know about it and will try to fix it.

## What it fixes

The Rockstar Editor crashes when it tries to read a custom asset that's
already been unloaded from memory (a freed pointer read). This plugin
catches that specific crash pattern safely and lets the editor keep running
instead of closing. A prevented crash may make a custom prop look missing
in the editor **preview only** — your recorded clips and exports are
unaffected.

## Features (v0.2.0)

**Crash fix — on by default:**
- Stops the Rockstar Editor crashing when switching, editing, or exporting
  clips that reference a custom asset (vehicle, MLO, prop, ytyp) which got
  unloaded. This is the core fix and covers every known variant of this
  crash found so far.
- Also catches the same crash pattern in FiveM's streaming/asset-unload
  code on heavy custom-asset servers, not just the editor itself.

**Editor free camera — on by default, each independently toggleable:**
- Remove the distance leash that pulls the free-cam back when it flies far
  from the subject (custom max distance).
- Uncap the zoom/FOV range past the stock ~10-100° (up to 1-130°).
- Disable free-cam collision with world geometry.
- Scale the free-cam's move speed (adjustable multiplier, updates live
  while flying — no relaunch needed).

## Known issues / what's being worked on

- **A specific crash tied to malformed custom vehicle data on some heavily
  modded servers** is still being actively investigated. It doesn't happen
  on every server — only ones with broken vehicle-variation files — and no
  safe universal fix exists yet. If you hit a crash exporting a clip on a
  heavily-modded server, this is likely it; a future update may resolve it.
- An experimental fix for the editor hanging on "Downloading assets" is
  now exposed in the config (`[Stuck Downloads]`), off by default. Less
  battle-tested than the core crash fix above — only turn it on if you
  actually hit that infinite hang.

## What might come in future updates

No promises on timing — solo project, worked on as time allows:
- A fix for the vehicle-data crash mentioned above, if a safe one is found.
- Camera roll/tilt control unlock.
- Export resolution/framerate unlock.
- Camera position/speed presets (bookmarks).
- Auto-save while editing, so a crash never loses your work.

Check back on this repo for updates — new versions will be numbered v0.2.0,
v0.3.0, and so on as they ship. Full version history: `CHANGELOG.md`.

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
comment explaining what it does. The `[Editor Camera]` section reloads live
while FiveM is running — edit, save, and it applies within a second, no
relaunch needed. Everything else needs a relaunch to take effect.

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
   - **All** the log files from your `WR Editor Fix` folder (next to the
     `.asi`, in your FiveM `plugins` folder) — `WR_Editor_Fix.log` and any
     other `WR_*.log` files in there.

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
