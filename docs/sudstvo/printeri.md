# Printers (nevera_printeri + bl_bridge)

When a player **Use**s a filled `document_a4` in their inventory, **`nevera_printeri`** opens it (renders the filled HTML form). Without this resource, Use on the document does nothing.

`nevera_printeri` depends on **`bl_bridge`** (framework/inventory/target bridge) — the printer will not start without it.

## Installation

Both resources ship with the purchased Nevera Court pack, in `Install/companion/`.

```
resources/[nevera]/bl_bridge/
resources/[nevera]/nevera_printeri/
resources/[nevera]/Nevera_Court/
```

### server.cfg order

```cfg
setr bl:framework   "qbx"     # qb | esx | qbx
setr bl:inventory   "ox"
setr bl:target      "ox"
setr bl:context     "ox"
setr bl:progressbar "ox"
setr bl:radial      "ox"
setr bl:notify      "ox"
setr bl:textui      "ox"

ensure bl_bridge
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

Notify: *nevera_printeri must be started to view documents.* → `ensure nevera_printeri` (and `bl_bridge`), then restart.
