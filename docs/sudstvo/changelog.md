# Nevera Court — Changelog

## [1.1.0] — Citizen requests & court filing fees

**Added**
- New **Requests** panel tab (Judge / Supreme Court / Clerk) — review and approve/deny citizen-filed requests separately from staff Forms
- New citizen-filed request form: **Request for Certificate of No Criminal Record**, alongside the existing Name Change Request
- **Clerk** role can now approve/deny citizen requests (previously Judge/Supreme Court only)
- `Config.Fees` — configurable court filing fee charged from the citizen's bank account on request submission (staff prints of an already-issued certificate stay free)
- "Print certificate" shortcut: approving a certificate request jumps to Forms with the official document pre-filled from the request
- Redesigned **Certificate of No Criminal Record** template (all 5 languages) with an optional 2D court seal toggle

**Changed**
- Printed-document storage moved to a slim `doc_id` reference resolved against the database, instead of baking the full HTML into inventory item metadata (fixes large documents failing to sync via `ox_inventory`)
- Inventory bridge docs split into **Tested** (ox_inventory, qb-inventory/qbox, ps-inventory) vs **Compatibility layer** (qs, tgiann, codem, origen, ak47) support tiers

## [1.0.0] — First release

Initial Tebex release. First-install only — no upgrade/migration scripts are shipped in this version.

- Full DOJ system: cases, forms, warrants, bail, hearings, jury, fines, penal code (NKZ), archive, admin/audit
- Multi-framework bridge: ESX, QBCore, Qbox, Standalone (`Config.Framework = 'auto'`)
- Multi-inventory bridge: ox, qs, qb, ps, codem, tgiann, origen, ak47
- Multi-phone bridge: LB, Quasar, YSeries, 17mov, GKS, NPWD, qb-phone
- MDT bridge: tk_mdt (full), Advanced (manual), ps-mdt (patch), ox_mdt (events)
- 5 languages: `en` · `hr` · `de` · `fr` · `es` — full UI + 37 A4 forms per language + NKZ titles
- Companion printer system (`nevera_printeri`, self-contained) for filled-form viewing
- Discord integration: system event webhooks + printed-form transcript screenshots
