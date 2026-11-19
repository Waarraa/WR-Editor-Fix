<!-- MADE BY WR | WARRAA_ -->
# WR Lights - your own lights in a clip

Light up a night scene the way a film crew would: add point lights, spot lights
and **searchlights** anywhere in a clip, colour them, give them a visible beam in
the air, let them ride with the camera, the player or their car, and switch them
on / off at markers. What you see in the editor is what the export gets - beams
included.

**Where:** WR Options -> **WR Lights**. **Editor only:** the lights exist only in
the Rockstar Editor, never in a game or on a server.

> **Tested:** b3095; point / spot / searchlight; colour, brightness, range, cone, shadows, fog beam; attach to World / Camera / Player / Car; Show From / Until with fades; Light Presets; beams in WR Export videos.
>
> **Not tested yet:** b3258 / b3407 in game (the game functions it uses are found and cross-checked on all three builds); many (10+) lights with shadows at once - the game shadows at most 8 lights at a time.

## How to use it

1. Open a clip in the editor, then **WR Options -> WR Lights**.
2. **Add Light**: a new light appears where the camera is, pointing where it looks.
3. The light's own page opens - set it up (rows below). Changes show right away.
4. Back on WR Lights, every light of the clip is listed (`Light 1 - On - Warm Spot, Car`).
   Enter on one opens its page again.

Tip: lights shine much better at night. Set the time on **WR Options -> WR Time &
Weather** (e.g. Hour 01) while you place them.

## The light's rows

| Row | Values | What it does |
|---|---|---|
| **Type** | Point / Spot / **Searchlight** | Point = shines all around like a bulb. Spot = a cone of light in one direction. **Searchlight** = a spot that sweeps around where you aimed it **on its own**, like a police helicopter's light. |
| **Colour** | Warm, White, Cool, Sunset, Red, Orange, Yellow, Green, Cyan, Blue, Purple, Pink, WR Red | The light's colour. |
| **Brightness** | 1 - 200 % | 100 % = a strong lamp. Night scenes need far less - 20 - 50 % for a soft fill. |
| **Range** | metres | How far the light reaches. Things past it get none of it. |
| **Cone** | 10 - 80 deg (Spot / Searchlight) | 10 = a narrow beam, 80 = a wide flood. |
| **Shadows** | Off / On | Things in the light cast shadows (the game shadows at most 8 lights at a time - a bigger Range helps a light win one). |
| **Fog Beam** | Off / Low / Medium / High | A visible beam in the air - best at night or in fog / haze. |
| **Attach** | World / Camera / Player / Car | World = stays where you put it. Camera = rides with the camera. Player / Car = follows the recorded player / the car they drive and keeps its place on them (behind the car, on the driver ...). Hidden while they aren't in the clip. |
| **Show From** | the clip's start or a marker | The light shows from here on. |
| **Show Until** | a marker or the clip's end | ... and until here. |
| **Fade** | Off / seconds | Fades in after Show From and out before Show Until. |
| **Move Here** | Enter | The light jumps to where the camera is now (a spot shines where the camera looks). |
| **Grab** | Off / On | On = the light rides with the camera while you fly it (Edit Camera) - place it like carrying a lamp. |
| **Preset** | your presets / Save New... | Enter on a preset = this light gets its look (not its place). Save New... = this light's look becomes "Light Preset 1", 2 ... in `WR Editor Fix\Light Presets\` (rename the .json to name it). |
| **Delete Light** | Enter twice | The light is gone. |

## Searchlight

The searchlight sweeps calmly left / right around the direction you pointed it,
with a slower drift and a gentle tilt - every searchlight its own way, so two of
them never move alike. The movement follows the **clip time**: scrubbing, playing
again and the export always show it at the same place.

Good setups:
- **Police chase**: Type Searchlight, Attach = Car, Move Here from above the car,
  Cone 15 - 20, Fog Beam Medium, Brightness 120 %, at night.
- **Stage / club**: two searchlights in different colours (Cool + Red), Attach =
  World, pointed at the car from the sides.

## Saved with your project

Your lights are saved in the project's WR file (`WR Editor Fix\Projects\<project>.json`)
next to WR blend / shake and come back when you load the project. Light Presets
are files of their own (`WR Editor Fix\Light Presets\*.json`) - share them freely.

## Limits

- The game draws shadows for at most 8 lights at a time.
- Fog Beam needs some haze / darkness to be seen - at noon on a clear day the
  beam is faint.
- Lights attached to the Player / Car hide while that player / car isn't in the clip.
