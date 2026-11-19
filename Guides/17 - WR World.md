<!-- MADE BY WR | WARRAA_ -->
# WR World - the world of your clip

Change the world the clip plays in: wet roads without rain, every car's lights on, an empty city, no tyre marks. What you see in the editor is what the WR Export video gets.

**Where:** WR Options -> **WR World**. **Editor only:** it changes nothing in a game or on a server.

> **Tested:** b3095. Road Wetness: every level on a clip recorded in rain and on a sunny one, while it plays, and in a WR Export video (2026-11-07 again after the flicker fix: Soaked + a night time in a WR Export video, steady frame to frame). Car Lights: every value on a city clip (90 cars) and a car clip. Empty City: a city clip in the preview and in a WR Export video. Tyre Marks: Off / On in the preview and the export.
>
> **Not tested yet:** b3258 / b3407 in game. Their game code was found and checked byte for byte on all three builds, and WR checks it again before it changes anything.

## The rows

| Row | Values | What it does |
|---|---|---|
| **Road Wetness** | Clip / Dry / Damp / Wet / Soaked | How wet the roads look, without making it rain. **Clip** = as recorded. **Dry** = dry roads even in a clip recorded in the rain (the rain still falls). **Damp** = a light sheen. **Wet** = wet asphalt with reflections. **Soaked** = puddles everywhere and a mirror-like road, even on a sunny day. |
| **Car Lights** | Clip / On / Full Beam / Off | Every car's lights in the clip. **Clip** = as recorded. **On** = headlights on, for night shots of a clip recorded in daylight. **Full Beam** = high beams. **Off** = all lights off, tail lights too. |
| **Clean Cars** | Clip / 0 - 15 | How dirty every car in the clip looks. **Clip** = as recorded, **0** = spotless ... **15** = filthy (the game's own dirt levels). Preview and export. |
| **Repair** | Clip / Repaired | **Repaired** = the game's own full repair on every car (dents, scratches, windows, lights), and the windows stay whole while the clip plays. Enter on Repaired = repair again. Parts that broke off in the recording (hood, doors, bumpers, wheels) stay off - the clip itself has them missing. |
| **Empty City** | Off / On | **On** = every other car and person disappears. Only the recorded player, their car and the people sitting in it stay - also your parked car while you stand next to it. Clean streets for cinematic shots. |
| **Tyre Marks** | On / Off | **Off** = the clip without the tyre / skid marks the cars leave (the black trails behind drifting wheels). It uses the game's own "no decals" switch, so blood and bullet holes go too. |

## Good to know

- **Soaked on a sunny clip** is the look: a rain-soaked road at golden hour, with no rain falling and no grey sky.
  Set the time on WR Time & Weather to match.
- **Dry on a rain clip** keeps the rain falling but takes the wet road away.
- Indoors (tunnels, garages) the game never shows wet floors. That's the game's own rule.
- Tyre marks that are painted into GTA's road textures (many curves have them) are part of the map and stay.
- **Car Lights On at night**: set the time on WR Time & Weather first (e.g. Hour 22). A clip recorded at noon then
  gets cars driving with their lights on.
- **Road Wetness, Car Lights, Clean Cars and Empty City are per clip:** every fresh clip starts with the defaults
  (Clip / Clip / Clip / Off). Open a clip again while the game runs and it gets back what you picked for it. They are
  not kept in `WR_Editor_Fix.ini`. A WR Export plays each clip with its own picks.
- **Tyre Marks** is kept for the next launch (`[Editor Time Weather] TyreMarks` in `WR_Editor_Fix.ini`).
