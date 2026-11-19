<!-- MADE BY WR | WARRAA_ -->
# WR Blend and WR Shake - camera paths and camera shake

Two new choices in every marker's Cameras page: **WR blend** for a smooth
camera path that is exactly on time, and **WR shake** for real handheld,
footstep, car, drone and helicopter camera shake - with its own **Shake
Options** page, copy / paste and your own **Shake Presets**. Both look the
same in the preview and in your export, and both are **saved with your
project**.

**Game builds:** b3258, b3095 and b3407. **Ini:** none - they're in the editor menu.

> **Tested:** WR blend in preview + EVE export; every WR shake style live; the Shake Options page, Copy / Paste Shake, Shake Presets (save + load); a WR Export with WR shakes; saving + reopening a project (12 marker settings back).
>
> **Not tested yet:** Attached / look-at markers (they keep Smooth on purpose), trimming / moving clips in a big project.
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## WR blend

### What it fixes

The stock **Smooth** blend lets a spring chase the camera: it always lags
behind the markers, so a camera that should pass a car at the right moment
arrives late, and the move never quite ends where you put it.

**WR blend** passes **every marker exactly at its time**, and its speed flows
smoothly through the markers - no lag, no kick at each marker. Position,
rotation and zoom (FOV) all follow the same path.

### How to use it

1. Select a marker -> **Cameras**.
2. On the **Blend** row, go right past Smooth to **WR**.
3. Do the same on the markers the move should flow through.
4. Play the clip.

The help line on the Blend row explains it while WR is selected.

### Good to know

- WR blend is for **free camera** markers. Markers with an attached or
  look-at camera keep the stock Smooth for now.
- The first and last markers of a WR blend path start and end naturally - the
  camera eases into the curve instead of aiming straight at the next marker.
- WR Automate puts WR blend on every marker it makes.

## WR shake

### How to use it

1. Select a marker -> **Cameras**.
2. On the **Shake** row, go right past Explosion to **WR**.
3. New rows appear below it: **WR Shake** (the style), **Strength**, **Speed**
   and **Shake Options** (Enter opens the page below).

Up / down picks a row, left / right changes it, Enter opens / runs, Back goes
one page back. The help line under the menu explains the row you're on.

### The styles

| Style | What it feels like |
|---|---|
| **Handheld** | Someone holding the camera: a slow, natural sway with a tiny tremble, drifts and small corrections, breathing. The classic cinematic look. |
| **Walk** | Carried while walking: a soft bounce on every step, rocking left and right. |
| **Run** | Carried while running: a bigger, faster bounce and more sway. Great for chase shots. |
| **Car** | Mounted on a moving car: a fine road buzz, the odd suspension bump, and the body leaning through turns. |
| **Helicopter** | Filming from a helicopter: a slow floating drift with a fast rotor buzz. |
| **Earthquake** | The ground rolls and jolts, coming in bursts. Turn Strength down for a smaller rumble. |
| **Drone** (new) | A drone hanging in the air: a soft, gimbal-steady float with a slow drift and turn. |
| **Boat** (new) | On the water: the swell rolls and pitches the camera over seconds, with the odd wave slap. |
| **Shoulder Rig** (new) | A pro camera on the shoulder: heavier and steadier than Handheld, a slow weighty drift and breathing. |
| **Motorbike** (new) | Mounted on a bike: a hard engine buzz, a rough road and deep leans through the turns. |
| **Combat** (new) | An operator under stress: nervous hand-held, quick reframes and sudden jolts like nearby hits. |
| **Custom** | Build your own with Turn, Slide, Shiver and Steps on the Shake Options page. |

### The Cameras page rows

| Row | What it does |
|---|---|
| **WR Shake** | The style (table above). |
| **Strength** | How much the camera shakes. 1.0 = the style as made, 2.0 = twice as much, 0.5 = half, 0 = no shake. (0 - 5.0) |
| **Speed** | How fast the camera moves. 100% = the style as made. Lower = calmer, higher = more nervous. (10% - 500%) |
| **Shake Options** | Enter: the WR Shake Options page. |

A marker you switch to WR starts with the style, Strength and Speed you used
last. Everything on the Shake Options page starts clean (normal).

## WR Shake Options

Cameras -> **Shake Options** (Enter). Everything for this marker's shake on
one page.

**Custom only** (the first four rows):

| Row | What it does |
|---|---|
| **Turn** | How far the camera turns and tilts, in degrees. 0.5 = subtle, 1 = natural, 3+ = wild. |
| **Slide** | How far the camera drifts up, down and sideways, in cm. 1-3 cm for close-ups, more for wide shots. |
| **Shiver** | A fast small vibration on top of the slow sway (engine, wind, nervous hand). 0% = smooth, 100% = only vibration. |
| **Steps** | Footsteps: Off, Walk or Run - a bounce on every step and a side-to-side rock. |

**Every style:**

| Row | What it does |
|---|---|
| **Variation** | The same style, moving differently. Two markers with the same style and another Variation never move alike. 1 = the style as made. (1 - 99) |
| **Fade In** | Seconds after this marker until the shake is at full strength - it starts from still. Off = the full shake right away. (0 - 10 s) |
| **Fade Out** | Seconds before the **next** marker over which the shake calms down to nothing. Off = it keeps going. (0 - 10 s) |
| **Impact** | A one-shot kick right at this marker: the camera drops, nods and springs back - a bump, a landing, a hit. Great on cuts. Off = none. (0 - 5.0) |
| **Zoom** | Zoom shake, in the editor's zoom levels (1.00x = normal, higher = more zoomed in). Enter: Off -> In -> Out -> Mixed. See "Zoom shake" below. |
| **Level Horizon** | On = the shake never tilts the horizon (no roll). Off = the style as made. |
| **Copy Shake** | Enter: copies this marker's whole shake - style, Strength, Speed and everything on this page. |
| **Paste Shake** | Enter: puts the copied shake on this marker (replaces its shake). Shows the copied style. |
| **Apply To All Markers** | Enter **twice**: puts this marker's shake on every camera marker of the clip. Their own WR shakes are replaced; markers with a stock shake keep theirs. **No undo.** |
| **Preset** | Your saved shakes. Left / right: pick one. Enter: put it on this marker (replaces its shake). |
| **Save Preset** | Enter: this marker's whole shake is saved as a new preset ("My Walk 1", "My Walk 2" ... after the style) - rename the .json in `WR Editor Fix\Shake Presets\` to give it your own name. |
| **Reset Options** | Enter: everything on this page back to normal. The style, Strength and Speed stay. |

### Zoom shake

- **In**: the zoom wanders between the marker's own zoom and the level you
  pick with left / right, zooming in.
- **Out**: the same, zooming out.
- **Mixed**: the zoom wanders anywhere between **0.70x and 2.00x**.
- Left / right picks the In / Out level, from **0.45x to 50x**.
- Speed changes how fast the zoom wanders too.

### Copy + paste to other markers (the fast way)

1. Marker A -> Cameras -> Shake Options -> **Copy Shake**.
2. Go to marker B. If its Shake is None, its Cameras page now shows a **Paste
   Shake** row right under Shake - Enter turns WR shake on, with the copy.
   (Marker B already on WR? Use Paste Shake on its Shake Options page.)

A marker with a **stock** shake (Handheld, Drunk ...) can't take a paste - set
its Shake to None first.

### Shake Presets

Every preset is one file:
`FiveM.app\plugins\WR Editor Fix\Shake Presets\<name>.json`

- The file name is the preset's name. Names: letters, digits, space and
  `- _ ( ) . +` (up to 32 characters).
- A preset holds the style, Strength, Speed and every Shake Options value.
- Copy, rename or delete them in Explorer - the list is read again every time
  you open Shake Options.
- Share a preset = send the `.json` file.

### Good to know

- The shake is worked out from the clip's time, so it's **identical every
  time** - in the preview, when you scrub back, and in the export.
- With a blend between two markers, the shake **fades** from one marker's shake
  into the next one's.
- With motion blur in WR Export, the very fast part of a shake (the Car /
  Motorbike buzz, Shiver) gets softer - the blur averages it out. That's
  normal.
- The marker's stock shake stays None underneath.
- The Shake Options page of a Custom marker is full (16 rows - the editor's
  limit).

## Saved with your project

Every marker's WR blend and WR shake (every Shake Options value too) is
written to `WR Editor Fix\Projects\<project name>.json` (next to the `.asi`)
right after you change it, and comes back when you open the project again.
Project files from older versions load as before.

- Clips are recognised by their recording, so trimming, moving or deleting
  other clips in the project doesn't move the settings to the wrong clip.
- The file is plain JSON, one line per marker - you can back it up or delete
  it.

## Limits

- WR blend: free camera markers only (attached / look-at: stock Smooth).
- Game builds b3258, b3095 and b3407.
