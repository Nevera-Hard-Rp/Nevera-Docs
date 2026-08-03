# Nevera Court — Configuration

Primary editable file: `config.lua` (escrow-open, safe to edit). Fine table: `config_fines.lua`.

## Essentials

```lua
Config.Debug     = false
Config.Locale    = 'en'       -- 'en' | 'hr' | 'de' | 'fr' | 'es'
Config.Currency  = '$'        -- UI symbol only: '$' or '€' (or any string)
Config.Framework = 'auto'     -- 'esx' | 'qb' | 'qbox' | 'standalone'
Config.MDT = {
    provider = 'auto',        -- tk_mdt → ps-mdt → ox_mdt (advanced = manual + resourceName)
    trustedInvokers = { 'ps-mdt', 'tk_mdt' },  -- also gates IssueFine / CreateCommitmentOrder / etc. — see Exports
}
Config.ESX = { RequireDuty = false, AdminGroups = { 'admin', 'superadmin' } }
Config.Inventory = { provider = 'auto' }
Config.Phone     = { provider = 'auto' }
```

## Currency (`$` / `€`)

Set the symbol yourself — it is **display only** (panel, notifies, forms chrome):

```lua
Config.Currency = '$'   -- US / dollar servers
Config.Currency = '€'   -- EU / euro servers
```

Changing the symbol does **not** convert amounts. Edit the numbers in `config_fines.lua` / `Config.Economy` to match your server economy.

## Fines & bail amounts (fully editable)

All preset fine / bail values live in `config_fines.lua`. Change any `fine`, `bail`, `hut`, or `label` — no code edits needed.

```lua
Config.Fines['minor_traffic'] = {
    label = 'Minor Traffic Violation',
    fine  = 500,    -- ← change this
    bail  = 750,    -- ← change this (often ~150% of fine)
    hut   = false,
    category = 'traffic',
}
```

Civil damages range and related economy knobs:

```lua
Config.Economy = {
    civilDamagesMin = 1000,
    civilDamagesMax = 500000,
    -- … see config.lua
}
```

Ship defaults are calibrated to a reference economy — **adjust for your city** before go-live.

## Map locations (courthouse, desks, archives) — you must set these

Nevera Court does **not** know your MLO. Every server places targets/zones on its own map.

| Config | What it is | Who uses it |
|--------|------------|-------------|
| `Config.Courthouse.mainZone` | Main DOJ / court interaction | Open panel at the courthouse |
| `Config.Courthouse.terminalZone` | Clerk / filing terminal | Forms / filings desk |
| `Config.Courthouse.bailZone` | Bail desk | Pay / process bail |
| `Config.Archive.Locations` | Archive rooms / cabinets | Password stashes for documents |
| `Config.Prison.intakeZone` (if used) | Prison intake | Commitment / custody handoff |

Ship coords are placeholders. Before go-live:

1. Stand in-game where the desk / courtroom / archive should be
2. Copy your `vector3(x, y, z)` (and heading if needed)
3. Paste into the matching entry in `config.lua`
4. Restart / `ensure` the resource and test the `ox_target` prompts

```lua
Config.Courthouse = {
    mainZone = {
        coords = vector3(0.0, 0.0, 0.0),  -- ← your courtroom / lobby
    },
    terminalZone = { coords = vector3(0.0, 0.0, 0.0) }, -- filing desk
    bailZone     = { coords = vector3(0.0, 0.0, 0.0) }, -- bail window
}

Config.Archive.Locations = {
    { label = 'City Hall archive 1', coords = vector3(0.0, 0.0, 0.0), heading = 0.0 },
    { label = 'City Hall archive 2', coords = vector3(0.0, 0.0, 0.0), heading = 0.0 },
    { label = 'Police archive',      coords = vector3(0.0, 0.0, 0.0), heading = 0.0 },
    { label = 'Hospital archive',    coords = vector3(0.0, 0.0, 0.0), heading = 0.0 },
    -- add / remove rows for every physical cabinet on your map
}
```

There is no separate "lawyer office" resource forced by Nevera Court — attorneys use the same DOJ panel + roles.

## Archive — how stashes actually work

Archive is **not** one shared locker for everyone. It is:

1. **Physical points** placed on the map (`Config.Archive.Locations`) — e.g. 2 at City Hall, 1 at police, 1 at hospital
2. **Logical stashes** opened by **DOJ role + password**, independent of which physical point was used

| Setting | Meaning |
|---------|---------|
| `Locations` | `ox_target` spots only. One `{ label, coords, heading }` per cabinet/room. Coords `0,0,0` are skipped. |
| `Passwords` | One password per role. Wrong password → stash does not open. |
| `UseRoleStashes = true` | Staff → shared role stash `doj_archive_<role>` (all judges share one, all police share one, …). Citizen → personal `doj_archive_<citizenid>`. |
| `UseRoleStashes = false` | Staff share one `StashId` (`doj_archive_main`); citizens still get a personal stash. |
| `AllowedItems = { 'document_a4' }` | Only printed court forms can go in — blocks dumping weapons/junk into the archive. |
| `StashSize` | Slots + weight for role/main stashes. |

```lua
Config.Archive = {
    Passwords = {
        citizen          = 'citizen123',   -- CHANGE before publish
        police           = 'police123',
        defense_attorney = 'defense123',
        public_defender  = 'defender123',
        prosecutor       = 'prosecutor123',
        clerk            = 'clerk123',
        judge            = 'judge123',
        supreme_court    = 'supreme123',
    },
    UseRoleStashes = true,
    AllowedItems   = { 'document_a4' },
    StashSize      = { slots = 50, weight = 100000 },
    StashId        = 'doj_archive_main',
    Locations = {
        { label = 'City Hall 1', coords = vector3(0,0,0), heading = 0.0 },
        { label = 'City Hall 2', coords = vector3(0,0,0), heading = 0.0 },
        { label = 'Police',      coords = vector3(0,0,0), heading = 0.0 },
        { label = 'Hospital',    coords = vector3(0,0,0), heading = 0.0 },
    },
}
```

**Checklist:**
1. Change all default passwords before going live
2. Stand at each cabinet in-game → copy `vector3` → paste into `Locations`
3. Restart / `ensure Nevera_Court` → test the target prompt
4. Each player uses their own role code; they can use any archive point on the map
5. Leave `AllowedItems = { 'document_a4' }` unless you deliberately want other items stored there

## Prison / commitment

```lua
Config.Prison = {
    provider = 'auto',
    commitmentOrder = true,   -- hard RP (recommended)
    executeJobs = { 'police', 'doc', 'correctional' },
    requireNearby = true,
}
```

Bridges: `qb-prison` · `rcore_prison` · `pickle_prisons` · `custom` · `none`. When `commitmentOrder = true`, a guilty verdict does **not** auto-jail — custody/DOC must execute the order near the inmate.

## UI

```lua
Config.UI = {
    openKey = 'F5',
    closeKeys = { 'Escape', 'F5' },
}
```

## System Discord webhooks

```lua
Config.Webhooks = {
    cases = '', warrants = '', bail = '', fines = '',
    verdicts = '', admin = '', audit = '',
}
```

These are text activity logs. Form **screenshot transcripts** use separate `server.cfg` convars — see [Discord & Webhooks](discord-webhooks.md).
