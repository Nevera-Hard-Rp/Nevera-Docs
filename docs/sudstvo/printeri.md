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

## Symptom when the printer isn't running

Notify: *nevera_printeri must be started to view documents.* → `ensure nevera_printeri`, then restart.
