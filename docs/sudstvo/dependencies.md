# Nevera Court — Dependencies

## Server requirements

| Resource | Required |
|----------|----------|
| `oxmysql` | **Yes** |
| `ox_lib` | **Yes** |
| Framework (ESX / QB / Qbox / OX_Core) or `standalone` | **Yes** |
| Inventory (**ox_inventory** recommended) | **Yes** (print / archive) |
| [`nevera_printeri`](/docs/printeri/overview.md) | **Optional, sold separately** — inventory Use opens the filled form; without it a printed document stays in the inventory but can't be viewed. Self-contained, no separate bridge needed |
| MDT (ps-mdt / tk_mdt / ox_mdt / Advanced) | Optional |
| `ox_target` | Recommended (courthouse zones; F5 panel key works without it) |
| Phone / prison / `peleg-billing` | Optional |

**Optional:** `nevera_menuguard` (soft lock, prevents multiple menus opening at once).

**OneSync** is recommended for a live server.

## Framework compatibility

| Framework | Supported |
|---|---|
| ESX | ✅ |
| QBCore | ✅ |
| Qbox | ✅ |
| OX_Core | ✅ (`Config.Framework = 'ox'`) |
| Standalone | ✅ (`Config.Framework = 'standalone'`) |

Auto-detected via `Config.Framework = 'auto'`, or set explicitly.

## Inventory bridge

Auto-detected via `Config.Inventory.provider = 'auto'`.

| Tier | Providers | Support level |
|------|-----------|----------------|
| **Tested** | `ox_inventory` · `qb-inventory`/`qbox` · `ps-inventory`/`lj-inventory` | Fully verified against real installs. Recommended for production. |
| **Compatibility layer** | `qs-inventory` · `tgiann-inventory` · `codem-inventory` · `origen-inventory` · `ak47_inventory` | Built from the provider's own published exports/docs, best-effort. Should work, but not verified against a live install — if something's off, tell us in support and we'll fix it. |

## Phone bridge

LB · Quasar · YSeries · 17mov · GKS · NPWD · qb-phone — auto-detected via `Config.Phone.provider = 'auto'`. Used for notifications only (hearing reminders, warrant alerts); no phone is strictly required.

## MDT bridge

| Provider | Sync level |
|----------|--------|
| `tk_mdt` | Full sync (exports) — tested |
| `ps-mdt` | Felon check + `OpenMDT` via exports (tested); warrants/cases/verdicts via events only — ps-mdt has no public export for creating those, a community patch can listen for `ps-mdt:server:nevera*` |
| `advanced` | Partial/Full — requires `provider` + `resourceName` set explicitly, no auto-guess |
| `ox_mdt` | Events only — ships no public exports upstream, so `nevera_court:mdt:*` / `ox_mdt:nevera:*` events fire for a community patch to consume |

MDT is entirely optional — the court system works standalone without any MDT connected.
