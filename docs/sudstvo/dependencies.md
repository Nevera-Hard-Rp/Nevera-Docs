# Nevera Court — Dependencies

## Server requirements

| Resource | Required |
|----------|----------|
| `oxmysql` | **Yes** |
| `ox_lib` | **Yes** |
| Framework (ESX / QB / Qbox) or `standalone` | **Yes** |
| Inventory (**ox_inventory** recommended) | **Yes** (print / archive) |
| **`nevera_printeri`** | **Yes** — inventory Use opens the filled form — see [Printers](printeri.md) |
| **`bl_bridge`** | **Yes** — dependency of `nevera_printeri` |
| MDT (ps-mdt / tk_mdt / ox_mdt / Advanced) | Optional |
| `ox_target` | Recommended (courthouse zones; F7 works without it) |
| Phone / prison / `peleg-billing` | Optional |

**Optional:** `nevera_menuguard` (soft lock, prevents multiple menus opening at once).

**OneSync** is recommended for a live server.

### Third-party component: `bl_bridge`

`bl_bridge` is included in the install package as a required dependency of `nevera_printeri`. It is **not our code** — it's an open-source resource by **Byte Labs Studio**, licensed under **GPLv3**.

- Original source / updates: **https://github.com/Byte-Labs-Studio/bl_bridge**
- Included as-is for convenience so the install works out of the box; you're free to grab the latest version from the link above instead.

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
