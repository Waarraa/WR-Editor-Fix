<!-- MADE BY WR | WARRAA_ -->
# Free Camera - no leash, no collision, any zoom, any speed

The Rockstar Editor's free camera has limits: it gets pulled back when it
flies too far, bumps into walls and cars, stops zooming at about 10-100
degrees and flies slowly. WR Editor Fix removes each limit - each one on its
own switch. All of them are on in the shipped `.ini`.

**Ini:** `[Editor Camera]` - this section **reloads live**: edit, save, and it
applies within a second, no relaunch.

> **Tested:** Every switch on b3258 and b3095; No seek freeze on one big server (225+ seeks); cutscene recording + blocked clips.
>
> **Not tested yet:** No seek freeze on other servers; script cameras over a cutscene (known not to work).
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## The switches

| Key | What it does |
|---|---|
| `UnlimitedCameraDistance = 1` | No leash: the camera doesn't get pulled back when it flies far from the subject. `MaxCameraDistance` = the new limit in metres (default 1000). |
| `UncapZoom = 1` | Zoom past the stock ~10-100 degrees: `ZoomMinFov` / `ZoomMaxFov` (default 1 - 130). |
| `DisableCameraCollision = 1` | The camera goes through anything: walls and the map, the car or ped it's attached to or looking at, and objects between two markers (no "Unable to apply camera blend due to object collision" jump). |
| `FreeCamMoveSpeed = 1` | Faster free camera: `FreeCamMoveSpeedMultiplier` (1.0 = stock, 3.0 = 3x, about 0.25 to 20). |

**Camera speed in the editor:** marker menu -> WR Options -> **Camera Speed**
(x0.25 to x20) changes it live and saves it back into
`FreeCamMoveSpeedMultiplier`.

Every switch reads and checks the game's real values before changing
anything, and puts them back the moment you set it to 0.

## Blocked clips and cutscenes

Two more switches (on in the shipped `.ini`, **need a relaunch**, game builds
b3258, b3095 and b3407):

| Key | What it does |
|---|---|
| `[Recording] AllowCutsceneRecording = 1` | The Rockstar Editor keeps recording while a real GTA V cutscene plays or loads (for example one a server script starts). Normally the recording stops the moment you aren't in control and the clip fails with "Clip must be at least longer than 3 seconds". The cutscene's actors, camera and audio all end up in the clip. Scripts that block recording on purpose still work. |
| `[Editor Camera] FreeCameraOnBlockedClips = 1` | The editor normally locks the camera on those clips ("You cannot edit camera properties as this clip contains a blocked cutscene") and on clips recorded in first person. This unlocks the marker's Cameras menu and lets the free camera move on them. |

Known limit: recording doesn't continue while a script camera flies over the
cutscene (a server's own cutscene camera tool).

## No seek freeze

```ini
[Editor Playback]
NoSeekStall = 1          ; on by default
NoSeekStallWaitMs = 100  ; longest wait after a seek, in ms
```

After every seek, cut or marker move, the stock editor waits until the whole
game has finished streaming - on a busy server about 7 seconds every time. With
NoSeekStall it waits at most `NoSeekStallWaitMs` and plays on; anything still
loading pops in a moment later. Exports always keep the full wait, so the video
is fully loaded. Too much popping in? Raise the wait (6600 = stock) or set
`NoSeekStall = 0`. Needs a relaunch. Game builds b3258, b3095 and b3407.

## Rockstar Editor+ (RE+)

RE+ is not supported. If it is installed with its own camera distance or zoom
switched on, WR Editor Fix leaves those two to RE+ (the log and the loading
screen say "RE+") so the two don't fight.
