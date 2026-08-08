# Printers — Troubleshooting

| Symptom | Cause | Fix |
|---------|-------|-----|
| Notify: *nevera_printeri must be started to view documents.* | `nevera_printeri` isn't running | `ensure nevera_printeri`, then restart. Must start **before** `Nevera_Court` in `server.cfg`. |
| Use on a filled document does nothing, no error at all | Item names in your `ox_inventory` don't match what `config.lua` / `shared/enums.lua` expect | Rename must be consistent in all three places — see [Configuration → Renaming items](configuration.md#renaming-items-to-match-your-own-inventory). A one-place rename fails silently, it doesn't error. |
| Printer doesn't consume the toner you loaded | Loaded the wrong size/color toner for that printer | Each printer only accepts its matching size (`small`/`medium`/`large`) **and** color (`bw`/`color`) toner — see `Config.TonerForPrinter`. There's no universal toner item. |
| Printer refuses to open even with the right code | `Config.EnableLock = false` but you're still trying to enter a code | Locking is optional per-printer — check `Config.EnableLock` and whether that specific printer was actually locked. |
| Placed printer isn't in the location you expect on restart | `Config.PublicPrinters` still has the shipped placeholder coords | The default entry ships with `coords = vec4(0.0, 0.0, 0.0, 0.0)` — fill in real coordinates in `config.lua`. |
| Image (custom logo/seal) doesn't render on a document | Image host isn't in the allowlist | Add the domain to `Config.AllowedDomains`. |
