# Weather — Configuration

All configuration is done through `server.cfg` convars — no source file needs editing for basic setup.

## Convar reference

| Convar | Default | Description |
|---|---|---|
| `my_sync_key` | *(empty)* | OpenWeatherMap API key. **Required.** |
| `my_sync_city` | `Split` | City name. Spaces and accents are handled. |
| `my_sync_country` | `HR` | ISO 3166 country code. Prevents matching the wrong city. |
| `my_sync_interval` | `10` | Minutes between API calls. |
| `my_sync_display` | `15000` | How long the panel stays on screen, in ms. `0` hides it entirely. |
| `my_sync_tzoffset` | *(auto)* | Manual UTC offset **in seconds**. Only set this if the automatic value is wrong. |
| `disable_fog` | `true` | Replaces fog with overcast. Useful where fog is rare. |
| `my_sync_debug` | `false` | Prints the full API response to console. |

## Choosing a city

Always pair the city with a country code. `Split,HR` is Split in Croatia — without `HR` the API may return a different Split entirely. Same for `San Juan,PR`, `Tallahassee,US`, `Valencia,ES`.

The timezone is derived from the API response for that city, so **you never configure a timezone**. Set the city correctly and the clock is correct.

## Keep your key private

Don't commit the API key, don't show it on stream, and don't type `my_sync_key` alone in the console (it prints the value). If a key is exposed, delete it in your OpenWeatherMap profile and generate a new one.

## Translating the on-screen panel

Open `realtime_client.lua`. Change only the **right-hand side** of these tables at the top of the file:

```lua
local LABELS = {
    time    = "Time",
    weather = "Weather",
    temp    = "Temp",
    wind    = "Wind",
    forced  = "Forced by admin"
}

local conditionNames = {
    Clear  = "Clear",
    Clouds = "Cloudy",
    Rain   = "Rain",
    -- ...
}
```

Leave the keys in `conditionNames` exactly as they are — those are API values, not display text.

## Moving the panel

Find `EndTextCommandDisplayText(0.015, 0.045)` in `realtime_client.lua`. First number is horizontal position, second is vertical (0.0–1.0 screen-relative).
