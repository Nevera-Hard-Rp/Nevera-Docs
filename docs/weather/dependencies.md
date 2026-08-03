# Weather — Dependencies

## Server requirements

| Requirement | Needed | Notes |
|---|---|---|
| FiveM server artifacts | Yes | Must support `fx_version 'cerulean'` |
| OpenWeatherMap API key | Yes | Free tier is enough — see [Installation](installation.md) |
| Outbound HTTPS access | Yes | The server must be able to reach `api.openweathermap.org` |

## FiveM resource dependencies

**None — fully standalone.** No framework, no other resource required.

| Framework | Supported |
|---|---|
| ESX | ✅ |
| QBCore | ✅ |
| QBox | ✅ |
| Standalone | ✅ |

The script only touches weather/time natives and the on-screen panel — it never reads player/job/inventory data from any framework, so there is nothing to bridge.

## Compatibility warning

Do **not** run this alongside another script that also sets weather/time (e.g. a framework's built-in weather sync, `vSync`, `cd_easytime`, etc.) — they will fight each other and the weather will flicker or revert. Run exactly one weather-controlling resource.
