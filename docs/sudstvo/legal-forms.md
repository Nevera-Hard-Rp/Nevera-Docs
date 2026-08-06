# Nevera Court — Legal Forms

**37 A4 HTML templates**, fully translated into **5 languages** — affidavits, complaints, warrants, motions, orders, subpoenas, civil filings, and more.

## How they work

- Fillable US-style court forms, filled out directly in the DOJ panel
- Role-based access — each role only sees the form types it's allowed to file (`Enums.FormsByRole`)
- A legal-misuse warning is shown before printing
- Printing gives a `document_a4` inventory item (+ an optional Discord court transcript — see [Discord & Webhooks](discord-webhooks.md))
- Judge approve / deny / sign workflow for forms that need it

## Citizen requests (Name Change / Certificate of No Criminal Record)

Two form types are **citizen-filed requests**, not direct court filings — a citizen submits a request, and staff (Judge, Supreme Court, or **Clerk**) review it in the **Requests** tab before anything official is issued:

| Form | What the citizen submits | What staff does |
|------|---------------------------|------------------|
| `name_change_request` | Requested new legal name + reason | Approve / deny |
| `request_certificate_no_criminal` | Purpose (employment, licence, court, …) | Approve / deny, then **Print certificate** — jumps to Forms with the official `certificate_no_criminal_record` pre-filled from the request |

A court filing fee is charged from the citizen's bank account on submission — see [Configuration → Court filing fees](configuration.md#court-filing-fees).

The **Certificate of No Criminal Record** itself also has an optional 2D court seal (toggle on the form) — applying it is gated by `Config.Seal.Roles` (typically Judge / Clerk / Supreme Court).

## File locations

| `Config.Locale` | Folder (edit `public`, ship `dist`) |
|-----------------|-------------------------------------|
| `en` | `web/dist/forms_en/` ← `web/public/forms_en/` |
| `hr` | `web/dist/forms_hr/` ← `web/public/forms_hr/` |
| `de` | `web/dist/forms_de/` ← `web/public/forms_de/` |
| `fr` | `web/dist/forms_fr/` ← `web/public/forms_fr/` |
| `es` | `web/dist/forms_es/` ← `web/public/forms_es/` |

A missing file in a locale folder **falls back to `forms_en`**. Optional JSON chrome for `data-i18n` strings lives at `web/dist/i18n/forms_*.json`.

> Do **not** use the old `web/public/forms/` folder — it's legacy and unused.

## Editing a form

Forms live under `web/public/forms_<locale>/` as full standalone HTML. After editing, sync/rebuild into `web/dist/forms_<locale>/` (FiveM's NUI reads **dist** only — see [Development](configuration.md)).

Keep the `name=` / `id=` attributes on form inputs **identical across every language version** of the same form — the panel relies on matching field names for autofill and data handling.
