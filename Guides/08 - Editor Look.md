# Editor Look - theme, fonts, colours and header

Make the Rockstar Editor yours: the WR Neon Glass theme, 10 built-in fonts,
every colour from a palette, and header art at the top of the menu. It's the
game itself drawing it (built into the plugin), not an overlay on top. Only
while the editor is open - the rest of the game looks stock.

**Game build:** b3258 only. **Ini:** `[Editor Look]`.

> **Tested:** Both themes, fonts, colours and headers, live switching and saving to the ini - one PC, Windows 11.
>
> **Not tested yet:** Other screen resolutions / UI scales.
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
  line, a glowing playhead and diamond markers.
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
both themes. The fonts are free Google Fonts - their licences are in the
`Fonts` folder of the release.

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

## What saves where

Font, Colors, Header Style and Header Motion (and Camera Speed) changed in WR
Options are saved back into their own `[Editor Look]` lines about a second
after your last change, so the next launch starts with them. `Theme` is only
set in the `.ini`.

## Coming from v0.8.0 or older?

`[Editor Look]` replaces `[Editor Theme]`: `EditorTheme`, `EditorFont` and the
old GTA font list (Font5, Font2_cond, RockstarTAG, gtaCash) are gone. Take the
new `.ini`; your old menu colours go into `MenuText` / `MenuTextGreyed`.

## Limits

- Game build b3258 only.
- Neon changes the clip edit screen only; the project list and other editor
  screens stay stock.
