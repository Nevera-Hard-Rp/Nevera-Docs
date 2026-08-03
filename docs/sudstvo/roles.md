# Nevera Court — Roles & Permissions

| Role | Key | Typical access |
|------|-----|----------------|
| Supreme Court | `supreme_court` | Full admin + all panels + role management |
| Judge | `judge` | Cases, warrants, bail, hearings, jury, fines, archive |
| Prosecutor / DA | `prosecutor` | Cases, forms, warrants, hearings |
| Defense attorney | `defense_attorney` | Cases, defense forms, hearings |
| Public defender | `public_defender` | Same as defense |
| Police | `police` | Affidavit, warrant requests, pre-filing |
| Clerk | `clerk` | Forms / hearings support |
| Citizen | `citizen` | Limited forms, jury register, personal archive (default) |

Assignable DB roles on a new install: `supreme_court`, `judge`, `prosecutor`, `defense_attorney`, `public_defender`, `police`.

## Setting the first admin

Edit and run `Install/sql/04_first_supreme_court.sql` with your character's identifier, or assign the role via the **Admin** tab in-game once someone already has Supreme Court.

- **QB / Qbox:** short `citizenid` (e.g. `ABC12345`)
- **ESX:** exact `users.identifier` (e.g. `char1:…`) — must match 1:1, not a nickname

## How a role is determined

A player's DOJ role comes from the `doj_roles` database table — **not** from their ESX group or QBCore job alone. If the panel shows "Citizen" for someone who should have a role, check that `doj_roles.citizenid` matches their live framework identifier exactly, then have them relog.

## Optional ACE / group mappings

`Config.Permissions` can map ACE groups or job names into DOJ context for auxiliary checks (e.g. which job can execute a commitment order) — this is separate from the core `doj_roles` role assignment.

## Archive access

Having a DOJ role is not enough on its own to open an archive stash — the player also needs the correct password for that role in `Config.Archive.Passwords`. See [Configuration](configuration.md#archive-how-stashes-actually-work).
