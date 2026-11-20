# Logistic Town

A warehouse logistics routing game for a tool supplier, in a single self-contained HTML file (`index.html`).
Open it in any modern browser. No build step, no external assets; sound and music are generated with the Web Audio API.

## How to play
- Orders arrive on the left and their totes light up in the **Shuttle Warehouse**. Click each glowing tote to send it to
  **Commissioning**, which starts picking once all of the order's totes have arrived.
- Click a handling unit (HU), then click its next station (or drag it, or press the station's number key).
- Route each order through only the services it needs: Calibration, Laser Signing, Patching (any order),
  then Focus Customer Care for ★ customers, then Packing & Shipping.
- ⚠ Flagged units (failed checks, wrong picks, failed weight checks on the conveyor) go to Quality Assurance first.
- Wrong pick: QA takes the wrong item out as a ↩ return tote. Route it back to the Shuttle Warehouse (key `0`),
  click the order's new glowing tote, and send the HU back to Commissioning for a re-pick.
- Ship before the timer runs out. Five shifts (Mon–Fri) introduce stations step by step, then endless overtime.
  Spend earnings on upgrades between shifts.

Keys: `1`–`9` route · `0` warehouse · `Tab` next unit · `H` hints · `F` speed · `Space` pause.

## Adding a station
Everything is data-driven at the top of the script in `index.html`:
1. Add a step to `STEPS` (`stage` sets the order; same stage = any order; `want(order)` decides if an order needs it).
2. Add a station to `STATIONS` with `handles: '<stepId>'` (time, slots, buffers, defect chance, description).
3. Add the station id to the `stations` list of the shifts in `SHIFTS`.
Layout, routing rules, order generation, help screen and the routing board update automatically.
