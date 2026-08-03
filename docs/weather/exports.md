# Weather — Exports

Server-side exports for other resources that want to read or react to the current weather state.

```lua
exports['Nevera-realtime-weather']:getWeatherCache()     -- full cached table
exports['Nevera-realtime-weather']:isOverrideActive()    -- boolean
exports['Nevera-realtime-weather']:forceUpdate()         -- trigger a fetch now
exports['Nevera-realtime-weather']:getLastUpdate()       -- unix timestamp
```

| Export | Returns | Use case |
|---|---|---|
| `getWeatherCache()` | Full cached weather table (condition, temp, wind, etc.) | Read current conditions from another resource without your own API call |
| `isOverrideActive()` | `true` / `false` | Check if an admin has forced a weather type right now |
| `forceUpdate()` | — | Manually trigger an immediate API refresh instead of waiting for the next interval |
| `getLastUpdate()` | Unix timestamp | Know how stale the cached data is |

### `getWeatherCache()` fields

| Field | Meaning |
|---|---|
| `weatherMain` | OpenWeatherMap condition group (e.g. `Clear`, `Clouds`, `Rain`) |
| `weatherId` | Full OpenWeatherMap condition ID (the detailed one behind the ~40-way mapping) |
| `temp` | Temperature in °C |
| `windSpeed` | Wind speed (m/s) |
| `windDeg` | Wind bearing in degrees |
| `tzOffset` | UTC offset in seconds for the configured city |
| `dt` | Unix timestamp of the API response |

### Example

```lua
local weather = exports['Nevera-realtime-weather']:getWeatherCache()
if weather then
    print(('Current: %s, %.1f°C'):format(weather.weatherMain, weather.temp))
end
```

There are currently no client-side exports and no events fired — read state via the exports above.
