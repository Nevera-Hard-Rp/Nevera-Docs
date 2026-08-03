# Nevera Court — Localization

| Code | Language | UI (`locales/`) | Full A4 HTML | Form chrome JSON | NKZ titles |
|------|----------|-----------------|--------------|------------------|------------|
| `en` | English (default) | `en.lua` | `forms_en/` | `forms_en.json` | `title` (base) |
| `hr` | Croatian | `hr.lua` | `forms_hr/` | `forms_hr.json` | `title_hr` (SQL `03`) |
| `de` | German | `de.lua` | `forms_de/` | `forms_de.json` | `title_de` (SQL `03`) |
| `fr` | French | `fr.lua` | `forms_fr/` | `forms_fr.json` | `title_fr` (SQL `03`) |
| `es` | Spanish | `es.lua` | `forms_es/` | `forms_es.json` | `title_es` (SQL `03`) |

## What `Config.Locale` controls

One switch drives **panel + ox_lib UI + full form HTML folder + NKZ display titles**. The public API / export names always stay English.

| Area | Localized |
|------|-----------|
| ox_lib notifies, alerts, menus, targets | Yes |
| React panel strings | Yes |
| Print legal warning | Yes |
| Full HTML court forms (`forms_<locale>/`) | Yes — 37 templates each |
| HTML `data-i18n` chrome (`forms_*.json`) | Yes |
| NKZ titles in the database (`title_*`) | Yes — seeded by SQL `03` (HR/DE/FR/ES) |
| Export / event names | **No** — always English |

## Important: dist vs public

FiveM's NUI loads **`web/dist/`** only. After editing anything under `web/public/forms_*`, you must sync/rebuild **all** language folders into `web/dist/forms_*/` and restart. A locale folder missing from `dist` (e.g. `forms_hr`) silently falls back to `forms_en`, which can look like a mixed EN/locale form.

## Adding a new language

1. Copy `locales/en.lua` → `locales/xx.lua`
2. Register the new locale in `fxmanifest.lua`
3. Add a `forms_xx/` folder (all 37 HTML files) + `forms_xx.json` chrome
4. Extend `FORM_LOCALES` / `forms_i18n.js` / `sv_printer.lua` to include `xx`
5. Add `title_xx` columns to the law tables + seed them
6. Set `Config.Locale = 'xx'`
