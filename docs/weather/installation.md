# Weather — Installation & Configuration

## 1. Place the resource

Download and place the folder in your `resources` directory.

## 2. Get an API key

- Register at [OpenWeatherMap](https://openweathermap.org/)
- Open the **API keys** section of your profile
- Generate a key

> ⚠️ A brand new key can take **up to 2 hours** to activate. A `401` right after signing up means the key is fine but not live yet — wait and try again.

## 3. server.cfg

Put all `set` lines **above** `ensure`:

```cfg
# ---- Nevera Realtime Weather ----
set my_sync_key      "YOUR_API_KEY"   # your OpenWeatherMap key
set my_sync_city     "Split"          # city name
set my_sync_country  "HR"             # ISO country code
set my_sync_interval "10"             # minutes between API calls
set my_sync_display  "15000"          # panel duration in ms, 0 = never show
set disable_fog      "true"           # "false" to allow fog
set my_sync_debug    "false"          # "true" prints the raw API response

# admin permission for the weather commands
add_ace group.admin nevera.weather allow

ensure Nevera-realtime-weather
```

## 4. Start the server

A successful sync looks like:

```
[nevera-weather] Split: Clouds, 29.6 C, wind 1.6 m/s from 228 deg
```

## Configuration reference

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

### Choosing a city

Always pair the city with a country code. `Split,HR` is Split in Croatia — without `HR` the API may return a different Split entirely. Same for `San Juan,PR`, `Tallahassee,US`, `Valencia,ES`.

The timezone is derived from the API response for that city, so **you never configure a timezone**. Set the city correctly and the clock is correct.

### Keep your key private

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

Leave the keys in `conditionNames` exactly as they are — those are API values.

To move the panel, find `EndTextCommandDisplayText(0.015, 0.045)` in the same file. First number is horizontal, second is vertical.

## Exports (server)

```lua
exports['Nevera-realtime-weather']:getWeatherCache()     -- full cached table
exports['Nevera-realtime-weather']:isOverrideActive()    -- boolean
exports['Nevera-realtime-weather']:forceUpdate()         -- trigger a fetch now
exports['Nevera-realtime-weather']:getLastUpdate()       -- unix timestamp
```

## Troubleshooting

| Symptom | Cause and fix |
|---|---|
| `status 0` | Outbound HTTPS blocked, firewall, or outdated artifacts. |
| `status 401` | Bad key, or a new key that hasn't activated yet (wait up to 2 hours). |
| `401` on boot, works after `restart` | `set` lines are below `ensure` in `server.cfg` — move them above. |
| `status 404` | Wrong city or country code. |
| `status 429` | Quota exceeded. Increase `my_sync_interval`. |
| Clock off by hours | Wrong city. Set `my_sync_country`, or override with `my_sync_tzoffset`. |
| No fog | `disable_fog` is `"true"`. Set it to `"false"`. |
| Panel never shows | `my_sync_display` is `0`, or the API hasn't responded yet. |
| Weather won't stay | Another weather script is fighting this one. Run only one. |
| Admin command denied | ACE not set, or QBCore admin without ACE — see [Admin commands](admin-commands.md). |

Test your key in a browser:

```
https://api.openweathermap.org/data/2.5/weather?q=Split,HR&appid=YOUR_KEY&units=metric
```

Set `my_sync_debug "true"` to print the full API response in console.
