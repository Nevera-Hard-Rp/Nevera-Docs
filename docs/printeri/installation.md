# Printers — Installation

## 1. Place the resource

```
resources/[nevera]/nevera_printeri/
```

## 2. SQL (run once)

Import `nevera_printeri/sql/nevera_printeri.sql` — creates the two tables the resource needs: `nevera_printeri` (placed printers — position, owner, lock state, print count) and `nevera_dokumenti` (print history / audit log).

> **Upgrading an install from before this schema fix?** Run this instead of re-importing the full file — `CREATE TABLE IF NOT EXISTS` won't add columns to a table that already exists:
> ```sql
> ALTER TABLE `nevera_printeri` ADD COLUMN `total_prints` INT(11) NOT NULL DEFAULT 0;
> ALTER TABLE `nevera_dokumenti` ADD COLUMN `char_name` VARCHAR(60) NOT NULL DEFAULT '';
> ALTER TABLE `nevera_dokumenti` ADD COLUMN `print_mode` ENUM('bw','color') NOT NULL DEFAULT 'bw';
> ```

## 3. Register the inventory items

`nevera_printeri` needs 11 items registered in `ox_inventory` — 3 printers, paper, 6 size/color-matched toner cartridges, and the `document_a4` item it prints to. See [Configuration](configuration.md#required-items) for the full list.

`nevera_printeri/install/` ships a ready-made `ox_items.lua` block using the exact item names the resource expects, plus matching `.png` icons in `install/img/` — paste the block into your `ox_inventory` items and copy the icons over. No need to write the item definitions yourself.

**Already own Nevera Court too?** Its own `document_a4` item takes priority for Court's official documents — replace the `document_a4` entry from `nevera_printeri/install/ox_items.lua` with Court's version from `Install/items/ox_inventory_document_a4.lua` instead (or `qbx_core_document_a4.lua` for Qbox). Only one `document_a4` definition can exist in `items.lua` at a time — a second one silently overrides the first and breaks Use on whichever one lost.

## 4. Configure printer locations

`Config.PublicPrinters` in `config.lua` is **empty by default** — no printer spawns automatically. Uncomment the example entry and fill in real world coordinates for a fixed public printer, or leave it empty and let staff place printers manually via the in-game placement tool instead.

## Symptom if the printer resource is missing

Notify: *nevera_printeri must be started to view documents.* → `ensure nevera_printeri`, then restart.
