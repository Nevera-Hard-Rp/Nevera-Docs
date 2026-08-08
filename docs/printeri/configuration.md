# Printers — Configuration

Primary editable file: `Install/companion/nevera_printeri/config.lua` (escrow-open, safe to edit).

## Locale

```lua
Config.Locale = 'en'   -- 'en' or 'hr'
```

`nevera_printeri` has its own, smaller locale set (`locales/en.lua`, `hr.lua`, `de.lua`, `es.lua`) — independent of Nevera Court's `Config.Locale`.

## Printer types

```lua
Config.Printers = {
    small  = { item = 'printer_small',  model = 'prop_printer_01',      maxPaper = 50,  maxToner = 100, speed = 3.0, stashSlots = 5,  stashWeight = 10000 },
    medium = { item = 'printer_medium', model = 'v_res_printer',        maxPaper = 200, maxToner = 100, speed = 1.5, stashSlots = 10, stashWeight = 25000 },
    large  = { item = 'printer_large',  model = 'v_med_cor_photocopy',  maxPaper = 500, maxToner = 100, speed = 0.8, stashSlots = 20, stashWeight = 60000 },
}
```

`speed` is seconds per page — lower is faster. `stashSlots`/`stashWeight` size the storage compartment each printer opens for loading paper/toner.

## Toner consumption

```lua
Config.TonerUsage = {
    bw    = { business_card = 0.3, medium = 0.7, a4 = 1.2 },
    color = { business_card = 0.8, medium = 1.5, a4 = 3.0 },
}
```

Percent of toner consumed per page, by document format and B/W vs. Color. Color always costs more toner than B/W for the same format.

## Low-stock warnings

```lua
Config.TonerWarningPct  = 20   -- notify when toner drops below this %
Config.PaperWarningAmt  = 10   -- notify when paper drops below this count
```

## Lock system

```lua
Config.EnableLock  = true
Config.LockCodeLen = 4
```

When enabled, a printer can be locked with a numeric code set by whoever locks it — the code is verified server-side (not trusted from the client), so it can't be bypassed by editing client state.

## Allowed image domains

```lua
Config.AllowedDomains = {
    'i.ibb.co', 'fivemanage.com', 'imgur.com', 'i.imgur.com',
    'cdn.discordapp.com', 'media.discordapp.net',
    'images-ext-1.discordapp.net', 'images-ext-2.discordapp.net',
    'discord.com', 'discordapp.com',
}
```

Whitelist for any image URLs the resource renders — add your own image host here if you use one that isn't listed.

## Public printers (fixed world spawns)

```lua
Config.PublicPrinters = {
    { label = 'City Hall Printer', type = 'large', model = 'v_med_cor_photocopy', coords = vec4(0.0, 0.0, 0.0, 0.0), public = true, locked = false },
}
```

Spawned automatically on server start. Fill in real `coords` before going live — the shipped entry is a placeholder. Add more entries for additional fixed locations, or leave the list empty if every printer should be player-placed.

## Placement

```lua
Config.PlacementDist    = 2.5   -- meters in front of player when placing
Config.PlacementRotStep = 5.0   -- degrees per scroll-wheel tick while rotating
```

## Document window sizes (NUI)

```lua
Config.Formats = {
    business_card = { width = 400,  height = 250,  position = 'top-right' },
    medium        = { width = 600,  height = 450,  position = 'center'    },
    a4            = { width = 794,  height = 1123, position = 'center'    },
}
```

## Required items

```lua
Config.Items = {
    printer_small = 'printer_small', printer_medium = 'printer_medium', printer_large = 'printer_large',
    paper = 'paper_a4',
    toner_small_bw = 'toner_small_bw',   toner_small_color = 'toner_small_color',
    toner_medium_bw = 'toner_medium_bw', toner_medium_color = 'toner_medium_color',
    toner_large_bw = 'toner_large_bw',   toner_large_color = 'toner_large_color',
    doc_business = 'document_business_card', doc_medium = 'document_medium', doc_a4 = 'document_a4',
}

Config.TonerForPrinter = {
    small  = { bw = 'toner_small_bw',  color = 'toner_small_color'  },
    medium = { bw = 'toner_medium_bw', color = 'toner_medium_color' },
    large  = { bw = 'toner_large_bw',  color = 'toner_large_color'  },
}
```

Toner is size-**and**-color matched — a printer only accepts the two toner items sized for it. There is no single generic "toner" item.

### Renaming items to match your own inventory

You can rename any of these item strings, but the name has to match byte-for-byte in **every** one of these places, or the mismatched item silently won't be recognized:

- your `ox_inventory` item definition (`install/ox_items.lua` ships the defaults)
- `config.lua` — `Config.Items` and `Config.TonerForPrinter` above
- `shared/enums.lua` — `PrinterItemMap` / `DocItemMap`, read directly by the placement and print logic

Rename all three together, never just one.
