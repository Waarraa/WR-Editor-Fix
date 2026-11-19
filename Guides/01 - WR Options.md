<!-- MADE BY WR | WARRAA_ -->
# WR Options - the editor's own WR page

WR Options is where most of WR Editor Fix's editor tools live. It is a page
inside the Rockstar Editor itself, drawn by the game like every other editor
menu.

**Game builds:** b3258, b3095 and b3407. **Ini:** `[Editor Time Weather] MenuRows = 1`
(on by default; `0` removes every WR row from the editor menus).

> **Tested:** Every row, live, and saving back to the ini - Windows 11, on b3258, b3095 and b3407.
>
> **Not tested yet:** Other game builds (the page switches itself off there).
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## How to open it

1. Open a clip in the Rockstar Editor (Edit).
2. Select any marker on the timeline so the marker menu shows.
3. Scroll to the last row, **WR Options**, and press **Enter**.
4. **Back** (Backspace / B on a controller) returns to the marker menu.

The help line under the menu explains the row you are on.

## The rows

Since v1.1.0 WR Options is a list of **categories** - Enter opens one, Back goes
up again. Every page ends with **WR Undo** (`14 - WR Undo.md`) and **Edit Camera**.

| Row | Opens | What's inside |
|---|---|---|
| **WR Time & Weather** | a page | **Hour**, **Minute**, **Weather** (Extra Sunny ... Halloween) for every clip of the project, **Back to Recorded** = back to what each clip was recorded with, **Remove Marker Weather** (Enter twice) = every marker loses its own time & weather. See `06 - Time and Weather.md`. |
| **WR World** | a page | **Road Wetness**, **Car Lights**, **Clean Cars**, **Repair**, **Empty City**, **Tyre Marks** - the world of the clip. See `17 - WR World.md`. |
| **WR Camera** | a page | **Move Speed** (how fast the free camera flies, x0.25 - x20), **Camera Range** (100 - 15000 m), **Map Detail** (Player / Camera), **Up / Down Speed** and **Right / Left Speed** (how fast a controller turns it, 1 - 12). See `09 - Free Camera.md`. |
| **WR Garage** | WR Garage | Tune the clip's car. See `03 - WR Garage.md`. |
| **WR Lights** | WR Lights | Your own lights in the clip. See `15 - WR Lights.md`. |
| **WR Director** | WR Director | Fly the camera live. See `07 - Director Mode.md`. |
| **WR Automate** | WR Automate | The editor builds the camera edit (+ Beat Sync). See `02 - WR Automate.md`. |
| **WR Editor Look** | a page | **Theme** (Default / WR / Custom), **Font**, **Timeline Size**, and on Custom: Base Look, **Header Style**, **Header Motion**, **Colors**; **Language** (27 + Auto), **Quick Menu Key** (`18 - WR Quick Menu.md`), **WR Buddy** + Buddy Position / Size / Hints / Chatty (`19 - WR Buddy.md`). See `08 - Editor Look.md`. |
| **WR Clear Timeline** | - | Puts the clip back to a fresh one. Press Enter twice. Can't be undone. |

Everything changes live: you see it in the preview right away.

## What gets saved, and where

- **Saved back to `WR_Editor_Fix.ini`** (about a second after your last change,
  each into its own line, so the next launch starts with it): Camera Speed,
  Header Style, Header Motion, Font, Colors, Timeline Size, and the WR
  Automate page values.
  Nothing else in the `.ini` is touched.
- **Saved with your project** (`WR Editor Fix\Projects\<project name>.json`): time + weather. Press Default
  to go back to the recorded look.

## WR Marker Options

There is a second WR page per marker: marker menu -> **Cameras** -> **WR Marker
Options** (Enter). It holds the settings that belong to one marker:

- **Time & Weather** for that marker - see `06 - Time and Weather.md`.
- **Car Look** for that marker - see `04 - Car Look per marker.md`.
- **Face Camera** - see below.
- **Freeze** (Matrix Freeze) - see `16 - Matrix Freeze.md`.

### Face Camera

While the marker plays, the camera frames the recorded player's **face** on its own
and follows it - no placing. In a car it becomes a driver cam that rides along with
every drift and bump.

| Value | The shot |
|---|---|
| **Off** | the marker's own camera (default) |
| **Front** | the face from the front, about 1 m away (in a car: from the dashboard) |
| **Close** | a tight close-up, about 0.6 m |
| **Left Side** / **Right Side** | the face in profile (in a car: through the driver's window / from the passenger seat) |
| **Low Hero** | from below, looking up - best for a player on foot (in a car the steering wheel is in the way) |

The marker's WR shake still goes on top (Handheld on a face shot looks great). The
camera cuts in at the marker and cuts to the next marker's camera at the next marker.
Saved with the project.

> **Tested:** b3095, all five styles on a driver in a drifting car (following during playback) and on a player
> standing on foot; b3258 Front on foot.
> **Not tested yet:** b3407 in game.

## Tips

- Lost? The help line always describes the selected row.
- WR Options only appears while a clip is open for editing (not in the
  project list or the clip gallery).
- If the WR rows are missing, check `MenuRows = 1` in `[Editor Time Weather]`
  and that you are on game build b3258, b3095 or b3407 (the log names your
  build).
