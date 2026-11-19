<!-- MADE BY WR | WARRAA_ -->
<!-- WR EDITOR FIX - CLOSED SOURCE. (c) Warraa / WR - ALL RIGHTS RESERVED. -->
# WR Discord Presence - show your friends you are editing

While the Rockstar Editor is open, your Discord card shows that you are cooking up an edit with WR Editor Fix:

```
Competing in WR Editor Fix
[WR logo]  Cooking up a cinematic edit
           FiveM • Rockstar Editor 🎬
           WR Editor Fix by Warraa
           🎮 0:21
[ WR Editor Fix ]  [ WR YouTube ]
```

> **New in v1.1.0.** **Tested:** in game with the Discord desktop app (Windows), next to FiveM's own Discord card.

## When it shows

- **Only while the editor is open** - from the moment the editor is up until a few seconds after you leave it.
- **Never in normal FiveM play** and never after you join a server.
- It sits **above FiveM's own card** ("Playing FiveM - In the replay editor"). In the member list your name shows
  "WR Editor Fix +1" - the +1 is FiveM's card underneath.
- The **timer** counts from the moment you opened the editor.
- The **buttons** (WR Editor Fix on GitHub, WR YouTube) are for your friends - Discord never shows your own buttons
  to you.

## Good to know

- Discord set to **Invisible** hides every card, the WR one too. Online, Idle and Do Not Disturb show it.
- No Discord running = nothing happens. Start Discord while you edit and the card shows up within about 30 seconds.
- It only talks to the Discord app on your own PC (Discord's local connection, the same one games use). WR Editor Fix
  sends nothing anywhere else, and the card never contains your clip or project names.
- Why "Competing in" and not "Playing"? Discord always puts FiveM's own "Playing" card first, so a "Playing WR Editor
  Fix" card would stay hidden under it. "Competing in" is the one that shows on top.

## Settings

None - WR Discord Presence is always on, with the same card for everyone. Don't want your friends to see it? Set your
Discord status to Invisible or turn off activity sharing in Discord (User Settings > Activity Privacy).

## Not working?

1. Is Discord running on the same PC, and is your status not Invisible?
2. Discord > User Settings > **Activity Privacy**: sharing your activity must be on.
3. Open the editor and wait a few seconds - the card shows once the editor is up.
4. Still nothing? Check `plugins\WR Editor Fix\Logs\WR_Editor_Fix.log` for the `[Discord]` lines and send them with
   your report.
