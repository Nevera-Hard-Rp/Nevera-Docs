# Weather — Installation

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

If you don't see that line, go to [Troubleshooting](troubleshooting.md).

Next: [Configuration](configuration.md) to fine-tune convars, choose your city correctly, and translate the on-screen panel.
