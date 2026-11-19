<!-- MADE BY WR | WARRAA_ -->
# WR Undo - Ctrl + Z / Ctrl + Y in the editor

One small mistake shouldn't mean redoing half the project. WR Undo takes the
editor back a step - camera moves, blends, shakes, speed, effects, a marker you
added or deleted - and Redo brings it back.

> **Tested:** b3095; Ctrl + Z / Ctrl + Y and the WR Undo row; marker settings (camera, speed, blend, effects); adding and deleting markers; the menu page updating right away.
>
> **Not tested yet:** b3258 / b3407 for adding / deleting markers (same code path as WR Automate's timeline, which runs on all three).

## How to use it

| Key / row | What it does |
|---|---|
| **Ctrl + Z** | Undo - the newest change on this clip goes back |
| **Ctrl + Y** (or Ctrl + Shift + Z) | Redo - the undo you just made comes back |
| **WR Undo** row | Second last row on every editor page (right before Edit Camera / WR Options): Enter = undo. It shows how many steps are left. |

The help line says what was undone / redone and how many steps are left, e.g.
`Undone: marker added at 0:07.3. 3 more undo left (Ctrl + Z), 2 redo (Ctrl + Y).`

The keys work while you **edit a clip** with the game window in front - not
during an export, a WR Automate run or a Director take.

After an undo / redo the **playhead jumps back onto the marker the menu is
editing**, so the menu always stays on a real marker - you can press Ctrl + Z
several times in a row. The messages and the row value follow the WR language.

## What one step is

- **One visit to a marker** = one step: everything you change on a marker
  (Cameras, Effects, Speed, Position, WR shake, ...) until you go to another
  marker or leave the menu is undone together.
- **Adding a marker** = one step (Ctrl + Z removes it again).
- **Deleting a marker** = one step (Ctrl + Z brings it back with all its settings).
- A brand-new marker's first visit (the editor sets its camera) can be a step of
  its own - press Ctrl + Z once more to remove the marker itself.

**5 steps** per clip, and 5 redos. A new change after an undo clears the redo
list (like every editor).

## When the history starts fresh

- You open another clip.
- **WR Automate** or **Director Mode** rebuilt the timeline (undo that by running
  it again, or Clear Timeline).
- **Clear Timeline** (it can't be undone).

## Limits

- 5 steps back per clip.
- Song / music settings, export settings and WR Options pages (time & weather,
  editor look ...) are not part of the undo - only the clip's markers.
