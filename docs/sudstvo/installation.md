# Nevera Court — Installation

Use the buyer pack under `Install/` (SQL, items, companion printer, Discord convars, guides) that ships with the resource.

## 1. Place the resources

```text
resources/[nevera]/Nevera_Court/          ← this resource
resources/[nevera]/nevera_printeri/       ← optional, sold separately — see Printers docs
```

Use the **exact folder name** in `ensure`. Printer / NUI paths resolve with `GetCurrentResourceName()`.

## 2. Database

Same schema for every framework — run in order:

```text
Install/sql/01 → 02 → 03 → 04
```

| File | What |
|------|------|
| `01_nevera_court.sql` | Tables + `title_hr/de/fr/es` columns |
| `02_seed_laws_english.sql` | English NKZ base (~93) |
| `03_seed_laws_i18n.sql` | HR + DE + FR + ES titles |
| `04_first_supreme_court.sql` | First Supreme Court admin |

Edit `04_first_supreme_court.sql`:
- QB/Qbox: short `citizenid`
- ESX: exact `users.identifier` (e.g. `char1:…`) — must match 1:1

**Verify:**

```sql
SELECT COUNT(*) AS categories FROM doj_law_categories;  -- expect 9
SELECT COUNT(*) AS laws FROM doj_laws;                  -- expect ~93
SELECT * FROM doj_roles WHERE role = 'supreme_court';
```

## 3. Inventory item (`document_a4`)

| Inventory | File |
|-----------|------|
| **ox_inventory** (QB / Qbox / ESX) | `Install/items/ox_inventory_document_a4.lua` → `ox_inventory/data/items.lua` |
| **Qbox (`qbx_core`)** | same ox block — `qbx_core` has no `shared/items.lua` — see `Install/items/qbx_core_document_a4.lua` |

Copy `Install/items/document_a4.png` → `ox_inventory/web/images/`.

**Critical:**

```lua
consume = 0,                           -- otherwise Use DELETES the item
stack = false,
export = 'Nevera_Court.viewDocument',  -- MUST match folder name (case-sensitive)
```

## 4. server.cfg

```cfg
ensure oxmysql
ensure ox_lib
ensure ox_target
ensure ox_inventory
ensure [your-framework]   # es_extended / qb-core / qbx_core

ensure nevera_printeri    # optional, sold separately — order doesn't matter, runtime check
ensure Nevera_Court       # exact folder name
```

If you own `nevera_printeri`, also run its `sql/nevera_printeri.sql` once.

## 5. First-boot checklist

- [ ] NKZ: 9 categories, ~93 laws
- [ ] `Config.Locale` + `Config.Framework = 'auto'` (or `'esx'` / `'qb'` / `'qbox'`)
- [ ] Supreme Court in `doj_roles` (ESX: id = `users.identifier`)
- [ ] `document_a4` with `consume = 0` + correct `export`
- [ ] `nevera_printeri` installed and started (optional, needed to view printed documents)
- [ ] Print → inventory → **Use** → filled document
- [ ] Courthouse coords / archive passwords / webhooks configured for your map

Ran into a problem after installing? See [Troubleshooting](troubleshooting.md).

Next: [Configuration](configuration.md) to set fine amounts, map locations, and archive passwords for your server.
