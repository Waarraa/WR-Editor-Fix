<!-- MADE BY WR | WARRAA_ -->
# WR Export - the editor's export, done properly

The Rockstar Editor's own export is stuck at 1920x1080, asks for a tiny
bitrate, leaves your ReShade preset out of the video and has no motion blur.
WR Export keeps the editor's Export button, frames and timing, and writes the
video itself:

- **HEVC, H.264 or AV1** on your graphics card's encoder (NVIDIA / AMD / Intel)
- **Constant quality (CQP) like OBS**, or a real bitrate
- **Any size**: Screen, 1440p, 4K and beyond - the 1920x1080 cap is gone
- **Your ReShade look** in every exported frame (needs ReShade with full add-on support, see "ReShade")
- **Real camera motion blur**: game frames blended like a camera shutter
- **Any frame rate**: 24, 30, 60, 120, 23.976 / 29.97 / 59.94 ...
- **Presets** in the editor's Export screen, and your own with **Save Preset**

**On by default.** **Game builds:** b3258, b3095 and b3407.
**Ini:** `WR_Export_Settings.ini` (next to `WR_Editor_Fix.ini`) - read again at
**every** export start - and the **WR EXPORT rows** in the editor's Export
screen, which save straight into it.

> **Tested:** Game builds b3258, b3095 and b3407; NVIDIA RTX 5070 Ti - HEVC, H.264 and AV1 with CQP (the encoder confirms constant QP) and bitrate; the CPU encoder (bitrate); Screen, 1440p and 4K; ReShade 6.8.0 (full add-on support version); motion blur 4 - 64 samples, every Blur Shutter, Blur Shape Soft and Even; Fps 23.976 and 59.94; the four presets + Save Preset; Sound off (no audio track).
>
> **Not tested yet:** AMD and Intel graphics card encoders (same Windows encoder path; anything an encoder refuses falls back on its own); sound together with motion blur (known issue, see "Sound").
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## How to use it

1. Edit your project as always.
2. Project menu -> **Export**. The Export screen now has the **WR EXPORT
   rows** under the game's own ones.
3. Pick a **Preset** (or set the rows yourself) and press **Export**.
4. Type the video's name in the game's keyboard, Enter - the export runs.

The video is saved as `WR_<the name you typed>.mp4` (spaces become `_`) in
`Videos\WR Exports` (or your `OutputFolder`). An older video is never
overwritten: the next one gets `(2)`, `(3)` ...

The log line `[WR Export] armed: exports go to ...` shows WR Export is on.

### Off, or EVE instead

- `[WR Export] Enabled = 0` in `WR_Editor_Fix.ini` = the editor's own stock
  export (needs a relaunch).
- **EVE** (ExtendedVideoExport) installed with its `enable_mod` on = EVE does
  the export and WR Export stands aside. **Pick one** - both at the same time
  can crash. The WR loading screen shows a blue INFO box when both are in.
  Want WR Export? Remove EVE. Want EVE? Set `[WR Export] Enabled = 0`.

## The Export screen - WR EXPORT rows

Left / right changes a row, the right side of the screen explains the row
you're on, and every change is saved into `WR_Export_Settings.ini` at once.

| Row | Values | What it does |
|---|---|---|
| **Preset** | Fast, Medium, Slow, Super Slow, your own | Sets every row below at once (see "Presets"). |
| **Save Preset** | Enter | The game's keyboard: type a name - every row is saved as your own preset. |
| **Resolution** | Screen, 720p, 1080p, 1440p, 4K | The video size, the game's aspect kept. Screen = exactly what the game renders. |
| **Codec** | HEVC, H.264, AV1 | HEVC = the same picture in a 30-50 % smaller file than H.264. AV1 = the smallest files (needs an NVIDIA RTX 40 / 50, AMD RX 7000 or Intel Arc, and an editor that opens AV1). |
| **Encoder** | Graphics Card, CPU | The graphics card's encoder (NVIDIA NVENC / AMD VCN / Intel Quick Sync - shown by name) or Windows' CPU encoder (H.264 only, slower). |
| **Video Quality** | CQP 10, 15, 18, 22, 28; Bitrate Auto, 60, 120, 200 Mbps | CQP = constant quality, lower = better + bigger. Bitrate = a fixed average. The CPU encoder offers the bitrates only. |
| **Frame Rate** | Stock Setting, 24, 25, 30, 50, 60, 120, 23.976, 29.97, 59.94 | Stock Setting = the editor's own frame rate row (30 / 60). |
| **Motion Blur** | Off, 4, 8, 16, 32, 64 Samples | Real camera motion blur (see "Motion blur"). |
| **Blur Shutter** | 0.25, 0.5 (Film), 0.75, 1 (Max) | How long the streaks are. |
| **Blur Shape** | Soft, Even | Soft = smoother, fewer visible copies of fast things. |
| **ReShade** | On, Off | Your ReShade preset in the video. |
| **Sound** | On, Off | The game's sound in the video. Off = no audio track at all. |

The game's own **Bit Rate** row is greyed out - WR decides the quality.

## Presets

| Preset | What it is |
|---|---|
| **Fast** | No motion blur, CQP 18, sound on - exports at normal speed. |
| **Medium** | 8-sample motion blur, film shutter, CQP 18, sound off - about 8x the export time. |
| **Slow** | 16-sample motion blur, film shutter, CQP 15, sound off - about 16x. |
| **Super Slow** | 32-sample motion blur, film shutter, CQP 15, sound off - about 32x, the smoothest. |

Presets are `.json` files in `plugins\WR Editor Fix\Export Presets\` - **the
file name is the preset's name**.

- **Your own:** Export screen -> **Save Preset** -> type a name -> Enter. It's
  saved as `Export Presets\<name>.json` and picked right away. The same name
  again = updated.
- Or copy a `.json` in that folder and rename it (`my.json` shows as "my").
- The preset you picked last is remembered (`[Video] Preset` in the ini).

## Every setting - WR_Export_Settings.ini

Every key is explained inside the file with copy-paste values. Change, save,
export - no restart.

`[Video]`

| Key | Options | What it does |
|---|---|---|
| `OutputFolder` | empty = `Videos\WR Exports`, or any folder | Where videos go. |
| `Preset` | a preset name | The preset picked or saved last (a name only - the keys below are what's used). |
| `Codec` | `HEVC` / `H.264` / `AV1` | AV1 falls back to HEVC, HEVC to H.264, when the card has no encoder for it. |
| `Encoder` | `Auto` / `CPU` | Auto = the encoder of the graphics card the game runs on (a PC with CPU graphics too keeps the export on the real card). CPU = H.264 only, slower - the fallback. |
| `Resolution` | `Screen`, `1080p`, `1440p` (`2K`), `4K` (`2160p`), any height 480-4320 | Bigger than the game renders = upscaled (bigger file, no new detail). |
| `BitrateMbps` | `Auto` or 2-400 | Average bitrate. Auto: 1080p60 = 60, 1440p60 = ~92, 4K60 = ~170. Not used when `CQP` is set. |
| `CQP` | `Off` or 1-51 | Constant quality like OBS CQP. 15-18 = very high quality. Graphics card encoders only. |
| `ReShade` | `1` / `0` | Your ReShade effects in the video. |
| `Fps` | `Game`, `24`, `25`, `30`, `50`, `60`, `120`, `23.976`, `29.97`, `59.94` | The video's frame rate. Game = the editor's own setting. |
| `MotionBlurSamples` | `0` or 2-64 | Game frames blended into each video frame. 0 = off. |
| `MotionBlurStrength` | `0.25`, `0.5`, `0.75`, `1` | The shutter: how long the streaks are. 0.5 = film look. Doesn't change the export time. |
| `MotionBlurShape` | `Soft` / `Even` | How the samples are mixed. |

`[Audio]`

| Key | Options | What it does |
|---|---|---|
| `Enabled` | `1` / `0` | The game's sound in the video. 0 = no audio track - use it for motion blur exports for now. |
| `BitrateKbps` | `96`, `128`, `160`, `192` | AAC sound quality. |

## Quality: CQP or bitrate

- **CQP** (`CQP = 18`): every frame gets the same quality and the file size
  follows the picture - calm shots stay small, fast action gets what it needs.
  This is what most creators use in OBS. **Graphics card encoders only** - with
  Encoder = CPU the bitrate is always used (Windows' CPU encoder doesn't do
  real constant quality), and the log says so.
- **Bitrate** (`BitrateMbps`): you pick the average data rate, so you know the
  file size up front: Mbps x 7.5 = MB per minute (100 Mbps = about 750 MB a
  minute).
- **AV1** uses its own quality scale (1-63); WR converts your CQP to it, so
  CQP 18 means about the same quality in every codec.

The log proves which one ran:
`[WR Export] the encoder reports: rate control constant QP, QP 18`.

## Resolution and 4K

`Screen` exports exactly what the game renders - 2560x1440 on a 1440p
monitor, no 1920x1080 cap. A bigger `Resolution` upscales the picture: the
file gets bigger but no new detail appears. For real 4K detail let the game
render 4K: turn on NVIDIA DLDSR or AMD VSR, set the game to 3840x2160 and
keep `Resolution = Screen`.

Tip: YouTube gives 1440p and 4K uploads a better encode than 1080p, so even
an upscaled 1440p export looks sharper on YouTube.

## ReShade

The stock export copies the picture before ReShade draws, so presets never
made it into videos. With ReShade on, WR Export has ReShade draw its effects
into every exported frame - the video looks like your game. With motion blur
on, ReShade runs on every sample before the blend, so sharpening and film
grain stay crisp instead of being smeared.

> **Only ReShade with full add-on support is supported.** WR draws your
> preset into the video through ReShade's add-on system, and the standard
> ReShade download isn't supported. Don't have it? Download
> **"ReShade ... with full add-on support"** from
> [reshade.me](https://reshade.me) and use it instead of the standard one.
> Check: "WR Editor Fix" shows up in ReShade's **Add-ons** tab. Many FiveM
> graphics packs (QuantV for example) already use this version.

ReShade costs some export speed: it runs for every frame the export renders.

## Motion blur

Every video frame becomes the average of **Motion Blur** samples - game frames
rendered a tiny step apart in time, like a real camera's shutter. Fast cars,
spinning wheels and camera pans get natural streaks instead of the
razor-sharp game look. The blend is done in linear light on the graphics
card, the way a real exposure adds up light.

- **Blur Shutter** (`MotionBlurStrength`) = how long the shutter stays open =
  how long the streaks are. 0.5 = the film look (a 180 degree shutter). It
  does **not** change the export time: the closed part of the shutter is
  skipped in one jump.
- **Blur Shape**: **Soft** (default) counts the middle of the shutter most and
  fades the streak ends - wheels blur into a smooth disc. **Even** counts every
  sample the same, like a plain camera shutter. Same export time.
- While it renders, your screen shows the last finished video frame - that's
  normal.

### How long will it take?

The game renders about 60 frames a second during an export (your PC, the
resolution and your ReShade preset change that), and every sample is one
rendered frame:

**export seconds = video seconds x fps x samples / 60**

| Video | Motion Blur | Export time |
|---|---|---|
| 10 s at 60 fps | 8 samples | 80 s, under 1.5 min |
| 10 s at 60 fps | 16 samples | 160 s, under 3 min |
| 10 s at 30 fps | 16 samples | 80 s |
| 10 s at 60 fps | 32 samples | 320 s, about 5 min |

The log shows the real speed every 2 seconds:
`[WR Export] speed: 3.5 video frames/s from 54.0 game frames/s ...`

The graphics card's encoder is never the slow part - the time goes into the
game rendering the extra frames.

## Sound

- Sound On: the game's sound as AAC (`BitrateKbps`).
- Sound Off: the video has **no audio track** at all.
- **Known issue - motion blur + sound:** the game makes one piece of sound
  for every frame it renders, and motion blur renders many frames per video
  frame - the sound comes out several times too long. That's why the blur
  presets have Sound Off: add your music in your video editor. A proper fix
  is planned (EVE has the same problem).

## Reading the log

`plugins\WR Editor Fix\Logs\WR_Editor_Fix.log` - every line starts with
`[WR Export]`:

| Line | Means |
|---|---|
| `armed: exports go to ...` | WR Export is on, with your folder, codec and quality |
| `graphics card encoders: ...` | the encoders Windows offers on this PC |
| `encoder card: NVIDIA GeForce ...` | the graphics card the export's encoder runs on |
| `export -> D:\...\WR_my_video.mp4 (...)` | an export started, where it goes |
| `video: HEVC 2560x1440 59.94 fps, constant QP 15` | what the video is written as |
| `encoder in use: NVIDIA HEVC Encoder MFT` | the encoder that really runs |
| `the encoder reports: rate control constant QP, QP 15` | what the encoder itself confirms |
| `motion blur: ...` | blur settings and how many frames the game renders |
| `speed: ...` | every 2 s: video and game frames per second |
| `done (...) in 198.7 s: ...` | the export finished: time, file, size |

## When something goes wrong

| Problem | Fix |
|---|---|
| No WR EXPORT rows in the Export screen | `[WR Export] Enabled = 0`, or EVE is installed and on (the log says so) - see "Off, or EVE instead" |
| The export fails right away, log says `the video encoder refused the game's frames` | Codec = H.264, or Encoder = CPU |
| The log says `EVE is installed and on - EVE does this export` | Remove EVE, or set EVE's `enable_mod = false` |
| Blur video is the right length but the sound is too long | Known issue - Sound Off for blur exports |
| The export is slow | Fewer Motion Blur samples, or a lower Frame Rate - see "How long will it take?" |
| The video has no ReShade look | Use ReShade **with full add-on support** (reshade.me) - the standard download isn't supported; ReShade On; check the log for the `ReShade:` line |
| AV1 file won't open in your editor | Your editor doesn't read AV1 yet - use HEVC |

Still stuck? Send `WR_Editor_Fix.log` and your `WR_Export_Settings.ini` in a ticket.
