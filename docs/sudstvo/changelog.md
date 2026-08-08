# Nevera Court — Changelog

## [1.1.0] — Citizen requests & court filing fees

**Added**
- New **Requests** panel tab (Judge / Supreme Court / Clerk) — review and approve/deny citizen-filed requests separately from staff Forms
- New citizen-filed request form: **Request for Certificate of No Criminal Record**, alongside the existing Name Change Request
- **Clerk** role can now approve/deny citizen requests (previously Judge/Supreme Court only)
- `Config.Fees` — configurable court filing fee charged from the citizen's bank account on request submission (staff prints of an already-issued certificate stay free)
- "Print certificate" shortcut: approving a certificate request jumps to Forms with the official document pre-filled from the request
- Redesigned **Certificate of No Criminal Record** template (all 5 languages) with an optional 2D court seal toggle

**Fixed**
- Requests panel (Judge / Supreme Court / Clerk) no longer falls back to Croatian field labels and status text on non-Croatian installs — field labels, Yes/No values, and the decision-reason/fee text are now fully localized in all 5 languages
- `doj_forms` was missing 4 columns (`arhiviran`, `arhivirao_citizenid`, `arhivirao_ime`, `datum_arhiviranja`) that `server/sv_archive.lua` writes on every archive/unarchive of a document — every move of `document_a4` into or out of the archive stash threw a SQL error, so the archive audit trail never actually recorded anything. Existing installs need an `ALTER TABLE` — see [Troubleshooting](troubleshooting.md).

**Changed**
- Printed-document storage moved to a slim `doc_id` reference resolved against the database, instead of baking the full HTML into inventory item metadata (fixes large documents failing to sync via `ox_inventory`)
- Inventory bridge docs split into **Tested** (ox_inventory, qb-inventory/qbox, ps-inventory) vs **Compatibility layer** (qs, tgiann, codem, origen, ak47) support tiers
- `config_fines.lua` no longer ships an unused legacy Croatian fine-key alias table — `Config.Fines` (English keys) is unchanged and is the only thing a fresh install ever uses
- `Install/sql/` trimmed to the 4 files a first install actually needs (`01`→`04`) — leftover migration scripts for upgrading a pre-existing older schema were removed, matching this being a first-install-only release
- **`nevera_printeri` is now a standalone product, sold separately** — no longer bundled in `Install/companion/`. It still integrates automatically if installed alongside Court (no manual linking needed), but is no longer required or included. See [Printers](/docs/printeri/overview.md).

## [1.0.0] — First release

Initial Tebex release. First-install only — no upgrade/migration scripts are shipped in this version.

- Full DOJ system: cases, forms, warrants, bail, hearings, jury, fines, penal code (NKZ), archive, admin/audit
- Multi-framework bridge: ESX, QBCore, Qbox, OX_Core, Standalone (`Config.Framework = 'auto'`)
- Multi-inventory bridge: ox, qs, qb, ps, codem, tgiann, origen, ak47
- Multi-phone bridge: LB, Quasar, YSeries, 17mov, GKS, NPWD, qb-phone
- MDT bridge: tk_mdt (full), Advanced (manual), ps-mdt (patch), ox_mdt (events)
- 5 languages: `en` · `hr` · `de` · `fr` · `es` — full UI + 37 A4 forms per language + NKZ titles
- Companion printer system (`nevera_printeri`, self-contained) for filled-form viewing
- Discord integration: system event webhooks + printed-form transcript screenshots
