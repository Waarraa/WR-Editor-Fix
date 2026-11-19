<!-- MADE BY WR | WARRAA_ -->
# WR Buddy - your little editing buddy

Editing alone at 3 AM? Not anymore. **WR Buddy** is a little WR robot who stands in a corner of the editor and keeps
you company: he breathes, blinks, looks around, dances, sneezes, glitches - and says something at the right moment.

> **New in v1.1.0.** **Tested:** b3407 (Warraa) + the WR testers on b3258 / b3095 / b3407. His lines are English for now.

## Where he shows

Everywhere in the editor: the WR launch screen, the editor's menus, the clip loading screen, while you edit and while
you export. He hides when you leave the editor.

- **Click-through:** every click on him goes to the editor - he never takes clicks or the focus.
- **Never in an export:** he is WR Editor Fix's own window over the game, a WR Export only records the game.

## What he reacts to

| You do | He ... |
|---|---|
| Open the editor | says hi (morning, day, evening or late night lines) |
| New / load / close a project, save, quit the editor | reacts to it |
| Open a clip | comments while it loads, and when a clip from another game build opens he tells you |
| Place markers | notices your 1st, 5th, 10th, 25th, 50th and 100th marker - and when you delete a lot |
| Undo / redo | "Oops? Ctrl + Z has your back." |
| Open WR pages | has something to say about WR Automate, Garage, Lights, World, Time & Weather, Director, Shake, Camera ... |
| Run WR Automate | commentates the whole build - yes, there is a siren |
| Export | follows the export: start, 25 / 50 / 75 / 90 %, falls asleep on long ones, cheers when it is done |
| Use the Quick Menu | notices that too |
| Nothing for a while | gets bored, then sleepy |

Between those he does his own thing: fidgets, dances, tips and random lines - how often is up to you (Chatty).

## Settings

On the editor's **front page** (5 rows under WR Language) and in **WR Options > WR Editor Look**:

| Row | Values |
|---|---|
| **WR Buddy** | On (default) / Off |
| **Buddy Position** | Top Left, Top Center, Top Right, Middle Left, Middle Right, Bottom Left, Bottom Center, Bottom Right (default) |
| **Buddy Size** | Small (default), Medium, Large, Huge |
| **Buddy Hints** | On (default) = speech bubbles / Off = he only moves |
| **Buddy Chatty** | Quiet, Normal, Chatty (default) - how often he does something on his own |

Every change works right away and is saved.

## Ini

```ini
[WR Buddy]
Enabled = 1        ; 0 = off
Position = BR      ; TL, TC, TR, ML, MR, BL, BC or BR
Size = Small       ; Small, Medium, Large or Huge
Hints = 1          ; 1 = speech bubbles, 0 = he only moves
Chatty = Chatty    ; Quiet, Normal or Chatty
```

## Good to know

- He never repeats a line he just said, and each reaction has a short cooldown so he never spams.
- His lines are English for now; the WR languages come later.
