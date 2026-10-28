<!-- MADE BY WR | WARRAA_ -->
# Time and Weather - per clip and per marker

Play any clip at another time of day and with another weather - for the whole
clip, or changing from one marker to the next (with a hard cut or a smooth
time-lapse). The lighting follows, and the export renders exactly what you see.
Nothing is written into your clips.

**Game builds:** b3258, b3095 and b3407. **Ini:** `[Editor Time Weather]`.

> **Tested:** WR Options: 5 EVE exports with 5 different looks. Per marker: cut and smooth markers in preview + EVE export.
>
> **Not tested yet:** Snow on the ground (not supported).
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## For the whole clip - WR Options

Marker menu -> **WR Options**:

| Row | What it does |
|---|---|
| **Hour** | The hour every clip in the project plays at (00 - 23). |
| **Minute** | The minute (00 - 59). |
| **Weather** | Extra Sunny, Clear, Clouds, Smog, Foggy, Overcast, Rain, Thunder, Clearing, Neutral, Snow, Blizzard, Light Snow, Xmas, Halloween. |
| **Default** | Enter: back to the time and weather each clip was recorded with. |

The rows show the clip's own recorded time and weather until you change them.
Your pick stays for every clip until you press Default or restart FiveM.

## Per marker - WR Marker Options

Select a marker -> **Cameras** -> **WR Marker Options** (Enter):

| Row | What it does |
|---|---|
| **Time & Weather** | On = this marker has its own time and weather. Off = no change here. |
| **Hour** / **Minute** | The time from this marker on. |
| **Weather** | The weather from this marker on. |
| **Change** | **Cut** = switch the moment playback reaches this marker. **Smooth** = change gradually from the previous time & weather marker (or the clip start) and arrive exactly here. |

When you switch Time & Weather On, the marker starts with the look on screen.
A marker's time and weather wins over the WR Options pick from that marker on.

### Smooth = time-lapse

With Change = Smooth the clock runs **forward** from the previous look to this
marker's time, and the weather blends over the same stretch. For example:
marker 1 at 18:00 Clear, marker 2 at 22:00 Rain with Smooth - the sun sets
and the rain rolls in between the two markers.

## Without the menu - the ini

```ini
[Editor Time Weather]
TimeWeatherOverride = 1    ; start with Time / Weather below instead of the clip's own
Time = 21:30               ; HH:MM, blank = the clip's own
Weather = RAIN             ; blank = the clip's own
```

These keys reload live - edit, save, and it applies within a second.
`TimeWeatherOverride = 0` (default) = as recorded.

## Tips

- Night car shots: time + weather on the marker, plus WR Garage Lights = On
  (`03 - WR Garage.md`).
- One clip at sunset, the next at night: put each clip's look on its first
  marker.
- Snow weather doesn't add snow on the ground - only the sky, light and
  falling snow.

## Limits

- Saved with your project (the WR Options pick and every marker's time + weather).
- Game builds b3258, b3095 and b3407.
