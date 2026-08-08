# Printers — Troubleshooting

| Symptom | Cause | Fix |
|---------|-------|-----|
| Notify: *nevera_printeri must be started to view documents.* (only appears if you also own **Nevera Court** — the message comes from Court's document handler, not from `nevera_printeri` itself) | `nevera_printeri` isn't running | `ensure nevera_printeri`, then restart. Order in `server.cfg` doesn't matter — the check runs when a document is opened, not at boot. |
| Use on a filled document does nothing, no error at all | Item names in your `ox_inventory` don't match what `config.lua` / `shared/enums.lua` expect | Rename must be consistent in all three places — see [Configuration → Renaming items](configuration.md#renaming-items-to-match-your-own-inventory). A one-place rename fails silently, it doesn't error. |
| Printer doesn't consume the toner you loaded | Loaded the wrong size/color toner for that printer | Each printer only accepts its matching size (`small`/`medium`/`large`) **and** color (`bw`/`color`) toner — see `Config.TonerForPrinter`. There's no universal toner item. |
| Printer refuses to open even with the right code | `Config.EnableLock = false` but you're still trying to enter a code | Locking is optional per-printer — check `Config.EnableLock` and whether that specific printer was actually locked. |
| No public printer spawns anywhere | `Config.PublicPrinters` is empty by default | Add an entry with real `coords` in `config.lua`, or place printers manually with the in-game placement tool. |
| Image (custom logo/seal) doesn't render on a document | Image host isn't in the allowlist | Add the domain to `Config.AllowedDomains`. |
