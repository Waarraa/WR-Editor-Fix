<!-- MADE BY WR | WARRAA_ -->
<!-- WR EDITOR FIX - CLOSED SOURCE. (c) Warraa / WR - ALL RIGHTS RESERVED. -->
# WR Longer Recordings - record up to ~3 minutes

The Rockstar Editor normally records only about **17 seconds** in busy city traffic (up to a minute on an empty road)
before it has to start a new clip. **WR Longer Recordings** gives the recording more replay memory, so one clip holds up
to about **3 minutes** of busy city driving - and much more in quiet areas.

> **New in v1.1.0, on by default.** **Tested:** game builds b3258, b3095 and b3407; 3-minute recordings straight into the
> editor; two 3-minute WR Exports in one session.
> **Good to know:** this is one of the two parts of WR Editor Fix that act **while you play** (recording happens in game,
> so it can't wait for the editor). It sets the game's replay memory size when FiveM starts - nothing else.

## How it works

- **Nothing to do** - with the shipped `.ini` it's on. Record the way you always do.
- `RecordBlocks = Auto` picks the size from your PC's memory:

| Your RAM | Blocks | Busiest city traffic, roughly |
|---|---|---|
| under 8 GB | off (the game's own size) | ~17 s |
| 8 GB | 64 | ~45 s |
| 16 GB | 128 | ~1 min 45 s |
| 24 GB | 192 | ~2.5 min |
| 32 GB or more | 220 (~1 GB, the most the game's replay memory handles) | ~3 min |

- When the memory fills, the game saves the clip and keeps recording into a new one - like before, just much later.
- Long clips open in the editor too (the editor gets the room it needs to load them).

## Settings (`WR_Editor_Fix.ini`, `[Recording]`)

| Key | What it does |
|---|---|
| `RecordBlocks = Auto` | Default - the biggest size your memory comfortably allows (table above). |
| `RecordBlocks = 0` | **Off** - the game's own size. |
| `RecordBlocks = 30 - 220` | Your own size in 4 MB blocks (220 = ~1 GB). If Windows can't give that much, a smaller size is used and the log says which. |
| `OpenLongClips = 1` | Open clips recorded with up to 128 blocks even with `RecordBlocks = 0` (above 30 blocks it's automatic). |

Changes need a FiveM restart.

## Memory and disk

- Each block costs about **4.4 MB of RAM** while the game runs (220 blocks = ~1 GB).
- Long clips take more disk space: about **230 MB per clip at 128 blocks**.
- Low on RAM or playing on a heavy server? Use a smaller number (64 / 128) or `0`.

## Tips

- **Edit clips on the game build they were recorded on** - on another build they load slower and some clips can crash.
- Long clips + WR Automate: with a song long enough, WR Automate uses the whole recording.
- The log line `[Longer Recordings]` at FiveM start says how much memory the recording got.
