<!-- MADE BY WR | WARRAA_ -->
# WR Automate - the editor builds the camera edit for you

Pick what to follow, press Automate, and WR Automate places the markers,
the cameras, the camera paths and the shakes for the whole clip. The car stays
centred on screen and the cameras stay clear of walls, cars, peds and props.
With **Beat Sync** it cuts on the beat of your own song. Everything it makes
is normal editor markers - you can change any of it afterwards.

**Game builds:** b3258, b3095 and b3407. **Ini:** `[WR Automate]`
(`Enabled = 1` shows the WR Automate and Clear Timeline rows).

> **Tested:** Open-road, city and drift / donut clips (calm follow), Follow = Main car, Style = Mixed, WR Blend and Hard Cut, the Distance and Height rows, Checks On, Beat Sync with mp3 songs (Cut every Bar) and the song playing in the editor - on b3258, b3095 and b3407.
>
> **Not tested yet:** Follow = Main ped, Style = Orbit / Chase on their own, Length = Timeline, Checks = Ground only, every Hard Cut option combination, very long clips, projects with several clips, other song formats (wav / m4a / flac / wma use the same Windows decoders).
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## How to use it

1. Record a clip with your car driving (it works best on a fresh clip, right
   after recording).
2. Open the clip in the editor, select a marker, go to **WR Options** ->
   **WR Automate** (Enter).
3. Set the rows (below), then select **Automate** and press **Enter**.
4. Watch the help line: the clip plays through while WR Automate scouts the
   car's path, then the markers appear.
5. Then it plays the clip again to check every camera for obstacles and moves
   the ones that hit something. The help line says when it's finished.
6. Press **Play**. Change anything you like - every marker is yours to edit.

**Back** stops it while it scouts. If the clip already has your own markers,
the first Enter asks first - press Enter again to replace them.

## The rows

| Row | Values | What it does |
|---|---|---|
| **Follow** | Main car / Main ped | Main car = the car the recorded player drives. Main ped = the recorded player. |
| **Length** | Whole clip, Timeline, 5 - 60 s | Whole clip; **Timeline** = exactly the start + end markers as you set them (trim the timeline first); or seconds from the clip's start (only lengths shorter than the clip show). With a Music song: the song section is the length. |
| **Markers** | 3 - 30 | How many markers, spread evenly. More = more camera moves. With a Music song: "On the beat". |
| **Style** | Mixed / Orbit / Chase | Mixed: sweeps round to the sides and the front. Orbit: circles the car the whole way. Chase: stays behind it, swinging up high. |
| **Shake** | Auto / Off / Handheld / Walk / Run / Car / Helicopter / Earthquake | Auto = a shake that fits each shot (Car, Helicopter on high shots, Handheld on the sides). A preset = that shake on every marker. |
| **Distance** | Mixed, 2, 3, 4, 5, 6, 8, 10, 12, 15, 20, 30 m | How far the cameras stay from the car / ped. Mixed = every shot its own (close low fronts, wide high rears, extra room for donuts). A car keeps at least 4 m. |
| **Height** | Mixed, Low (0.3 m), 1, 2, 3, 5, 8, 12, 20 m | How high the cameras fly over the real ground. 12 / 20 m = drone shots. |
| **Checks** | On / Ground only / Off | On: cameras that would touch or look through things are moved - near your Distance / Height. Ground only: just never under the ground. Off: exactly your Distance / Height. |
| **Blend / Cut** | WR Blend / Hard Cut | WR Blend: the camera glides from marker to marker. Hard Cut: every marker cuts to its own camera - its options show up below. |
| **- Follow Car** | On / Off | Hard Cut: each cut's camera rides along with the car. Off = a tripod, placed so the cut shows the car (front: it drives up to the camera, rear: drives away). |
| **- New Angle** | On / Off | Hard Cut: every cut a different side, in a random order every run - never the same side twice in a row. |
| **- Pan With Car** | On / Off | Hard Cut: the camera keeps turning toward the car. Off = a fixed view the car drives through. |
| **Music** | Off / a song | **Beat Sync** - see below. Enter opens the Music page. |
| **Automate** | Enter | Starts it. |

The page remembers your values: they are saved into `[WR Automate]` in the
`.ini` and the next launch starts with them.

## Beat Sync - cut on the beat of your song

1. Drop songs into `plugins\WR Editor Fix\Music\` (mp3, wav, m4a, flac, wma) -
   the folder comes with the release.
2. WR Automate -> **Music**: left / right picks a song. Enter opens the
   **Music page**:

| Row | What it does |
|---|---|
| **Song** | The songs in the Music folder - drop new ones in any time. Enter = read the folder again. |
| **Start** | Where the song section starts (on a bar) - the video starts with it. |
| **End** | Where the section ends - the video is as long as the section. |
| **Cut every** | Beat / 2 beats = fast cuts, Bar (4 beats) = a good start, 2 / 4 bars = calm. WR Blend arrives on the beat, Hard Cut cuts on it. |
| **Volume** | How loud the song plays in the editor when you press Play after Automate (Off = silent). |

The help line shows the song's BPM, its bars and its drop, and how long your
section is.

3. Back to WR Automate -> **Automate**. The markers land on the beat and the
   video is exactly as long as the song section.
4. Press **Play**: the song plays in the editor in sync with the cuts.

**The export has no song in it** (on purpose - you add the music in your video
editor). Every run writes an **edit sheet** to `Music\Edits\` (a `.txt` and a
`.json`): the song, its BPM, the drop, the section you used (start + end, in
your video editor's hh:mm:ss.mmm) and every marker's song time - crop the song
to that section in Vegas / Premiere and it lines up with the cuts.

## What it makes

- **Its own markers** between the clip's start and end markers.
- **A free camera on every marker** from a ring of cinematic shots around the
  car: chase, high rear quarters, sides, low front quarters, front.
  Neighbouring shots follow each other, so the camera orbits smoothly instead
  of jumping.
- **WR blend** on every marker (smooth on-time camera path, see
  `05 - WR Blend and WR Shake.md`) - or **hard cuts** - and the shake you picked.
- **The car centred on screen** the whole time.
- **Calm follow**: when the car drifts or does donuts, the cameras sit around
  the middle of the move and follow it slowly instead of shaking with every
  spin. Straight driving is followed normally.

## Obstacle checks

After placing the markers, WR Automate runs along the clip again with the
game's own camera collision test. Any camera that would touch or look through a
car, ped, prop or wall is pulled in, lifted, or swung round the car, and the
check runs again (up to 6 passes) until the path is clear.

- Close to the ground is fine (down to 20 cm) - low shots still work. Under
  the ground is not.
- With your own Distance / Height the fixes stay near them: blocked view =
  closer at the same height, touching = swing round the car.
- No camera move ever goes through the followed car itself (3 m from a car's
  centre, 1 m from a ped).
- **Checks = Off** (`AvoidObstacles = 0`) skips them: faster, and the cameras
  stay exactly on their planned shots.

## Clear Timeline

WR Options -> **Clear Timeline**, press **Enter twice**: the clip goes back to
a fresh one - every marker gone, the default start and end markers at the full
clip length, every setting default, and the clip's WR blend, WR shake, time +
weather and Car Look gone too. **No undo.**

## Tips

- One car, one clip: WR Automate follows the car the recorded player drives.
  If the player isn't in a car, pick Follow = Main ped.
- Music video in a minute: a song, Cut every Bar, Hard Cut + New Angle.
- Too busy? Fewer markers and Style = Orbit give long smooth moves.
- Drifting? Distance 8 - 12 m and Height 2 - 3 m keep the whole car in frame.
- Want a calmer video? Shake = Off, then add WR shake by hand on a few markers.
- Don't like one shot? Move just that marker's camera - the rest stays.

## Limits

- It follows the player's car or the player, not other cars in the clip (yet).
- The obstacle checks use the world as it streams in; on a very busy server
  a prop that loads late can still get close to a camera.
- The song is for the editor and the edit sheet - it isn't written into the
  export.
