# Nevera Court — Discord & Webhooks

There are **two separate** Discord layers — don't confuse them.

| Layer | Purpose |
|-------|---------|
| **1. System logs** | Case / warrant / bail / fine / verdict / admin / audit **text** events (`Config.Webhooks`) |
| **2. Court transcripts** | Every **printed** A4 form is screenshotted → uploaded → posted to Discord as a lasting visual record |

## Court transcripts (printed forms → Discord)

When a player **Save/Print**s a court form (and accepts the legal warning), Nevera Court can:

1. Capture the filled A4 page as an image
2. Upload it via **imgbb**
3. Post an embed into the matching Discord channel

That channel becomes your **transcript archive** — staff can scroll history and prove what was filed/printed (complaint, warrant, bail bond, verdict, etc.), even if the in-game item is later lost.

**Organize like a real docket room:**

- Create **one webhook per channel** (recommended) — e.g. `#court-criminal`, `#court-verdicts`, `#court-bail`
- Or use one shared `#court-transcripts` channel for a single feed
- Keep channels staff-only if you want controlled access

Without `nevera_court_imgbb_key` **and** the matching `nevera_court_wh_*` URL, printing still gives the player their `document_a4` item — it just skips the Discord transcript.

> New to Discord webhooks? Official guide: [Intro to Webhooks (Discord Support)](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks)

## Creating a webhook

1. Discord server → **Server Settings** → **Integrations** → **Webhooks** → **New Webhook**
2. Name it (e.g. `Nevera Court — Criminal transcripts`), pick the target text channel
3. **Copy Webhook URL** — `https://discord.com/api/webhooks/ID/TOKEN`
4. Paste into the matching `set nevera_court_wh_…` line in `server.cfg` (or into `Config.Webhooks` for system logs)
5. Repeat per channel so transcripts stay organized

**Tips:** you need the **Manage Webhooks** permission; treat the URL like a password; restart the server (or `ensure Nevera_Court`) after editing `server.cfg`.

## Imgbb API key (required for transcripts)

1. Free account at [imgbb.com](https://imgbb.com/) → API → copy the key
2. `set nevera_court_imgbb_key "YOUR_KEY"` in `server.cfg`

## 1) System event webhooks — `config.lua`

Used for case / warrant / bail / fine / verdict / admin / audit **text** logs (`Config.Webhooks`). These are activity logs, not full form images.

## 2) Form transcript channels — `server.cfg` convars

Printed forms → imgbb → Discord embed (visual transcript). Reference file: `Install/server_cfg_discord.cfg`.

```cfg
set nevera_court_imgbb_key "YOUR_IMGBB_API_KEY"

set nevera_court_wh_criminal "https://discord.com/api/webhooks/..."
set nevera_court_wh_verdict  "https://discord.com/api/webhooks/..."
set nevera_court_wh_fines    "https://discord.com/api/webhooks/..."
set nevera_court_wh_bail     "https://discord.com/api/webhooks/..."
set nevera_court_wh_citizen  "https://discord.com/api/webhooks/..."
set nevera_court_wh_admin    "https://discord.com/api/webhooks/..."
set nevera_court_wh_audit    "https://discord.com/api/webhooks/..."
```

| Convar | Transcript channel for |
|--------|-------------------------|
| `nevera_court_imgbb_key` | Imgbb upload (required) |
| `nevera_court_wh_criminal` | Criminal filings / complaints / warrants |
| `nevera_court_wh_verdict` | Verdicts / judgments |
| `nevera_court_wh_fines` | Fine-related prints |
| `nevera_court_wh_bail` | Bail / bond prints |
| `nevera_court_wh_citizen` | Citizen / civil prints |
| `nevera_court_wh_admin` | Admin / Supreme Court prints |
| `nevera_court_wh_audit` | General / catch-all document shots |
