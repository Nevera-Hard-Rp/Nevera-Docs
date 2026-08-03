# Nevera Court — Overview

A full **Department of Justice (DOJ)** system for serious legal roleplay on FiveM. Police, prosecutors, defense counsel, judges, clerks, and citizens run criminal and civil procedure end-to-end inside one resource:

- Open and manage cases with auto docket numbers
- Fill, sign, print, and archive official A4 court forms
- Request and execute arrest / search warrants
- Set bail, schedule hearings, run jury selection
- Enter verdicts and issue **commitment orders** (hard RP prison handoff)
- Calculate fines, browse the penal code (NKZ), and log actions to Discord

## Supported frameworks

ESX · QBCore · Qbox · Standalone (`Config.Framework = 'auto'`)

## Languages

`en` · `hr` · `de` · `fr` · `es` — full UI + A4 forms + NKZ titles (`Config.Locale`)

## Dependencies

| Resource | Required |
|----------|----------|
| `oxmysql` | Yes |
| `ox_lib` | Yes |
| Framework (ESX/QB/Qbox) or standalone | Yes |
| `ox_inventory` | Yes (print/archive) |
| **`nevera_printeri`** | Yes — see [Printers](printeri.md) |
| **`bl_bridge`** | Yes — printer dependency |
| `ox_target` | Recommended |

Continue: [Installation](installation.md) · [Staff & Player Guide](court-flow.md) · [Printers](printeri.md) · [Changelog](changelog.md)
