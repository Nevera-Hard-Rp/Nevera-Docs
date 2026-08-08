# Printers (nevera_printeri) — Overview

**`nevera_printeri`** is the companion resource that renders filled court documents in-game. When a player **Use**s a filled `document_a4` in their inventory, `nevera_printeri` opens it and displays the completed HTML form.

Without this resource running, Use on a printed document does nothing — the document sits in the inventory but can never be read.

## What it does

- Places physical printer objects (small / medium / large) in the world, or lets staff place their own
- Consumes paper and toner per print, matched to printer size and B/W vs. Color
- Optional lock-code system so a printer can be restricted to whoever set the code
- Renders `document_a4` (and other formats) as a viewable in-game document on inventory Use
- Ships its own SQL table for tracking placed printers

## Relationship to Nevera Court

`nevera_printeri` is self-contained — it auto-detects QBCore / ESX / Qbox internally and talks to `ox_lib`, `ox_inventory`, and `ox_target` directly. **No separate framework bridge is required.**

It ships inside the Nevera Court package (`Install/companion/nevera_printeri`) so document printing works out of the box. Court owns and creates the `document_a4` item; `nevera_printeri` is what makes Use on that item actually do something.
