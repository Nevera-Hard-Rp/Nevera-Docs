# Printers — Dependencies

| Resource | Required |
|----------|----------|
| `oxmysql` | **Yes** |
| `ox_lib` | **Yes** |
| `ox_inventory` | **Yes** — item registration, stash slots for placed printers |
| `ox_target` | **Yes** — printer interactions (refill paper/toner, lock, pick up) |
| Framework (QBCore / ESX / Qbox) | **Yes** — auto-detected internally, no bridge file needed |

No separate framework bridge is required — `nevera_printeri` detects QB/ESX/Qbox on its own.

## server.cfg order

```cfg
ensure oxmysql
ensure ox_lib
ensure ox_inventory
ensure ox_target
ensure qbx_core          # or es_extended / qb-core

ensure nevera_printeri
```

**Also running Nevera Court?** Start `nevera_printeri` **before** `Nevera_Court` — Court's document-viewing Use handler calls into it (see [Overview → Optional integration](overview.md#optional-nevera-court-integration)). Not required if you don't own Court.
