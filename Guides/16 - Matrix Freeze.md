<!-- MADE BY WR | WARRAA_ -->
# Matrix Freeze - stop time, keep the camera moving

The bullet-time shot: at a marker the whole world **stops** (the car mid-drift, the
smoke in the air, the other cars, the people) while the camera keeps flying round the
frozen moment. Then the clip plays on from exactly where it stopped.

**Where:** a marker's **Cameras -> WR Marker Options -> Freeze**. **Editor only:** it
works in the Rockstar Editor, never in a game or on a server.

> **Tested:** b3095 + b3258; Freeze 2 s - every Freeze Camera move in the preview; in WR Export videos Orbit Left and Still on b3095 (29.97 fps, with and without motion blur 8 samples) and Push In on b3258 (a freeze right at the clip start); Freeze Sound Mute and Hold; the freeze saved with the project and back after a restart; the sound after the freeze in sync with the picture.
>
> **Not tested yet:** b3407 in game; several freezes in one clip; projects with several clips; 60 fps exports.

## How to turn it on

There is no switch in the ini - the freeze is a setting **per marker**:

1. Open a clip and go to the **marker** where time should stop (no marker there yet?
   Press **M** during playback to add one).
2. In the marker menu open **Cameras**, scroll down to **WR Marker Options** and press
   **Enter**.
3. Go down past the Time & Weather and Car Look rows to **Freeze** and pick a length
   with **Left / Right** (0.5 - 5 s of video). **Off** = no freeze at this marker.
4. As soon as Freeze is on, two more rows appear right under it:
   **Freeze Camera** (the camera move) and **Freeze Sound** (the sound).
5. Press **Enter** on any of the Freeze rows: the camera move plays right there as a
   preview.
6. Export with **WR Export**. The freeze is only in the WR Export video, and the video
   gets longer by it: a 2 s freeze on an 18.6 s clip = a 20.6 s video.

**Quick first try:** a drift moment, **Freeze 2 s + Orbit Right**, then export.

## The rows

| Row | Values | What it does |
|---|---|---|
| **Freeze** | Off / 0.5 / 1 / 1.5 / 2 / 3 / 4 / 5 s | How long the world stands still at this marker, in seconds of video. Enter = preview the camera move. |
| **Freeze Camera** | Orbit Left / Orbit Right / Orbit Close / Arc / Push In / Still | **Orbit**: one full circle round the car or the player (whichever is nearer the camera), back exactly where it started. **Orbit Close**: the circle spirals in to about half the distance and back out. **Arc**: swings about 50 degrees out to the side and back. **Push In**: moves straight in to about half the distance and back. **Still**: a freeze frame, the camera stops too. |
| **Freeze Sound** | Mute / Hold | The game makes no sound while time stands still. **Mute**: the sound fades out, silence, then it comes back right where it stopped. **Hold**: the last moment's sound hangs in the air and slowly fades - the classic time-stop sound. |

## Good to know

- **Only in WR Export videos.** The editor's normal playback runs on real time and
  plays straight through a freeze - use Enter on the Freeze row to see the camera
  move. EVE or the game's own export don't freeze.
- **Motion blur works with it**: the frozen world stays sharp and the orbiting camera
  smears it like a real camera move. That's the look.
- **Every camera move ends where it started**, so the clip carries on after the
  freeze with no jump.
- **The orbit keeps clear** of walls, buildings, tree trunks, cars and props: where
  one is in the way, the camera comes in closer round the car instead of flying
  through it.
- **Trees and bushes**: GTA gives tree crowns, bushes and leaves no collision, so
  nothing can see them. If the preview shows the orbit going through a tree, switch
  to **Orbit Right** or **Arc**, or move the marker's camera closer to the car.
- A wide drone shot makes a big orbit. For a classic bullet-time look, set the
  marker's camera 4 - 8 m from the car first.
- The freeze is saved with the project (`WR Editor Fix\Projects\<project>.json`,
  `"freeze"`, `"freezeCam"`, `"freezeSound"`) and comes back when you load it.

## Limits

- One freeze per marker; a clip can have as many as it has markers.
- With motion blur the game's sound comes out too long anyway (see WR Export), so
  Freeze Sound only applies to exports without motion blur.
- The preview shows the camera move only: the world doesn't stop in the editor's
  playback.
