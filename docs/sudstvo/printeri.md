# Printers (nevera_printeri)

When a player **Use**s a filled `document_a4` in their inventory, **`nevera_printeri`** opens it (renders the filled HTML form). Without this resource, Use on the document does nothing.

`nevera_printeri` is self-contained — it auto-detects QB/ESX/Qbox internally and uses `ox_lib` + `ox_inventory` + `ox_target` directly. No separate framework bridge is required.

## Installation

Ships with the purchased Nevera Court pack, in `Install/companion/`.

```
resources/[nevera]/nevera_printeri/
resources/[nevera]/Nevera_Court/
```

### server.cfg order

```cfg
ensure oxmysql
ensure ox_lib
ensure ox_inventory
ensure ox_target
ensure nevera_printeri
ensure Nevera_Court
```

## Physical printers (map)

Printer objects are placed in the world (small/medium/large) and can be:

- **Public** — anyone can use them
- **Job-restricted** — only a specific job
- **Code-locked** — needs a code set by the owner when locking

The printer consumes paper and toner from the player's inventory; both are refilled via `ox_target` interaction on the printer.

## Required inventory items

| Item | Default name | Notes |
|------|---------------|-------|
| Small printer | `printer_small` | Placeable |
| Medium printer | `printer_medium` | Placeable |
| Large printer | `printer_large` | Placeable |
| Paper | `paper_a4` | Consumed per print |
| Toner — small, B/W | `toner_small_bw` | Fits small printer only |
| Toner — small, Color | `toner_small_color` | Fits small printer only |
| Toner — medium, B/W | `toner_medium_bw` | Fits medium printer only |
| Toner — medium, Color | `toner_medium_color` | Fits medium printer only |
| Toner — large, B/W | `toner_large_bw` | Fits large printer only |
| Toner — large, Color | `toner_large_color` | Fits large printer only |
| Filled document | `document_a4` | Created when a Court form is printed |

Toner is size-**and**-color matched — a printer only accepts the two toner items sized for it. There is no single generic "toner" item.

`Install/companion/nevera_printeri/install/` ships a ready-made `ox_items.lua` block (paste into your `ox_inventory` items) and matching `.png` icons (`install/img/`) using these exact names — no need to write the item definitions yourself.

## Using your own item names

Printer/toner/document item names can be renamed to match your own inventory setup, **as long as you rename them consistently everywhere** — the item name string has to match byte-for-byte in every one of these:

- `install/ox_items.lua` (or wherever you define the item in your inventory)
- `config.lua` — the primary item-name table
- `shared/enums.lua` — `PrinterItemMap` / `DocItemMap`, read directly by the placement and print logic

If any one of these three uses a different name than the other two, printer/document Use silently won't recognize your item — rename all three together, never just one.

## Symptom when the printer isn't running

Notify: *nevera_printeri must be started to view documents.* → `ensure nevera_printeri`, then restart.
