# Printers — Installation

## 1. Place the resource

Ships inside the purchased Nevera Court pack, in `Install/companion/`:

```
Install/companion/nevera_printeri  →  resources/[nevera]/nevera_printeri
Nevera_Court (main resource)       →  resources/[nevera]/Nevera_Court
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

`nevera_printeri` needs 10 items registered in `ox_inventory` — 3 printers, paper, and 6 size/color-matched toner cartridges. See [Configuration](configuration.md#required-items) for the full list.

`Install/companion/nevera_printeri/install/` ships a ready-made `ox_items.lua` block using the exact item names the resource expects, plus matching `.png` icons in `install/img/` — paste the block into your `ox_inventory` items and copy the icons over. No need to write the item definitions yourself.

**`document_a4` is owned by Nevera Court, not `nevera_printeri`** — register it from `Install/items/ox_inventory_document_a4.lua` (or `qbx_core_document_a4.lua` for Qbox — same block, since Qbox has no `qbx_core/shared/items.lua`). Do **not** paste a second `document_a4` from the printer's item file.

## 4. Configure printer locations

`Config.PublicPrinters` in `config.lua` is **empty by default** — no printer spawns automatically. Uncomment the example entry and fill in real world coordinates for a fixed public printer, or leave it empty and let staff place printers manually via the in-game placement tool instead.

## Symptom if the printer resource is missing

Notify: *nevera_printeri must be started to view documents.* → `ensure nevera_printeri`, then restart.
