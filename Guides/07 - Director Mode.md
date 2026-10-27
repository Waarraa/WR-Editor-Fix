# Director Mode - fly the camera live, the take becomes markers

Play the clip and fly the camera yourself, like a camera operator. When the
take ends, Director Mode turns your move into editor markers - the fewest that
still reproduce it - so it plays back exactly like you flew it, and you can
still edit every marker afterwards.

**Game build:** b3258 only. **First version** - see Limits.
**Works best with a controller.** Mouse + keyboard works but is harder to fly
smoothly.

> **Tested:** A take at 50 % record speed with an XInput (Xbox-style) controller - 18 Smart markers; mouse + keyboard (works, clunky).
>
> **Not tested yet:** Very long takes, Follow on peds, other controllers (PlayStation pads need an XInput tool such as Steam Input or DS4Windows).
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## How to use it

1. Open the clip, select a marker -> **WR Options** -> **Director Mode** (Enter).
2. Set the options (below).
3. Select **START** and press **Enter**.
   - If the clip already has markers, it asks first: the take replaces the
     whole timeline.
4. The clip jumps to its start, **3 - 2 - 1**, and plays. Fly!
5. The take ends when the clip ends, or when you press **B** / **Backspace**.
6. The take becomes markers, and the playhead goes back to the start. Play it.

While a take runs, the editor itself doesn't see your pad or keys, so nothing
in the menu changes by accident.

## The options

| Row | Values | What it does |
|---|---|---|
| **Look Assist** | On / Off | On: the camera keeps the car / player centred; the right stick (or mouse) shifts the framing. Off: full free look. |
| **Follow** | On / Off | On: the camera rides along with the car / player, so it never gets away - you move around it. Off: the camera stays where you fly it. |
| **Record Speed** | 100 / 50 / 35 / 20 % | How fast the clip plays while you fly. The camera keeps its own speed, so slower = easier to track. It plays back at normal speed after, your moves sped up with it. |
| **Detail** | Low / Normal / High | How closely the markers follow your take. Low = few markers, smooth. High = many markers, every little move kept. |
| **START** | Enter | Starts the take. |

## Controls

| Action | Controller | Mouse + keyboard |
|---|---|---|
| Move | Left stick | W A S D |
| Look | Right stick | Mouse |
| Down / up | LT / RT | Q / E |
| Zoom | LB / RB | - |
| Roll | D-pad left / right | Z / C |
| Fly speed down / up | D-pad down / up | - / + |
| Precise (slow) | Hold A | Hold Ctrl |
| Fast | Hold L3 | Hold Shift |
| Look Assist on / off | X | F |
| Follow on / off | Y | G |
| Stop the take | B | Backspace / Esc |

## Smart markers

Director Mode doesn't drop a marker every few frames. It finds the fewest
markers that still reproduce your move along the WR blend path (checked frame
by frame with the same maths the playback uses), up to 60 markers, at least
150 ms apart. Every marker gets a free camera and WR blend, so the playback
passes each point exactly on time.

## Tips

- Start with Record Speed 50 %: half-speed takes are much easier to frame.
- Look Assist On + Follow On is the easiest way to get a clean car shot - you
  only steer where the camera sits around the car.
- Hold A (controller) for slow, precise moves near the car.
- Not happy? START again - the new take replaces the old one.

## Limits (first version)

- No obstacle checks on a take yet - the camera can go through walls if you
  fly it there (WR Automate has checks, Director Mode doesn't yet).
- No re-recording just one part of a take, and no undo.
- No settings in the `.ini` yet.
- Game build b3258 only.
