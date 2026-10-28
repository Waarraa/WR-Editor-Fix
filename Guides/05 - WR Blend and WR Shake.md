<!-- MADE BY WR | WARRAA_ -->
# WR Blend and WR Shake - camera paths and camera shake

Two new choices in every marker's Cameras page: **WR blend** for a smooth
camera path that is exactly on time, and **WR shake** for real handheld,
footstep, car and helicopter camera shake. Both look the same in the preview
and in your export, and both are **saved with your project**.

**Game builds:** b3258, b3095 and b3407. **Ini:** none - they're in the editor menu.

> **Tested:** WR blend in preview + EVE export; every WR shake style live; saving + reopening a project (12 marker settings back).
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
   (and, for Custom, **Turn**, **Slide**, **Shiver**, **Steps**).

### The styles

| Style | What it feels like |
|---|---|
| **Handheld** | Someone holding the camera: a slow, natural sway with a tiny tremble, drifts and small corrections, breathing. The classic cinematic look. |
| **Walk** | Carried while walking: a soft bounce on every step, rocking left and right. |
| **Run** | Carried while running: a bigger, faster bounce and more sway. Great for chase shots. |
| **Car** | Mounted on a moving car: a fine road buzz, the odd suspension bump, and the body leaning through turns. |
| **Helicopter** | Filming from a helicopter: a slow floating drift with a fast rotor buzz. |
| **Earthquake** | The ground rolls and jolts, coming in bursts. Turn Strength down for a smaller rumble. |
| **Custom** | Build your own with Turn, Slide, Shiver and Steps. |

### The rows

| Row | What it does |
|---|---|
| **Strength** | How much the camera shakes. 1.0 = the style as made, 2.0 = twice as much, 0.5 = half, 0 = no shake. |
| **Speed** | How fast the camera moves. 100% = the style as made. Lower = calmer, higher = more nervous. |
| **Turn** (Custom) | How far the camera turns and tilts, in degrees. 0.5 = subtle, 1 = natural, 3+ = wild. |
| **Slide** (Custom) | How far the camera drifts up, down and sideways, in cm. 1-3 cm for close-ups, more for wide shots. |
| **Shiver** (Custom) | A fast small vibration on top of the slow sway (engine, wind, nervous hand). 0% = smooth, 100% = only vibration. |
| **Steps** (Custom) | Footsteps: Off, Walk or Run - a bounce on every step and a side-to-side rock. |

### Good to know

- The shake is worked out from the clip's time, so it's **identical every
  time** - in the preview, when you scrub back, and in the export.
- With a blend between two markers, the shake **fades** from one marker's shake
  into the next one's.
- A marker you switch to WR starts with the settings you used last.
- The marker's stock shake stays None underneath.

## Saved with your project

Every marker's WR blend and WR shake is written to
`WR Editor Fix\Projects\<project name>.json` (next to the `.asi`) right after
you change it, and comes back when you open the project again.

- Clips are recognised by their recording, so trimming, moving or deleting
  other clips in the project doesn't move the settings to the wrong clip.
- The file is plain JSON, one line per marker - you can back it up or delete
  it.

## Limits

- WR blend: free camera markers only (attached / look-at: stock Smooth).
- Game builds b3258, b3095 and b3407.
