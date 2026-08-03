# Nevera Court — Installation

Use the buyer pack under `Install/` (SQL, items, companion printer, Discord convars, guides) that ships with the resource.

## 1. Place the resources

```text
resources/[nevera]/Nevera_Court/          ← this resource
resources/[nevera]/bl_bridge/             ← copy from Install/companion/bl_bridge
resources/[nevera]/nevera_printeri/       ← copy from Install/companion/nevera_printeri
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

# bl_bridge (required by nevera_printeri) — Qbox example:
setr bl:framework   "qbx"
setr bl:inventory   "ox"
setr bl:target      "ox"
setr bl:context     "ox"
setr bl:progressbar "ox"
setr bl:radial      "ox"
setr bl:notify      "ox"
setr bl:textui      "ox"

ensure bl_bridge          # from Install/companion/
ensure nevera_printeri    # from Install/companion/ — before Court
ensure Nevera_Court       # exact folder name
```

Also run `nevera_printeri/sql/nevera_printeri.sql` once.

## 5. First-boot checklist

- [ ] NKZ: 9 categories, ~93 laws
- [ ] `Config.Locale` + `Config.Framework = 'auto'` (or `'esx'` / `'qb'` / `'qbox'`)
- [ ] Supreme Court in `doj_roles` (ESX: id = `users.identifier`)
- [ ] `document_a4` with `consume = 0` + correct `export`
- [ ] `bl_bridge` + `nevera_printeri` copied and started
- [ ] Print → inventory → **Use** → filled document
- [ ] Courthouse coords / archive passwords / webhooks configured for your map

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Resource won't start | Check `oxmysql` + `ox_lib`; read console |
| Panel shows **Citizen** despite SQL | `doj_roles.citizenid` = live framework id (ESX = `users.identifier`); relog |
| NKZ shows 0 laws | Run `02_seed_laws_english.sql` |
| Laws still English on HR/DE/FR/ES | Run `03_seed_laws_i18n.sql`; set `Config.Locale`; restart |
| `No such export viewDocument…` | Item `export` must match **folder name** casing |
| Use deletes item / nothing opens | `consume = 0` + start **`nevera_printeri`** |
| Save / Print error | Add `document_a4` + PNG; check `[sv_printer]` console log |
| Archive won't open | Role + `Config.Archive.Passwords` |
| Discord screenshots fail | `nevera_court_imgbb_key` + `nevera_court_wh_*` convars |
