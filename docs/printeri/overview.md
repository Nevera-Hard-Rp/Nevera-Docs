# Printers (nevera_printeri) — Overview

**`nevera_printeri`** is a standalone printer system for FiveM. Players place physical printers (small / medium / large), load paper and toner, and print documents that can be Used from the inventory to view.

## What it does

- Places physical printer objects in the world, or lets staff place their own with the in-game placement/rotation tool
- Consumes paper and toner per print, matched to printer size and B/W vs. Color
- Optional lock-code system so a printer can be restricted to whoever set the code
- Public / job-restricted / private (owner-only) access per printer
- Renders printed documents (business card / A5 / A4) as a viewable in-game document on inventory Use
- Print history / audit log per printer
- Ships its own SQL tables for tracking placed printers and print history

## Relationship to other resources

`nevera_printeri` is self-contained — it auto-detects QBCore / ESX / Qbox internally and talks to `ox_lib`, `ox_inventory`, and `ox_target` directly. **No separate framework bridge is required, and no other Nevera product is required to run it.**

### Optional: Nevera Court integration

If **Nevera Court** (the DOJ/legal roleplay system) is also installed and running, `nevera_printeri` automatically detects it (`GetResourceState('Nevera_Court')`) and can render Court's official filled A4 forms when a player Uses a printed `document_a4` — no manual setup required, and `nevera_printeri` never fails or errors if Court isn't present. This is a one-way, fully optional integration between two independent products:

- Buy `nevera_printeri` alone and it works completely on its own.
- Buy Nevera Court too and printing/viewing its official documents starts working automatically.
- Court's own `document_a4` item registration takes priority if both are installed — see [Installation → Register the inventory items](installation.md#3-register-the-inventory-items) for how to avoid a conflicting duplicate item definition.
