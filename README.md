# Logistic Town

A warehouse logistics routing game for a tool supplier, in a single self-contained HTML file (`index.html`).
Open it in any modern browser. No build step, no external assets: all tools, apparel and station icons are hand-drawn, coloured SVG icons (`CICONS`, layers of `[fill, path]`; UI glyphs stay as line icons in `ICONS`),
and sound and music are generated with the Web Audio API.

## How to play
- Orders arrive on the left and their totes light up in the **Shuttle Warehouse**. Click each glowing tote to send it to
  **Commissioning**, which starts picking once all of the order's totes have arrived.
- Shuttles drive the aisles and bring totes to the lift. Only as many totes as you have shuttles are fetched at
  once (start with 2, upgrade to 5); the rest wait in line. Shuttle count and speed live in `ROBOT` and the warehouse upgrades.
- Click a handling unit (HU), then click its next station (or drag it, or press the station's number key).
- Route each order through only the services it needs: Calibration, Laser Signing, Patching (any order),
  then Focus Customer Care for ★ customers, then Packing & Shipping.
- ⚠ Flagged units (failed checks, wrong picks, failed weight checks on the conveyor) go to Quality Assurance first.
  QA either corrects it (it continues its route, a failed service is redone) or finds the item defective:
  the ✖ box goes to **Retoure** (next to Packing) and a replacement must be commissioned.
- Wrong pick: QA takes the wrong item out as a ↩ return tote. Route it back to the Shuttle Warehouse (key `0`),
  click the order's new glowing tote, and send the HU back to Commissioning for a re-pick.
- Ship before the timer runs out. Five short shifts (Mon–Fri) introduce stations step by step, then endless overtime.
  Stations start slow; the upgrade shop shows how busy each station was, so you can fix bottlenecks.

Keys: `1`–`9` route · `0` warehouse · `Tab` next unit · `H` hints · `F` speed · `Space` pause.

## Adding a station
Everything is data-driven at the top of the script in `index.html`:
1. Add a step to `STEPS` (`stage` sets the order; same stage = any order; `want(order)` decides if an order needs it).
2. Add a station to `STATIONS` with `handles: '<stepId>'` (time, slots, buffers, defect chance, description).
3. Add the station id to the `stations` list of the shifts in `SHIFTS`.
Layout, routing rules, order generation, help screen and the routing board update automatically.

New items go into `ITEMS` with an icon key from `CICONS` (or `ICONS`) and tags: `measure` items can be calibrated, `tool` items
signed, `sewable` clothing patched (a step's `tag` decides which items it applies to).
