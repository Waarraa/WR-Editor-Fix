<!-- MADE BY WR | WARRAA_ -->
# Real 4K exports - DLDSR / VSR

WR Export can write a 4K video on any monitor. But there is a difference between
a 4K **file** and 4K **detail**:

- `Resolution = 4K` with the game at 1440p = the picture is **upscaled**: a
  bigger file, the same detail as 1440p.
- The game **rendering** at 3840x2160 + `Resolution = Screen` = **real 4K**:
  every pixel is drawn by the game. Sharper cars, readable signs, cleaner
  trees - and YouTube gives the upload its best encode.

You don't need a 4K monitor for that. NVIDIA **DLDSR** (and AMD **VSR**) let the
game render at 4K and scale it down to your screen, so you play / edit on your
normal monitor while the export gets the full 4K frame.

> **Tested:** WR Export writing 3840x2160 videos (Resolution = 4K) and the game's own size (Resolution = Screen) - b3258 / b3095 / b3407, NVIDIA RTX 5070 Ti, HEVC / AV1 CQP.
>
> **Not tested yet:** the DLDSR / VSR setup itself end to end (game rendering 3840x2160 on a 1440p monitor -> Screen export). WR Export takes whatever size the game renders, so it should simply give a 3840x2160 video - please report how it goes. AMD VSR and Intel graphics not tested.

## What you get

| Setup | The video | Detail |
|---|---|---|
| Game 1440p, `Resolution = Screen` | 2560x1440 | 1440p |
| Game 1440p, `Resolution = 4K` | 3840x2160 | 1440p, upscaled |
| **Game 4K via DLDSR, `Resolution = Screen`** | **3840x2160** | **4K** |

## NVIDIA: turn on DLDSR

1. **NVIDIA Control Panel** -> **Manage 3D settings** -> **Global settings**.
2. **DSR - Factors**: tick **2.25x DL** (on a 1440p monitor that's 3840x2160;
   on a 1080p monitor 2.25x = 2880x1620 - tick **4.00x** (legacy) for a full
   3840x2160 there).
3. **DSR - Smoothness**: 33 % is a good start (0 % = sharpest, more = softer).
4. **Apply**.

Optional but easiest: set your **Windows desktop** to the new resolution too
(Settings -> Display -> Display resolution -> 3840 x 2160). Then the game's
Borderless mode picks it up on its own.

## AMD: turn on VSR

**AMD Software** -> **Gaming** -> **Display** -> **Virtual Super Resolution** -> On.
The 3840x2160 entry then shows up in Windows and in the game.

## In the game

1. **Settings -> Graphics -> Screen Type**: **Windowed Borderless** (or Fullscreen).
2. **Resolution**: **3840 x 2160**.
3. **Frame Scaling Mode**: **Off** (1/1). Higher numbers render even bigger than
   4K and cost a lot of time; lower ones (2/3, 1/2) render less than 4K again.
4. Leave **MSAA** as you like it - at 4K FXAA / no MSAA usually looks clean already.

With **GTAV Upscaler (DLSS)**: keep `mTargetResolutionScale = 1.0` (DLAA at 4K)
or use a DLSS quality mode to get the frame rate back - the upscaler's Target
Resolution Scale only supersamples inside the game, the final frame the export
sees is still the game's resolution. **CoreFX**: its own DLSS / FSR / XeSS works
the same way - don't stack another upscaler on it.

## In WR Export

Export screen -> WR EXPORT rows:

| Row | Set it to |
|---|---|
| **Resolution** | **Screen** - the game's 3840x2160, no scaling |
| **Codec** | **HEVC** (or AV1 on RTX 40 / 50 series) - H.264 at 4K needs a very high bitrate |
| **Video Quality** | **CQP 18 - 22** for YouTube masters (smaller = better + bigger), or a bitrate of 120 - 170 Mbit/s |
| **Frame Rate** | your choice - 29.97 / 59.94 |

Export as always. The log shows it worked:

```
[WR Export] export size 3840x2160 (Resolution = Screen; the game renders 3840x2160 ...)
[WR Export] video: HEVC 3840x2160 59.94 fps, constant QP 20
```

## How long, how big

- The **export** renders every frame at 4K: about 2 - 2.5x slower than 1440p.
  Motion blur multiplies that again (8 samples = about 8x).
- A 30 s 4K60 HEVC video at CQP 20 is roughly 300 - 600 MB - fine for YouTube.
- Playing / editing at 4K costs frame rate in the editor; that doesn't matter
  for the export (it's frame-exact, not real-time).

## Tips

- **YouTube**: upload the 4K file as it is. Even if most people watch at 1080p,
  YouTube's 4K encode (VP9 / AV1) looks clearly better than its 1080p one.
- **Vegas / Premiere**: edit with a 4K project at the export's frame rate. If
  playback is slow, use proxies - the final render reads the full file.
- Back to normal: set the game (and the desktop) back to your monitor's
  resolution. DLDSR can stay ticked in the NVIDIA panel - it does nothing until a
  game or the desktop picks the bigger resolution.

## When something goes wrong

| Problem | Fix |
|---|---|
| No 3840 x 2160 in the game's list | DLDSR / VSR not ticked, or the game is in Windowed mode - use Borderless or Fullscreen, or set the desktop to 3840x2160 first. |
| The video is 2560x1440 | The game isn't rendering 4K - check the in-game Resolution and Frame Scaling Mode 1/1. |
| The video is 4K but soft | `Resolution = 4K` with the game at 1440p = upscaled. Use DLDSR + `Screen`. Or DSR Smoothness too high. |
| Very low frame rate while editing | Normal at 4K. Edit at 1440p, switch to 4K only for the final export (the project and its markers don't change). |
| Export crashes / runs out of video memory | 4K + motion blur 32 - 64 samples + heavy graphics mods is a lot. Lower the samples or the game's texture settings. |
