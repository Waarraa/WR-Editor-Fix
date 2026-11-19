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

## Language

On the editor's **front page** (the last rows: **WR Language**, Left / Right), in WR Options -> WR Editor Look ->
**Language** (live), or in the `.ini`:

```ini
Language = English    ; 27 languages + Auto: English, Spanish, French, German, Italian, Portuguese, Dutch, Finnish,
                      ; Swedish, Indonesian, Polish, Turkish, Russian, Ukrainian, Czech, Hungarian, Romanian, Greek,
                      ; Chinese (Simplified), Chinese (Traditional), Japanese, Korean, Thai, Hindi, Bengali, Arabic, Urdu
```

Every language has its own font built in (Chinese, Japanese, Korean, Thai, Hindi, Bengali, Arabic, Urdu ... draw with
their own letters; Arabic and Urdu read right to left). The editor's own texts (the game's menus, alerts, the Export
screen) follow the WR language too - only the bottom-right button hints stay in the game's language for now.

The language of WR Editor Fix in the editor:
- every WR row label and value (Hour / Weather / Freeze / Distance ...);
- the help line under the menu (the long explanations too);
- the WR loading screen (the one shown while the editor starts) and the "Preparing clip" screen.

Labels and help switch the moment you change the language. The loading screens follow it from the next time the
editor loads. **Auto** = your Windows language (English when it isn't one of these). Feature names (WR Garage,
WR Automate, WR Director, WR Shake ...) stay as they are. The game's own rows (Cameras, Edit Camera ...) follow GTA's
own language setting.

> **Tested:** b3095 - German, French, Polish, Turkish and Russian on WR Options, WR Editor Look, WR Automate,
> WR Garage and WR Marker Options (accents, ß, ł, ę, ş, ğ, ı, İ and Cyrillic draw right; every label fits the column).
> Finnish and Russian help lines (the longest, WR Director's START, fits the help box), the Finnish loading screen in
> game, Finnish / Russian / German loading + clip screens in a browser preview.
>
> The translations are first drafts: native speakers, tell us what reads wrong.

Fonts and letters: every WR font shows every language. Where a font doesn't have a letter (Cyrillic in all but
Oswald / Ubuntu Mono, a few Polish / Turkish letters in the decorative fonts), the letter comes from Oswald, sized to
match - Russian in Chakra Petch looks slightly bolder than the Latin letters around it.

## Wallpaper

The picture behind the editor's pages (the front page, an empty project, the clip lists - everywhere the game shows
its grey pattern). On the editor's **front page**, last row **WR Wallpaper**, Left / Right: **WR** (the WR wallpaper,
default), **Drift**, **Inside**, **Canyon**, **Sunset**, or **Rockstar** (the game's own grey background). It changes
right away and is saved (`[Editor Look] Wallpaper`). A clip's preview or playback is never covered - the wallpaper is
only where the game would draw its own background.

## Quick Menu Key and WR Buddy

The last rows of WR Editor Look (v1.1.0):

| Row | What it does |
|---|---|
| **Quick Menu Key** | The key that opens the WR Quick Menu: Enter, then press the new key - saved and working right away. See `18 - WR Quick Menu.md`. |
| **WR Buddy** | On / Off - the WR robot in a corner of the editor. |
| **Buddy Position** | Any corner or the middle of an edge. |
| **Buddy Size** | Small, Medium, Large, Huge. |
| **Buddy Hints** | On = he talks in a speech bubble, Off = he only moves. |
| **Buddy Chatty** | Quiet, Normal, Chatty - how often he does something on his own. |

The WR Buddy rows are on the editor's front page too (under WR Language). See `19 - WR Buddy.md`.

## What saves where

Font, Colors, Header Style, Header Motion, Timeline Size, Language, Wallpaper (and Camera Speed)
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
- Since v1.1.0 the look switches on when the editor opens from FiveM's main
  menu. Opened from a server (ESC -> Rockstar Editor), the editor keeps the
  stock look for that session - it loads before WR Editor Fix switches on.
