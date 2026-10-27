# Loading Screens - the WR launch screen and clip screen

Two WR screens replace FiveM's own while the Rockstar Editor opens and while
a clip loads. Both close by themselves the moment the editor is ready.

**Ini:** `[Editor Loading Screen]` (needs a relaunch). Both are on in the
shipped `.ini`.

> **Tested:** Windows 11, windowed borderless, one PC.
>
> **Not tested yet:** Windows 10, exclusive fullscreen, other PCs.
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## The launch screen

Press **Rockstar Editor** + **Yes** in FiveM's main menu and the WR screen
shows at once. It has:

- **The version** you're running.
- **Running now** - what's on in **your** `.ini`: the crash fix, No seek
  freeze, the free camera switches, the camera speed, WR Automate, and your
  editor theme, header and font.
- **Update log** - the newest releases from GitHub, with an **Update
  available** box when a newer version is out.
- **Tips** about WR Editor Fix's features.
- Live load progress.

Double-click it to close it early. It stays out of the way at the main menu
and when you join a server.

## The clip screen

A minimal WR screen while a clip loads (after pressing Edit) or an export
starts, instead of the stock "Preparing clip" screen, with tips that rotate
every few seconds. Double-click to close it.

## The switches

```ini
[Editor Loading Screen]
LaunchScreen = 1            ; the launch screen (0 = FiveM's own)
LaunchScreenTimeoutSec = 300 ; safety cap: closes after this many seconds anyway (30 - 900)
ClipScreen = 1              ; the clip screen (0 = the stock "Preparing clip")
UpdateCheck = 1             ; ask GitHub for the update log (0 = no network request, built-in log)
```

## Requirements

- **Microsoft Edge WebView2 Runtime**: built into Windows 11; on Windows 10 it
  comes with Microsoft Edge. If it's missing, the log says so and FiveM's own
  screens are used.
- Works best with the game in **Windowed Borderless**.

## Windows 10 / something looks wrong

The screens are **tested on Windows 11**. On Windows 10, or if anything looks
wrong while the editor opens (black / white / frozen screen, flickering, the
game minimising, a missing or double mouse cursor), set `LaunchScreen = 0` and
`ClipScreen = 0`. FiveM's own screens come back and **nothing else changes** -
the crash fix and every other feature keep working. Please send your `Logs`
folder on Discord so it can be fixed.

## Known issue

Pressing Export a second time in the same session can show the clip screen a
few seconds late.
