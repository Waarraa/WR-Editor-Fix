<!-- MADE BY WR | WARRAA_ -->
# WR Quick Menu - your favourite WR pages, one key away

No more scrolling through menus to find a tool. Press **J** and a round WR menu opens over the clip editor: point at a
slot, press Enter, and you are on that WR page. You choose what goes in the 8 slots.

> **New in v1.1.0.** **Tested:** b3407 (Warraa) + the WR testers on b3258 / b3095 / b3407: J / L3, mouse, arrows, pad,
> slot picks, saved slots, the tile picker, the frosted glass, the Quick Menu Key row.
> **Not tested yet:** other screen resolutions / UI scales. The page is English for now.

## Open and pick

| Key / button | What it does |
|---|---|
| **J** (keyboard) / **L3** (controller, left stick press) | Opens and closes the Quick Menu |
| **Mouse** | Point at a slot to select it, **left click** opens it, **right click** or a click outside closes the menu, the **wheel** steps round |
| **Left / Right** arrows | Step round the slots |
| **Up / Down** arrows | Top / bottom slot |
| **Left stick** | Points at a slot |
| **Enter / A** | Opens the selected slot |
| **Esc / B** | Closes the menu |

The Quick Menu works while you **edit a clip** (the marker menu or a WR page is up). Outside the clip editor a pick says
"Open a marker first (M)". It does not open during an export, a WR Automate build or a Director take.

**The editor behind it does not react** while the menu is open - your keys, mouse and controller only drive the menu.
Ctrl + Z / Ctrl + Y do nothing while it is open.

## Change what is in a slot

Select a slot and press **C** (controller: **Y**). A big panel opens with every option as a tile - its icon, its name
and a short description of the one you point at:

| Key / button | What it does |
|---|---|
| **Mouse** | Point at a tile to see what it does, **click** puts it in the slot |
| **Arrows / left stick** | Move one tile at a time |
| **Enter / A** | Puts the selected tile in the slot |
| **Esc / B / right click** | Cancels - the slot stays as it was |
| **Click a slot on the small wheel**, **1 - 8**, **LB / RB** | Change another slot right there, without going back |

"Now" marks the option already in this slot, "Slot N" an option that is in another slot. Your slots are saved at once
in `WR Editor Fix\Quick Menu.json` and stay after a restart.

**Options:** Edit Camera, WR Camera, WR Time & Weather, WR Lights, WR Garage, WR World, WR Automate, WR Undo, WR Director,
WR Editor Look, WR Shake Options, WR Marker Options, Matrix Freeze, Face Camera, WR Clear Timeline.

## Change the key

**WR Options > WR Editor Look > Quick Menu Key:** press Enter, then the new key. It is saved and works right away. Keys
the editor uses are refused with the reason (Enter, Space, Tab, Delete, the arrows, W A S D Q E Z M H, [ ], C - the
Quick Menu's edit key, F8 - FiveM's console, the Windows keys). Esc cancels. The controller button stays L3.

## The look

The menu is **frosted glass**: the game shows blurred behind it. The blur is one picture of the game taken when the
menu opens. `Glass = 0` in the ini gives solid dark panels instead.

## Ini

```ini
[WR Quick Menu]
Enabled = 1        ; 0 = off
Key = J            ; the key (also in WR Options > WR Editor Look > Quick Menu Key)
PadButton = L3     ; L3, R3, Back, Y, X, DpadUp, DpadDown or None
Glass = 1          ; 1 = frosted glass, 0 = solid dark panels
```

## Good to know

- The Quick Menu is WR Editor Fix's own window over the game - **never in an export**.
- The page is English for now; the WR languages come later.
