# Weather — Admin Commands

All three commands require the `nevera.weather` ACE permission. They also work from the server console.

| Command | Description |
|---|---|
| `/setweather <TYPE> [minutes]` | Force a weather type. Default 30 minutes, max 720. |
| `/resetweather` | Cancel the override immediately and resync. |
| `/weatherstatus` | Show real conditions and override state. |

**Available types:**
`CLEAR` `EXTRASUNNY` `CLOUDS` `OVERCAST` `CLEARING` `RAIN` `THUNDER` `FOGGY` `SMOG` `SNOW` `SNOWLIGHT` `BLIZZARD` `XMAS` `NEUTRAL` `HALLOWEEN`

**Examples:**

```
/setweather BLIZZARD 45
/setweather FOGGY
/resetweather
```

While an override is active, real-time sync pauses and the panel shows which admin set it. When the timer expires, the script returns to real weather on its own.

> There is no command to change the clock. Time always follows the real world.

## Granting permission

```cfg
add_principal identifier.license:YOUR_LICENSE group.admin
add_ace group.admin nevera.weather allow
```

> **QBCore:** being a QBCore admin does **not** grant ACE. You still need `add_principal` / `add_ace` as above.
