# Printers — Changelog

## [1.0.0] — First release

**Fixed before release**
- **SQL schema was missing 3 columns the code actively reads/writes on every print** — `nevera_printeri.total_prints` (written by the print handler, read by the status display) and `nevera_dokumenti.char_name` / `nevera_dokumenti.print_mode` (written by the audit-log insert, read by the history display). Every print threw a SQL "unknown column" error, silently breaking print counts, printer status, and print history on a fresh install. Fixed in `sql/nevera_printeri.sql`; existing installs need an `ALTER TABLE` to add the 3 columns without losing data (`CREATE TABLE IF NOT EXISTS` doesn't retroactively add columns).
- `Config.TonerUsage` was defined twice in `config.lua` (a dead stub, silently shadowed by the real bw/color-aware table) — removed the dead definition
- Added `qbx_core` fallback to `GetPlayerCitizenId`/`GetPlayerJob` — these only checked `qb-core` and `es_extended`, so ownership tracking and job-restricted printers silently failed on a clean Qbox server (no `qb-core` compat export)
- `no_toner_inv` (all 4 languages) and `no_paper_inv` (German, Spanish) wrongly said the printer's own stash was empty — paper and toner are actually pulled from the player's inventory, not a printer-side stash
- German and Spanish locales were missing 10 keys present in English/Croatian (`target_history`, `pickup_confirm_title/text`, `status_title/content/locked/unlocked/private`, `history_title/empty`) — players on those languages saw raw locale keys instead of text
- Removed ~40 lines of dead HTML (`#doc-overlay` and its child elements) from `html/index.html` — unused since the document viewer is built dynamically in `app.js`, no matching CSS ever existed for it
- `Config.PublicPrinters` no longer ships with a placeholder `vec4(0,0,0,0)` entry that would spawn a printer at the map's center — empty by default, with a commented example to uncomment

- Placeable small/medium/large printers with configurable paper/toner capacity and print speed
- Size-and-color-matched toner system (6 SKUs) with configurable per-format consumption
- Optional lock-code system — codes are verified server-side, never trusted from the client
- Low-stock warnings for paper and toner
- Fixed public printer spawns + player-placement tool
- Self-contained framework detection (QBCore / ESX / Qbox) — no separate bridge needed
- 4 languages: `en` · `hr` · `de` · `es`
