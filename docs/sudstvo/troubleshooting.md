# Nevera Court — Troubleshooting

| Problem | Fix |
|---------|-----|
| Resource won't start | Check `oxmysql` + `ox_lib`; read console |
| Panel shows **Citizen** despite SQL | `doj_roles.citizenid` = live framework id (ESX = `users.identifier`); relog |
| NKZ shows 0 laws | Run `02_seed_laws_english.sql` |
| Laws still English on HR/DE/FR/ES | Run `03_seed_laws_i18n.sql`; set `Config.Locale`; restart |
| Form half English / half locale | Sync all `web/public/forms_*` → `web/dist/forms_*`; restart |
| `No such export viewDocument…` | Item `export` must match **folder name** casing |
| Use deletes item / nothing opens | `consume = 0` + start **`nevera_printeri`** |
| Save / Print error | Add `document_a4` + PNG; check the `[sv_printer]` console log |
| Archive won't open | Wrong role, or wrong `Config.Archive.Passwords` entry |
| Discord screenshots fail | Missing `nevera_court_imgbb_key` or `nevera_court_wh_*` convars — see [Discord & Webhooks](discord-webhooks.md) |

## When opening a support ticket, include

1. Resource version (`fxmanifest.lua` → `version`)
2. Framework + inventory + phone bridge in use
3. `Config.Locale`
4. Server console excerpt (`[nevera_court]`, `[sv_printer]`, `[DISCORD]`, `[sv_archive]`)
5. Clear steps to reproduce

Modified escrow binaries, leaked copies, or "fix it for me" tickets without logs are not supported.
