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

| Row | What it does | Controls |
|---|---|---|
| **Hour** | The hour every clip in the project plays at. Shows the clip's own recorded hour until you change it. | Left / right |
| **Minute** | The minute of that time. | Left / right |
| **Weather** | The weather every clip plays with: Extra Sunny, Clear, Clouds, Smog, Foggy, Overcast, Rain, Thunder, Clearing, Neutral, Snow, Blizzard, Light Snow, Xmas, Halloween. | Left / right |
| **Default** | Puts time and weather back to what each clip was recorded with. | Enter |
| **Camera Speed** | How fast the editor's free camera flies, x0.25 to x20 (x1.00 = stock). | Left / right |
| **Header Style** | The logo at the top of the editor menu: Stock, WR, Meme, Retro, Cinematic. | Left / right |
| **Header Motion** | Animated or Still (Meme, Retro and Cinematic move). | Left / right |
| **Font** | The font of every editor menu and text: Default (the original) or one of 10 built-in fonts. | Left / right |
| **Colors** | Opens the WR Colors page - every colour of the editor's look. | Enter |
| **Timeline Size** | How big the timeline is: markers, start / end, playhead and the bar's thickness, 50 - 300 % (100 % = the original size). See `08 - Editor Look.md`. | Left / right |
| **WR Garage** | Opens WR Garage - tune the clip's car. See `03 - WR Garage.md`. | Enter |
| **Director Mode** | Opens Director Mode - fly the camera live. See `07 - Director Mode.md`. | Enter |
| **WR Automate** | Opens WR Automate - the editor builds the camera edit. See `02 - WR Automate.md`. | Enter |
| **Clear Timeline** | Puts the clip back to a fresh one. Press Enter twice. No undo. | Enter, Enter |

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

## Tips

- Lost? The help line always describes the selected row.
- WR Options only appears while a clip is open for editing (not in the
  project list or the clip gallery).
- If the WR rows are missing, check `MenuRows = 1` in `[Editor Time Weather]`
  and that you are on game build b3258, b3095 or b3407 (the log names your
  build).
