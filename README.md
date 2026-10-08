# Pocketopolis

An isometric city-building game that runs in a single HTML file, inspired by SimCity.
This README records everything that was built and changed on **7 October 2026**.

## Files

| File | What it is |
|---|---|
| `pocketopolis-v3.7.html` (same as `pocketopolis.html`) | **Current build (v3.7).** Admin-only test build with a more realistic look (High graphics) and a Graphics quality setting. |
| `pocketopolis-v3.6.html` | v3.6: connected-but-empty zones say why (paused, no demand, waiting). Superseded by v3.7. |
| `pocketopolis-v3.5.html` | v3.5: zones easier to see, with missing road/power/water icons. Superseded by v3.6. |
| `pocketopolis-v3.4.html` | v3.4: easier, clearer land buying. Superseded by v3.5. |
| `pocketopolis-v3.3.html` | v3.3: admin access settings. Superseded by v3.4. |
| `pocketopolis-v3.2.html` | v3.2: version 3 land, money and rent, with every building unlocked for admins. Superseded by v3.3. |
| `pocketopolis-v3.1.html` | v3.1: admin full access (every lot open, unlimited money). Superseded by v3.2. |
| `pocketopolis-v3.0.html` | v3.0, before admin full access became the default (kept for reference). |
| `pocketopolis-v2.html` | v2.0, the admin build before land lots, rent and the sky (kept for reference). |
| `pocketopolis-v1.html` | First release (v1.0). No passcode, fewer buildings, cartoon look. |
| `README.md` | This file. |

All game files are self-contained: open them in a modern browser. The only outside request is the Google font, which falls back to a system font if it cannot load.

The current build (v3.7) is also published as a private page at https://claude.ai/artifact/37piMfGjMUDhTabYYPMWY7 (visible only to its owner unless shared).

## Version history (7 Oct 2026)

### v1.0: first release
Requested: *"Create a building simulator in html where I can play designing my own town, using SimCity as the reference."*

- Isometric canvas city with a random river and lake; roads over water become bridges.
- Zoning (Residential, Commercial, Industrial) with buildings that grow through 3 levels.
- Power and water networks that follow roads; brownouts and dry taps shrink buildings.
- Services: police, fire station, school, hospital, parks, plaza, stadium.
- Economy: monthly budget, tax slider, upkeep, and population milestones that unlock buildings and pay a bonus.
- Advisor ("Hoot") that gives next-step hints; inspector with resident quotes; map views (power, water, land value, pollution, crime, fire cover).
- Cars on the roads, day/night cycle with lit windows and street lamps, sound effects.
- Disasters and fun: meteor, fire, tornado, fireworks.
- Save/load (browser storage), sandbox mode, light/dark interface theme.

Fixes made before delivery, after a headless test run:
- Rebuilt the stadium so the rim and inner field draw correctly.
- Budget tax slider no longer resets while dragging.
- Residential demand can no longer crash a city that builds homes before jobs.
- Softened smoke puffs that looked like solid blobs.
- Removed the internal test hook from the shipped file.

Also delivered: the file was sent into the chat on request ("send it here").

### v2.0: admin test build
Requested: make the game admin-access only for testing; add more buildings and decorations; make it realistic; make the game follow world time.

**Admin access**
- Passcode screen before the game loads. The passcode is stored only as a salted, repeated SHA-256 hash, not in plain text.
- Five wrong attempts lock the screen for 30 seconds or more.
- Admin tools panel (🛠): add money, sandbox mode, unlock all buildings, free power and water, max zone demand, upgrade zones, skip a month or year, clear fires, wipe the city, max happiness, force weather or season, set the hour, time lapse, trigger disasters, performance and tile-coordinate readouts, export and import saves, sign out.
- Important: this is a **client-side** check for a testing build. It keeps casual visitors out but cannot stop someone who reads the page source. Keep the link private for real access control.

**New buildings (11)**
- Utilities: solar farm, gas plant, water treatment plant.
- Civic and transit: chapel, library, town hall, train station (animated train), museum, university.
- Landmarks: lighthouse (shoreline only, rotating night beam) and an animated Ferris wheel.
- They affect power, water, education, land value, happiness, crime, demand and tourism income. Budget now includes a Tourism line.

**New decorations (14), in a Decor tab**
Oak tree, pine grove, flower garden, hedge garden, bench, street lamp, statue, fountain, duck pond, playground, picnic spot, market stall, bus stop, windmill. Each gives a small land-value lift. Ambient extras: boats on the water, bird flocks, drifting cloud shadows, grass tufts, flowers and rocks.

**Realistic version**
- Muted real-world colour palettes and richer building details (doors, chimneys, rooftop equipment).
- Shadows cast by the sun, with golden-hour, dusk, night and overcast lighting.
- Crosswalks and lane markings, railed bridges, shoreline foam and water glints.
- Construction phase with cranes when buildings are built or upgraded.
- Buses and vans in the traffic.
- Seasons change grass and trees (spring blossom, autumn leaves, snow in cold-region winters).
- Weather: clear, cloudy and rain.
- Currency symbol changed from `§` to `$`.

**World time**
- The game follows real date and time in a chosen time zone (defaults to the device's zone). A world clock in the top bar shows it, and the menu has a time zone picker.
- Sun position is calculated from the date, time and latitude. Night, shadows, seasons (flipped for the southern hemisphere), rush-hour traffic and the evening power peak all follow the clock.
- Solar farms follow the real sun: no output at night, less under cloud.
- The simulation's own month counter (used for budgets) is separate from the world date.

**Fixes during v2.0**
- Setting the hour from the admin panel now refreshes the clock first, so it cannot be thrown off by a stale reading.
- Passcode correction: an early message in the chat gave a wrong string (the hash salt) instead of the passcode. The real passcode was then sent in the chat. It is deliberately **not** written in any file.

### v3.0: land lots, rent, rivers, sky and zoom
Requested: more buildings where every building earns rent; lots you have to buy to expand; adding water (rivers) and land; a realistic sky with clouds; and zoom.

**More buildings, and every building earns rent**
- 11 new buildings: hotel, shopping mall, cinema, bank, café, fuel station, data center, farm, harbor (shoreline only), post office and sports centre. They sit in a new **Business** tab (post office in Civic, sports centre in Parks & Fun).
- Every finished building now pays monthly **rent** to the city: homes, shops, factories, utilities, civic buildings, parks, landmarks and even decorations. Rent scales with land value; a building without power or water pays only 35%. Roads do not pay rent (they only cost upkeep).
- Little gold "+$" coins rise from buildings when rent comes in. A new **Rent** map view shows where the money comes from, the inspector shows each tile's rent, and the budget now lists rent by category plus a land tax ($18 per owned lot per month).
- New buildings affect power, water, land value, shop and industry demand, happiness and tourism (the hotel adds tourism income).

**Land lots you must buy**
- The map is an 8 by 8 grid of 6 by 6 tile lots (64 lots). You start with a small 2 by 2 plot of lots near the middle, chosen for the most land.
- You can only build on lots you own. **Buy lot** (Land & Rivers tab) purchases a lot that touches your land. Prices rise as you own more and are lower for lots that are mostly water.
- Lots that are not for sale yet stay hidden in the sky. Lots next to your land appear as buyable plots with a "FOR SALE" sign, gold dashed borders and a price tag.
- Saves keep your lots. Older v2 saves load with every lot owned.

**Rivers and land**
- **Dig water** turns an empty land tile into a river or lake ($50). **Add land** fills water with land ($70). Both only work on lots you own, and you must clear buildings (or remove a bridge) first.
- Shorelines, water depth, foam and boats update as you reshape the land. Terrain changes are saved.

**Realistic sky with clouds**
- The land now floats in a sky. The sky colour follows the real sun: blue day, orange sunset, deep blue night.
- Real moon phase from the date, stars at night, a sun with a glow, and layered drifting clouds that tint at dawn, dusk and night and grow heavier with the weather.
- Cloud shadows drift across the land only.
- The land has soil-layer cliffs along its edge, and the camera starts framed on your land.

**Zoom**
- Zoom range 30% to 350%, with smooth zoom: mouse wheel, pinch, the new **+ / &minus; / fit** buttons, the `+` `-` keys, and `0` to fit your city. Double-click with the Pan tool zooms in at the cursor (Shift to zoom out).
- Zoomed in, you can see pedestrians walking along the pavements. Their numbers follow the time of day and drop in the rain.

**Fixes during v3.0 testing**
- Cloud shadows were drawing over empty sky as dark smudges; they are now clipped to the land.
- Clouds were too big and blurry; they are smaller and crisper.
- Rent coin text no longer grows huge when zoomed in.

Testing for v3.0: a headless run checked 15 things (start with 4 lots, building on unowned land refused, buying only next to your land with rising prices, no purchase without money, dig and fill water with shoreline updates, all new buildings placing, every finished building paying rent, rent coins, zoom limits, save/load keeping lots) and all passed with no script errors. It also rendered day, night, sunset, zoomed-in and buy-lot views for visual checks.

### v3.1: admins get full access by default
Raised by the project owner: *"Isn't it supposed to be that admins can access all materials?"* That was a gap: in v2.0 and v3.0 the admin panel had switches for unlocking everything, but they were off by default, so a signed-in admin still met locked buildings, unowned lots and a limited budget.

- Signing in now turns on **Full admin access** automatically: every building, tool and decoration is unlocked, every lot is open (visible and buildable without buying), and money is unlimited so building is free.
- A single **Full admin access** switch at the top of Admin tools turns it off, which restores the normal rules (population unlocks, buying lots, a real budget) so progression can still be tested. Turning it back on restores everything. Switching off sets money to at most $50,000.
- Loading a save or starting a new city keeps full access while it is on. Your lot ownership is not overwritten, so it comes back unchanged when you switch access off.
- Help text now explains this.
- Testing: a headless run checked 15 things (access on after sign-in, unlimited money, all 68 tools unlocked, all 64 lots open, building on an unpurchased lot, building the highest-unlock building from the start, free building, switch off restores normal rules, switch back on, master switch in the panel, save/load) and all passed with no script errors.

### v3.2: version 3 experience, with every building unlocked for admins
Raised by the project owner: *"Version 3 is much better than the others... apply the changes of version 3 in version 3.1."* In v3.1 the **Full admin access** switch opened every lot and gave unlimited money, which hid the things that made v3 better: the small floating plot, "For sale" lots, buying land, and a real money and rent economy.

- Admins keep **every building, tool and decoration unlocked** (the "access all materials" request from v3.1).
- **Land, money and rent work as in version 3 again:** you start with 4 lots and $20,000, other lots stay hidden or for sale next to your land, and you buy land to expand. The floating-island sky view is back as the default.
- The single master switch is gone. Admin tools now has three independent switches: **Unlock every building and tool** (on by default), **Open every lot** (off), and **Unlimited money and free building** (off). Turn on the last two when you want to test without limits.
- Loading a save keeps the version 3 land and money rules.
- Testing: a headless run checked 15 things (all buildings unlocked, 4 starting lots, 12 of 64 lots visible, normal $20,000 start, for-sale signs, building refused on unbought land, buying a lot costs money, the three switches, open-every-lot and unlimited-money toggles, unlock toggle, save/load) and all passed with no script errors.

### v3.3: admin access with settings to enable or disable it
Raised by the project owner: *"Enable all the items and the money should be infinite since it is admin access. Or put in the settings that you can enable and disable the access for admin."*

- Admins now start with **every building, tool and decoration unlocked** and **unlimited money** (building is free; lots also cost nothing).
- Land still works as in version 3: you start with a small plot, other lots are hidden or for sale next to your land, and you expand by buying lots. (Lots are free for admins while unlimited money is on.)
- New **Admin access** section at the top of Admin tools (also reachable from the menu entry "Admin access & tools", which shows the current status):
  - **Enable everything** (renamed *Enable items & money* in v3.4) and **Normal rules** buttons.
  - Three switches: all items unlocked, unlimited money, every lot open.
  - Choices are remembered on the device and applied at the next sign-in, after loading a save, and for new cities.
- Defaults when nothing has been saved: items unlocked on, unlimited money on, every lot open off.
- Testing: a headless run checked 15 things (defaults, infinite money, 68 of 68 items unlocked, version 3 land with 4 lots, free lot purchase, building the highest-unlock building immediately, each switch, both preset buttons, settings remembered, loading a save, menu status) and all passed with no script errors.

### v3.4: easier, clearer land buying
Raised by the project owner: *"Why I cannot buy the land?"*

I could not reproduce a failure: in a simulated browser, a mouse click and a touch tap on a "For sale" lot with the Buy lot tool both bought it. Looking at the flow, there were several ways to get stuck, so this version fixes them:
- **Another way to buy:** with the Inspect tool, tap any "For sale" lot and press the new **Buy this lot** button in the card (it shows the price; free for admins while money is unlimited).
- **Clearer messages.** Tapping an unbought lot with a build tool now says how to buy it. Buying a lot that does not touch your land says to look for the FOR SALE signs. The messages stay on screen a little longer.
- **"Every lot open" message:** if that switch is on, buying now explains that every lot is already open and where to switch it off (before, the message was easy to miss and looked like buying was broken).
- **"Enable everything" is now "Enable items & money".** It no longer turns on "Every lot open", so the for-sale lots stay in place. Open every lot remains its own switch.
- Testing: a headless run checked real clicks and taps (mouse buy, touch buy, inspector button, button disappears after buying, clearer message on a build tool, the open-every-lot message, the changed preset) and all passed with no script errors.

### v3.5: zones and buildings are easier to see
Raised by the project owner: *"The zone tab, like the building are not showing up in the map."*

I could not reproduce a total failure. In a simulated browser, dragging a road, power, water and zones with real clicks made buildings grow within about 12 seconds, and a browser-strict canvas raised no drawing errors. But the test showed several ways it can look like nothing is happening, so this version fixes them:
- **Zones are much more visible:** stronger Residential (green), Commercial (blue) and Industrial (yellow) colours, a thicker outline and an **R / C / I** letter on every empty zone tile. Before, the green zone tint was close to the grass colour.
- **The map now says what a zone is waiting for:** a small icon on each empty zone shows 🛣️ no road within 2 tiles, ⚡ no power, or 💧 no water.
- **Power or water that is not touching a road is flagged** with a 🛣️ icon. In my own test the power and water were three tiles from the road, so nothing grew, which is an easy mistake to make.
- **First-time hint:** the first time you zone without a road, power or water, a message explains that zones only turn into buildings beside a road with power and water.
- **Closer starting view:** the camera starts framed tighter on your land (about 96% instead of 67% in the test), so buildings are not tiny.
- **Safer drawing:** if one item ever fails to draw, the rest of the map still draws, and a message tells you to check the browser console. Before, an error could have stopped the whole picture.
- Help text now explains zones and the icons.
- Testing: a headless run with real clicks checked the road, zones, hint, empty-zone icons, flagged power and water, and growth into buildings once connected. All passed with no script errors.

If zones still look empty for you, the most likely reasons are no road within 2 tiles, no power or water connected to the road, the game paused, or the browser tab in the background.

### v3.6: a zone that is connected but empty now says why
Raised by the project owner, with a screenshot: an L-shaped road, a wind turbine, a water tower and one Commercial zone beside the road, still empty. *"Why is it still like this?"*

The screenshot showed no ⚡ 💧 🛣️ icon, so the game considered the zone connected to a road with power and water. I rebuilt that exact scene: the zone built in about 4 seconds on average (about 18 seconds in the slowest of 30 trials), so I could not reproduce a stuck zone. A connected zone can still stay empty for three reasons that the map did not show:
- **The game is paused** (for example, Space was pressed).
- **There is no demand yet** for that zone type (the R / C / I bars show demand).
- **Builders have not arrived yet:** each zone tile has a small random chance to start building every tick.

So this version shows the reason on the map:
- ⏳ on an empty connected zone: everything is connected and builders are coming.
- 📉: there is no demand for that zone type yet.
- ⏸️: the game is paused.
- A **"Paused" banner** at the top of the map. Click it (or press Space) to resume.
- Help text explains all the icons.
- Testing: a headless run checked the paused banner and icon, resuming from the banner, the no-demand icon, the waiting icon, the no-road icon, and that a built zone loses its icon. All passed with no script errors.

If a zone still looks stuck, look at the icon on the zone and the R / C / I demand bars (top left of the map).

### v3.7: a more realistic look (High graphics)
Requested: *"Can you make the map more realistic looking?"*

The game is still a 2D isometric picture, so this is realism within that style. New **High graphics** (the default) adds:
- **Seamless, textured ground.** All natural ground and water is now drawn as merged shapes with a grass texture across the whole land, so the visible tile seams are gone. Parks get the same texture.
- **Living water.** Water has moving ripples in two directions, sun glitter that depends on the real sun and cloud, and a reflection of the current sky colour (orange at sunset), plus the existing shoreline foam.
- **Lighting that follows the sun.** The two visible sides of every building are lit differently through the day (the left side is brighter in the morning, the right in the evening), and flatter at night and under cloud.
- **Sky reflected in the glass.** Windows take on the colour of the sky: blue at midday, warm at sunset, grey when overcast.
- **Softer, more natural shadows** with soft edges, and a contact shadow where buildings meet the ground.
- **Better building shading:** edge highlights, edge shade lines on corners, and shingle courses on roofs when zoomed in.
- **Fuller trees:** shaded canopies with highlights.
- **Depth haze:** the far (upper) part of the land is slightly softer and bluer.
- **Smarter map icons:** the status bubbles stay small when you zoom in.
- **Graphics quality setting** in the menu: High (realistic) or Standard (the previous look, faster). It is remembered on the device. If a device runs High slowly for a while, the game switches itself to Standard and tells you; choosing High again in the menu turns that automatic switch off.
- Testing: a headless run rendered a developed town in High and Standard at noon, golden hour, night, rain and autumn, and zoomed in close, on a canvas that throws the same errors as a real browser. Everything rendered with no errors, and the menu setting switched back and forth and was saved. In that slow software test, High took about 30% longer per frame than Standard. That is not a real graphics chip, so actual speed will differ. I checked the pictures at noon, golden hour and in a close-up, and fixed two problems found along the way (shadows that were far too dark, and oversized status bubbles when zoomed in).

## Controls

- Drag to paint roads, zones, parks and some decorations; click to place everything else.
- Scroll, pinch or use the + / − / fit buttons to zoom (30%-350%); right-drag, the Pan tool or two fingers to pan; arrow keys also pan.
- Keys: `Q` inspect, `R` road, `B` bulldoze, `1` `2` `3` zones, `P` park, `W` wind turbine, `E` water tower, `G` cycle map views, `Space` pause, `+` `-` zoom, `0` fit city, `Esc` back to Inspect.

## Known limitations

- The passcode gate is not real security (see above).
- Testing was done headless (a simulated browser). It has not been tried with a real mouse, touch screen, or on a phone.
- Solar farms can cause blackouts at night by design; pair them with wind, gas or coal.
- Saves live in the browser's own storage, so they are per browser and per device.
- Economy balance (rent, lot prices, land tax) is my own estimate and has not been play-tested over a long game.
- Land beyond your lots is hidden until it is next to your land, unless you switch on Open every lot in Admin tools.
- The Admin tools menu entry and button are available to anyone who gets past the passcode.
- Rent and budget balance can only be judged with unlimited money switched off (use Normal rules in Admin access).
