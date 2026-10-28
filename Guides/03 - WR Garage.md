<!-- MADE BY WR | WARRAA_ -->
# WR Garage - tune the car inside the editor

Change the paint, livery, lights, plate and body parts of the clip's car
right in the editor, live. The export renders the car exactly as you see it.

**Game builds:** b3258, b3095 and b3407. **Ini:** none - it's in the editor menu.
For a different look from one marker on, see `04 - Car Look per marker.md`.

> **Tested:** A vanilla car: every row, Body Parts, wheels, randomise, Reset, plate text + style; add-on drift cars (their paint slots are mapped their own way); Clean, also in the export; the look saved with the project. Exports: EVE and WR Export.
>
> **Not tested yet:** Motorbikes / boats / aircraft, many add-on cars.
>
> Everything that's supported / tested: `00 - Support and Testing.md`.

## How to open it

Marker menu -> **WR Options** -> **WR Garage** (Enter). **Back** returns to
WR Options.

WR Garage tunes **the car the recorded player drives** (or, if the recorded
focus is a car itself, that car).

## The rows

Every value row starts at **As recorded** (the car exactly as the replay made
it). Left / right steps through the values and the car changes at once.

| Row | Values | What it does |
|---|---|---|
| **Car** | Player's car / No car found | Shows whether a car was found. |
| **Livery** | As recorded, Off, every livery the car has (by name) | The car's own livery designs. A livery covers the body paint - Off shows the colours. |
| **Primary** | 22 colours | Main paint colour. |
| **Secondary** | 22 colours | Second paint colour (stripes, trim, wheels on some cars). |
| **Finish** | Normal, Metallic, Pearl, Matte, Metal, Chrome | Paint finish. |
| **Neon** | 22 colours | Underglow neon, all four sides on. |
| **Xenon** | White, Blue, Electric Blue, Mint Green, Lime Green, Yellow, Golden Shower, Orange, Red, Pony Pink, Hot Pink, Purple, Blacklight | Headlight colour (xenon lights on). |
| **Lights** | On, On + Full Beam, Off | Headlights - for night shots, and to see the xenon colour in daylight. |
| **Window Tint** | None, Pure Black, Dark Smoke, Light Smoke, Limo, Green | Window tint. |
| **Plate Text** | Enter | Opens the game's keyboard: type up to 8 characters, Enter = done, Esc = cancel. Empty = the recorded plate. |
| **Plate Style** | San Andreas, SA Black, SA Blue, SA Plain, SA Exempt, North Yankton, eCola, Las Venturas, Liberty City, LS Car Meet, LS Panic, LS Pounders, Sprunk | The plate's look. |
| **Body Parts** | Enter | Opens the Body Parts page (below). |
| **Randomise Colors** | Enter | Random paint, second colour, finish, xenon, and sometimes neon. Press again for a new roll. |
| **Randomise All** | Enter | Everything random - colours, every body part, wheels and livery. |
| **Clean** | Enter | No dirt, dents + scratches fixed, every decal (wall scrapes too) off - and it stays that way (see "Clean" below). Broken-off parts go back on with the press. |
| **Reset** | Enter | The car back exactly as it was recorded. |

The 22 colours: Black, Graphite, Grey, Silver, White, WR Red, Red, Candy Red,
Orange, Gold, Yellow, Lime, Green, Racing Green, Mint, Cyan, Sky Blue, Blue,
Navy, Purple, Pink, Bronze.

## Body Parts page

WR Garage -> **Body Parts** (Enter) lists every part slot **this car** has -
up to 13 of: Spoiler, Front Bumper, Rear Bumper, Side Skirts, Grille, Hood,
Fenders, Right Fender, Roof, Exhaust, Roll Cage, Suspension, Trunk, Arch
Covers, Aerials, Engine Block, Air Filter, Struts, Tank, Windows, Trim, Plate
Holder, Trim Design, Ornaments, Seats, Steering Wheel, Dashboard. Add-on cars
can name their own slots ("Canards", "Wing" ...) and the page uses those names.

| Row | What it does |
|---|---|
| **A part slot** | Left / right: As recorded, Stock, then every part the car has (by its name). |
| **Wheel Type** | Sport, Muscle, Lowrider, SUV, Offroad, Tuner, Bike, High End, Benny's Original, Benny's Bespoke, Open Wheel, Street, Track. Picking one puts its first rim on. |
| **Rims** | The rim, from the wheel type above. |
| **Randomise Parts** | Enter: every part slot, the wheel type and the rims random. The livery stays. |

**Back** returns to WR Garage.

## Clean

Press **Clean** once and the car stays clean: no dirt, no dents or scratches,
no decals (black wall scrapes, bullet holes). It stays on through everything -
your other Garage changes, marker looks, the export, and the project opened
again later (it's saved with the look). If the replay puts scrapes or damage
back while the clip plays, they are taken off again right away.

Parts that broke off in the recording (a bumper on the road) go back on only
when you press Clean. Reset turns Clean off.

## In the export

The look is applied to the car the replay makes, so it is in your export too.
If the replay makes the car again (jumping back past the moment it appears,
starting an export) the look goes straight onto the new car, and if the replay
puts its own paint or plate back, the look goes back on the same frame.

## Tips

- Use a **vanilla car** to see every row do exactly what it says. Add-on cars
  map their paint slots their own way (for example the second colour may
  colour the headlight glass, or the xenon colour may do nothing).
- A livery hides the body paint: set Livery = Off to see Primary / Secondary.
- Xenon colours show best at night - use Lights = On, or set the time with WR
  Options -> Hour.
- Randomise All, press again, again... Reset when you've had enough.

## Limits

- Saved with your project (`WR Editor Fix\Projects\<project name>.json`): open the project again and the look is back.
- Only the player's car (or the focused car) - other cars in the clip later.
- Broken-off parts go back on only when you press Clean (dents, scratches,
  scrapes and dirt stay off by themselves).
