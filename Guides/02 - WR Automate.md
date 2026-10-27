# WR Automate - the editor builds the camera edit for you

Pick what to follow, press Automate, and WR Automate places the markers,
the cameras, the camera paths and the shakes for the whole clip. The car stays
centred on screen and the cameras stay clear of walls, cars, peds and props.
Everything it makes is normal editor markers - you can change any of it
afterwards.

**Game build:** b3258 only. **Ini:** `[WR Automate]` (`Enabled = 1` shows the
WR Automate and Clear Timeline rows).

> **Tested:** An open-road clip and a dense city clip, Follow = Main car, Style = Mixed, the obstacle checks and the 20 cm ground rule.
>
> **Not tested yet:** Follow = Main ped, Style = Orbit / Chase on their own, very long clips, projects with several clips.
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## How to use it

1. Record a clip with your car driving (it works best on a fresh clip, right
   after recording).
2. Open the clip in the editor, select a marker, go to **WR Options** ->
   **WR Automate** (Enter).
3. Set the rows (below), then select **Automate** and press **Enter**.
4. Watch the help line: the timeline starts fresh, the clip plays through
   while WR Automate scouts the car's path, then the markers appear.
5. Then it plays the clip again to check every camera for obstacles and moves
   the ones that hit something. The help line says when it's finished.
6. Play the clip. Change anything you like - every marker is yours to edit.

**Back** stops it while it scouts.

## The rows

| Row | Values | What it does |
|---|---|---|
| **Follow** | Main car / Main ped | Main car = the car the recorded player drives. Main ped = the recorded player. |
| **Length** | Whole clip, 5, 8, 10, 12, 15, 20, 25, 30, 45, 60 s | How long the video is, from the clip's start. Shorter than the clip = the end marker moves there. |
| **Markers** | 3 - 30 | How many markers WR Automate makes between the start and end marker, spread evenly. More markers = more camera moves. |
| **Style** | Mixed / Orbit / Chase | Mixed: sweeps round to the sides and the front. Orbit: circles the car the whole way. Chase: stays behind it, swinging up high. |
| **Shake** | Auto / Off / Handheld / Walk / Run / Car / Helicopter / Earthquake | Auto = a shake that fits each shot (Car, Helicopter on high shots, Handheld on the sides). Off = no shake. A preset = that shake on every marker. |
| **Automate** | Enter | Starts it. |

The page remembers your values: they are saved into `[WR Automate]` in the
`.ini` and the next launch starts with them.

## What it makes

- **Its own markers** between the clip's default start and end markers. The
  default first and last markers are kept as they are.
- **A free camera on every marker** from a ring of cinematic shots around the
  car: chase, high rear quarters, sides, low front quarters, front. Neighbouring
  shots follow each other, so the camera orbits smoothly instead of jumping.
- **WR blend** on every marker (smooth on-time camera path, see
  `05 - WR Blend and WR Shake.md`) and the shake you picked.
- **The car centred on screen** the whole time - the camera looks at the car's
  path every frame, even between markers.

## Obstacle checks

After placing the markers, WR Automate runs along the clip again with the
game's own camera collision test. Any camera that would touch or look through a
car, ped, prop or wall is pulled in, lifted, or moved to a chase spot, and the
check runs again (up to 6 passes) until the path is clear.

- Close to the ground is fine (down to 20 cm) - the camera can still do low
  shots. Under the ground is not.
- `AvoidObstacles = 0` in `[WR Automate]` skips the checks: faster, and the
  cameras stay exactly on their planned shots.

## Clear Timeline

WR Options -> **Clear Timeline**, press **Enter twice**: the clip goes back to
a fresh one - every marker gone, the default start and end markers at the full
clip length, every setting default, and the clip's WR blend, WR shake, time +
weather and Car Look gone too. **No undo.**

## Tips

- One car, one clip: WR Automate follows the car the recorded player drives.
  If the player isn't in a car, pick Follow = Main ped.
- Too busy? Fewer markers and Style = Orbit give long smooth moves.
- Want a calmer video? Shake = Off, then add WR shake by hand on a few markers.
- Don't like one shot? Move just that marker's camera - the rest stays.

## Limits

- Game build b3258 only.
- It follows the player's car or the player, not other cars in the clip (yet).
- The obstacle checks use the world as it streams in; on a very busy server
  a prop that loads late can still get close to a camera.
