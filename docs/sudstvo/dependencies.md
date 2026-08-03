# Nevera Court — Dependencies

## Server requirements

| Resource | Required |
|----------|----------|
| `oxmysql` | **Yes** |
| `ox_lib` | **Yes** |
| Framework (ESX / QB / Qbox) or `standalone` | **Yes** |
| Inventory (**ox_inventory** recommended) | **Yes** (print / archive) |
| **`nevera_printeri`** | **Yes** — inventory Use opens the filled form — see [Printers](printeri.md). Self-contained, no separate bridge needed |
| MDT (ps-mdt / tk_mdt / ox_mdt / Advanced) | Optional |
| `ox_target` | Recommended (courthouse zones; F7 works without it) |
| Phone / prison / `peleg-billing` | Optional |

**Optional:** `nevera_menuguard` (soft lock, prevents multiple menus opening at once).

**OneSync** is recommended for a live server.

## Framework compatibility

| Framework | Supported |
|---|---|
| ESX | ✅ |
| QBCore | ✅ |
| Qbox | ✅ |
| Standalone | ✅ (`Config.Framework = 'standalone'`) |

Auto-detected via `Config.Framework = 'auto'`, or set explicitly.

## Inventory bridge

`ox` · `qs` · `qb` · `ps` · `codem` · `tgiann` · `origen` · `ak47` — auto-detected via `Config.Inventory.provider = 'auto'`.

## Phone bridge

LB · Quasar · YSeries · 17mov · GKS · NPWD · qb-phone — auto-detected via `Config.Phone.provider = 'auto'`. Used for notifications only (hearing reminders, warrant alerts); no phone is strictly required.

## MDT bridge

| Provider | Sync level |
|----------|--------|
| `tk_mdt` | Full sync (exports) |
| `advanced` | Partial/Full — requires `provider` + `resourceName` set explicitly, no auto-guess |
| `ps-mdt` | Events + optional patch |
| `ox_mdt` | Events only (API still evolving upstream) |

MDT is entirely optional — the court system works standalone without any MDT connected.
