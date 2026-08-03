# Nevera Court — Changelog

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
