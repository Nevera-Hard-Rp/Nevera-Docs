# Printers — Installation

## 1. Place the resource

Ships inside the purchased Nevera Court pack, in `Install/companion/`:

```
Install/companion/nevera_printeri  →  resources/[nevera]/nevera_printeri
Nevera_Court (main resource)       →  resources/[nevera]/Nevera_Court
```

## 2. SQL (run once)

Import `nevera_printeri/sql/nevera_printeri.sql` — creates the table that tracks placed printers (position, owner, lock state).

## 3. Register the inventory items

`nevera_printeri` needs 10 items registered in `ox_inventory` — 3 printers, paper, and 6 size/color-matched toner cartridges. See [Configuration](configuration.md#required-items) for the full list.

`Install/companion/nevera_printeri/install/` ships a ready-made `ox_items.lua` block using the exact item names the resource expects, plus matching `.png` icons in `install/img/` — paste the block into your `ox_inventory` items and copy the icons over. No need to write the item definitions yourself.

**`document_a4` is owned by Nevera Court, not `nevera_printeri`** — register it from `Install/items/ox_inventory_document_a4.lua` (or `qbx_core_document_a4.lua` for Qbox — same block, since Qbox has no `qbx_core/shared/items.lua`). Do **not** paste a second `document_a4` from the printer's item file.

## 4. Configure printer locations

`Config.PublicPrinters` in `config.lua` ships with one placeholder entry and `coords = vec4(0.0, 0.0, 0.0, 0.0)` — fill in real world coordinates before going live, or remove the entry if you'd rather staff place printers manually via the placement tool.

## Symptom if the printer resource is missing

Notify: *nevera_printeri must be started to view documents.* → `ensure nevera_printeri`, then restart.
