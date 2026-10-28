<!-- MADE BY WR | WARRAA_ -->
# Car Look per marker - the car changes on a cut

Give a marker its own car look: from that marker on, the car wears it - a new
paint, livery, plate or body kit - until the next marker that has its own.
Great for beat-synced edits where the car changes on every cut.

**Game builds:** b3258, b3095 and b3407. Uses WR Garage's rows - see `03 - WR Garage.md`.

> **Tested:** 5 marker looks in preview playback and in an EVE export - the car switched at every marker.
>
> **Not tested yet:** Projects with several clips.
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## How to use it

1. Select the marker where the new look should start.
2. Marker menu -> **Cameras** -> **WR Marker Options** (Enter).
3. Select **Car Look** (the last row, shows On / Off) and press **Enter**.
   The WR Garage page opens with the title **WR Marker Car Look**.
4. Change any row - paint, livery, plate, Body Parts, Randomise... The first
   row, **Marker Look**, turns **On** by itself: the marker gets its own look,
   starting as a copy of what the car shows there now.
5. **Back** returns to WR Marker Options (Car Look now says On).
6. Repeat on other markers, then play the clip.

## How playback works

- Before the first marker with a car look, the car wears the clip's look
  (WR Options -> WR Garage, or as recorded).
- At a marker with a car look, the car switches to it - a hard cut - and keeps
  it until the next marker that has its own.
- While WR Marker Car Look is open, the car shows the look you are editing.
- The export does exactly the same switches at the same markers.

## The Marker Look row

| Value | Meaning |
|---|---|
| **On** | This marker has its own car look. |
| **Off** | No look of its own - the car keeps the look from before this marker. |

Left / right / Enter on Marker Look switches it. Turning it Off drops the
marker's look. **Reset** on this page means "from this marker on, the car is as
recorded" (the marker look stays On).

## Tips

- Beat-synced car swaps: put markers on the beats, give each one Randomise
  Colors or Randomise All.
- A marker with only a new plate: open Car Look, Plate Text, type, done - the
  rest stays the same as before the marker.
- Night shot halfway through? Car Look with Lights = On on that marker, plus
  time + weather on the same marker (`06 - Time and Weather.md`).

## Limits

- Saved with your project, like WR blend and WR shake: reopen it and every marker's look is back.
- The switch is a cut, not a fade.
- The player's car only.
