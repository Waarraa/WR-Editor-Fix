<!-- MADE BY WR | WARRAA_ -->
# Editor Look - theme, fonts, colours, header and Timeline Size

Make the Rockstar Editor yours: the WR Neon Glass theme, 10 built-in fonts,
every colour from a palette, header art at the top of the menu, and the
timeline at the size you like. It's the
game itself drawing it (built into the plugin), not an overlay on top. Only
while the editor is open - the rest of the game looks stock.

**Game builds:** b3258, b3095 and b3407. **Ini:** `[Editor Look]`.

> **Tested:** Both themes, fonts, colours and headers, live switching and saving to the ini; Timeline Size 50 - 300 % on the Neon theme, on b3258, b3095 and b3407 - one PC, Windows 11.
>
> **Not tested yet:** Other screen resolutions / UI scales; Timeline Size on the Default theme.
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## Theme

```ini
[Editor Look]
Theme = Neon      ; or Default
```

- **Neon** (on in the shipped `.ini`) - WR Neon Glass on the clip edit screen:
  a frosted glass menu with a neon pill on the selected row, one glass panel
  for the time and the playback buttons, a slim timeline with a red played
  line, a glowing playhead orb and diamond markers.
- **Default** - the stock Rockstar Editor.

Only the clip edit screen (where you edit markers) changes; the other editor
screens stay stock. The theme takes effect the next time the editor opens.

## Font

WR Options -> **Font** (live), or `Font =` in the `.ini`:

| Font | Look |
|---|---|
| Default | the original Rockstar Editor font |
| Chakra Petch | techy, clean |
| Spicy Rice | wild, chunky |
| Bagel Fat One | round, bubbly |
| Oswald | clean, condensed |
| Carter One | bold, playful |
| Ubuntu Mono | code style |
| Permanent Marker | marker pen |
| Germania One | old-style blackletter |
| Kavoon | fat brush |
| Sriracha | handwriting |

Every editor text uses it: menus, the help line, headings, project info and
timeline clip names (not your own text clips or number fields). Works with
both themes. The fonts are free Google Fonts, built into the plugin - their
licences are in `THIRD-PARTY-NOTICES.txt`.

## Colors

WR Options -> **Colors** (Enter) opens the WR Colors page. Left / right on a
row picks **Built-in** or a colour from the palette (WR Red, Hot Red ...
Black); a custom hex from the `.ini` shows as `#RRGGBB`. **Default Colors**
(Enter) puts the whole page back.

| Theme | Rows |
|---|---|
| Neon | Glass, Selection, Buttons, Icons, Time, Timeline, Markers, Help Box |
| Default | Menu Text, Greyed Text |

Every pick shows right away and is saved into its `[Editor Look]` line.

In the `.ini`, colours are `RRGGBB` hex without the `#` (`E01234` = WR red),
blank = the built-in colour:

```ini
Glass =          ; frosted glass: menu, time + button panel, timeline rail
Selection =      ; the neon pill around the selected row
Buttons =        ; playback button glow, hover + pressed
Icons =          ; playback button icons
Time =           ; the time above the playback buttons
Timeline =       ; played line + glowing playhead
Markers =        ; diamond markers (start + end included)
HelpBox =        ; the help line box
MenuText =       ; Default theme: row labels + values, playhead
MenuTextGreyed = ; Default theme: greyed rows, played region, second timecode
```

## Header

WR Options -> **Header Style** / **Header Motion** (live), or in the `.ini`:

```ini
Header = Meme          ; Stock, WR, Meme, Retro, Cinematic
HeaderAnimated = 1     ; 1 = animated (Meme, Retro, Cinematic move), 0 = still
```

The logo at the top of the editor menu. Stock = the original R* EDITOR.

## Timeline Size

WR Options -> **Timeline Size** (live), or in the `.ini`:

```ini
TimelineSize = 100    ; 50 - 300 (percent), 100 = the original size
```

How big the clip edit timeline is: the markers, the clip start / end, the
playhead and how thick the bar is. Left / right steps 10 %. The icons grow
around their point on the line, so they stay exactly on it, and the timeline
keeps its width - every marker stays at its time. The Neon rail grows up to
150 % (it stays inside the space the editor lays the timeline out in); on the
Default theme only the icons grow, the stock bar stays as it is.

## What saves where

Font, Colors, Header Style, Header Motion and Timeline Size (and Camera Speed)
changed in WR Options are saved back into their own `[Editor Look]` lines about a second
after your last change, so the next launch starts with them. `Theme` is only
set in the `.ini`.

## Coming from v0.8.0 or older?

`[Editor Look]` replaces `[Editor Theme]`: `EditorTheme`, `EditorFont` and the
old GTA font list (Font5, Font2_cond, RockstarTAG, gtaCash) are gone. Take the
new `.ini`; your old menu colours go into `MenuText` / `MenuTextGreyed`.

## Limits

- Game builds b3258, b3095 and b3407.
- Neon changes the clip edit screen only; the project list and other editor
  screens stay stock.
