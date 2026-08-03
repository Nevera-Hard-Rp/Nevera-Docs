# Weather — Troubleshooting

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
| Weather won't stay | Another weather script is fighting this one. Run only one — see [Dependencies](dependencies.md). |
| Admin command denied | ACE not set, or QBCore admin without ACE — see [Admin Commands](admin-commands.md). |

## Testing your API key directly

Open this in a browser, replacing the placeholders:

```
https://api.openweathermap.org/data/2.5/weather?q=Split,HR&appid=YOUR_KEY&units=metric
```

A JSON response back means the key is valid and live. An error there means the problem is the key/city, not the script.

## Verbose logging

Set `my_sync_debug "true"` in `server.cfg` to print the full raw API response to console on every sync — useful for comparing what the API actually returned against what you expected.
