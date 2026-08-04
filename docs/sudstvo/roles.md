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

A player's DOJ role comes from the **`doj_roles` database table first** — not from their ESX group or QBCore job/grade. If the panel shows "Citizen" for someone who should have a role, check that `doj_roles.citizenid` matches their live framework identifier exactly, then have them relog.

**Only if there is no `doj_roles` row** does the system fall back to the player's **job name** (not grade):

| Job name | Maps to |
|---|---|
| `judge` | Judge |
| `district_attorney`, `prosecutor` | Prosecutor |
| `lawyer`, `defense_attorney` | Defense Attorney |
| `public_defender` | Public Defender |
| `police`, `sheriff`, `bcso`, `sasp`, `lspd`, `correctional`, `doc`, `judicial_police` | Police |
| Group `supreme_court`, `admin`, `superadmin` | Supreme Court |

**Grade is not used for this fallback**, with two narrow exceptions:
- A police officer with `job.grade.level >= 4` is also treated as Prosecutor for permission checks (fixed, not configurable).
- One specific form-filing check accepts a police officer as `police` role if `job.grade.level >= Config.Permissions.policeMinGrade` (default `2`, set in `config.lua`).

**Important:** if your server uses **one combined job** for the whole court staff (e.g. a single `doj` job with grades like `Associate → Prosecutor → Judge → Chief Justice`), the job-name fallback **cannot** tell those grades apart — every grade of that job maps to the same thing (or nothing, if the job name isn't in the table above). In that setup you **must** assign roles through `doj_roles` for every DOJ member; don't rely on the job/grade alone.

### Example: separate jobs (qb-core `shared/jobs.lua`)

If you'd rather use the job-name fallback instead of manually managing `doj_roles`, give each DOJ role its **own job**, one grade is enough:

```lua
['judge'] = {
    label = 'Judge',
    defaultDuty = true,
    grades = {
        ['0'] = { name = 'Judge', payment = 150 },
    },
},
['district_attorney'] = {
    label = 'District Attorney',
    defaultDuty = true,
    grades = {
        ['0'] = { name = 'Prosecutor', payment = 120 },
    },
},
['lawyer'] = {
    label = 'Defense Attorney',
    defaultDuty = true,
    grades = {
        ['0'] = { name = 'Attorney', payment = 100 },
    },
},
['public_defender'] = {
    label = 'Public Defender',
    defaultDuty = true,
    grades = {
        ['0'] = { name = 'Public Defender', payment = 90 },
    },
},
```

Qbox (`qbx_core`) doesn't ship `shared/jobs.lua` — add the same jobs through your jobs database/admin tool instead, keeping the same job names.

### Example: ESX (SQL `jobs` / `job_grades`)

```sql
INSERT INTO `jobs` (`name`, `label`) VALUES
('judge', 'Judge'),
('district_attorney', 'District Attorney'),
('lawyer', 'Defense Attorney'),
('public_defender', 'Public Defender');

INSERT INTO `job_grades` (`job_name`, `grade`, `name`, `label`, `salary`) VALUES
('judge', 0, 'judge', 'Judge', 0),
('district_attorney', 0, 'da', 'District Attorney', 0),
('lawyer', 0, 'attorney', 'Attorney', 0),
('public_defender', 0, 'pubdef', 'Public Defender', 0);
```

Police already have their own job from your existing police script (`police`, `sheriff`, `bcso`, `sasp`, `lspd`, …) — no extra setup needed there, it's already in the recognized list above.

## Archive access

Having a DOJ role is not enough on its own to open an archive stash — the player also needs the correct password for that role in `Config.Archive.Passwords`. See [Configuration](configuration.md#archive-how-stashes-actually-work).
