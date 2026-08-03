# Nevera Court — Staff & Player Guide

**Purpose:** explain **how to use** the in-game panel (not how to install the resource — see [Installation](installation.md)).

UI language follows `Config.Locale` (`en` / `hr` / `de` / `fr` / `es`). Sidebar labels below use English (same order as the panel).

## 1. Big picture — who does what

```text
CITIZEN / DEFENDANT
  • Limited forms, pay bail (where allowed), jury pool register, personal archive

POLICE
  • Affidavit, pre-filing, warrant REQUESTS → then wait for judge

PROSECUTOR (DA)
  • Open / drive cases, complaints, warrants, hearings, motions

DEFENSE / PUBLIC DEFENDER
  • Appear on case, defense forms, motions, hearings

CLERK
  • Filing / hearing support (role-dependent)

JUDGE
  • Approve warrants, bail, schedule hearings, pick jury, fines, verdicts

SUPREME COURT
  • Everything judge has + Admin (roles) + audit

SYSTEM (automatic)
  • Notifies online jurors when selected
  • Prints → document_a4 + optional Discord screenshots
  • Archive stash filters (document_a4 only by default)
```

**There is no automatic phone "summons script" for every event.**
Staff schedule **Hearings**; jurors get an **in-game notify** when selected; Discord tags / RP cover the rest.

## 2. Typical criminal timeline (order of work)

Use this as the default RP + system order. Skip steps your city does not use.

```text
1. POLICE     Affidavit / arrest facts          → Forms
2. POLICE/DA  Criminal Pre-Filing / Complaint   → Forms
3. DA/JUDGE   Case opened (docket number)       → Cases
4. POLICE/DA  Warrant request (optional)        → Warrants / Forms
5. JUDGE      Approve / deny warrant            → Warrants
6. POLICE     Execute warrant (RP + MDT if used)
7. JUDGE      Bail / bond                       → Bail / Bond  (+ optional Hearing)
8. ANY STAFF  Schedule courtroom time           → Hearings
9. CITIZENS   Register for jury pool            → /doj_jury (not the Jury tab)
10. JUDGE     Select jury for a CASE            → Jury  (needs case number)
11. JUDGE     Trial / verdict                   → Cases + Forms
12. CUSTODY   Commitment order if prison        → /doj_commitment
13. ANYONE    Print papers → inventory / archive
```

### Common confusion

| Screen | What it is | What it is NOT |
|--------|------------|----------------|
| **Hearings** | Calendar: when/where people meet in court | Not jury selection |
| **Jury** | Judge assigns people from the pool to a **case number** | Not "sign up here" for citizens |
| **Bail Hearing** (hearing type) | One scheduled event about bail | Does not auto-create a jury |
| **Jury trial** | Needs pool + judge selection (min jurors in config) | Separate from bail hearing |

## 3. How to open the panel

| Method | Notes |
|--------|--------|
| Keybind | Default **F5** (`Config.UI.openKey`) |
| Courthouse target | `ox_target` zones in `Config.Courthouse` |
| Close | **Esc** or same key again |

Your **role** (sidebar title, e.g. Supreme Court) comes from `doj_roles` in the database — not from ESX job alone.

## 4. Sidebar categories

### 4.1 Dashboard

Snapshot of open work (counts / shortcuts). Start here to see if anything needs attention; real work is in the other tabs.

### 4.2 Cases

**Purpose:** the **docket** — one row = one legal matter with a number (`CR-…` criminal, civil numbers as configured).

**Who:** prosecutor, judge, defense (view/manage by permission), Supreme Court.

**How to create (typical):**

1. Open **Cases** → **+ New Case**
2. Choose Criminal or Civil
3. Enter defendant CitizenID / identifier + full name
4. Optional: MDT incident, charges, facts
5. Create → note the **case number** (needed for warrants, hearings, jury)

### 4.3 Forms

**Purpose:** fill legal templates, save/print to inventory (`document_a4`).

**Who:** each role only sees forms allowed for that role (see role matrix below).

**How to use:**

1. Pick a form type
2. Fill fields (link case number when relevant)
3. Save / Print → accept legal warning → choose copies
4. Item appears in inventory → **Use** opens the filled document (requires **`nevera_printeri`**)
5. Optional Discord channel screenshot if webhooks/imgbb are configured

**Tip:** printing does **not** replace opening a Case or scheduling a Hearing — it produces the paper trail.

### 4.4 Warrants

**Purpose:** arrest / search warrant **requests** and **judicial decisions**.

```text
Police/DA request  →  Judge reviews  →  Approved or Denied  →  Police execute (RP)
```

### 4.5 Bail / Bond

**Purpose:** set bail, record payment / forfeiture / conditions for a defendant.

**Who:** mainly judge (and staff with bail permissions).

Bail hearing ≠ jury.

### 4.6 Hearings

**Purpose:** **schedule** court sessions (calendar).

1. **Hearings** → **+ Schedule hearing**
2. Case number, type (e.g. Bail Hearing, Probable Cause, Trial…), courtroom, date/time
3. Optional Discord link for voice

**Players are not auto-teleported** — notify them via RP, Discord, or in-game announce.

### 4.7 Jury

**Purpose (judge only):** assign jurors from the **pool** to a **specific case**.

**Citizen — join the pool** (not this tab): `/doj_jury` to register, `/doj_jury_odjava` to unregister.

**Judge — form a jury for a case:**

1. Open **Jury**
2. See **Jury Pool** count
3. Enter **case number** → **Search**
4. **Random jury** or **Manual (FIFO)** selection
5. Online selected players get a notify
6. Judge may **excuse** a juror (voir dire); after trial, **release** the jury

**Config:** `Config.Jury.minJurors` (default **6**), `maxJurors` (default **12**). If the pool is smaller than `minJurors`, selection **fails**.

### 4.8 Fines

Court fines / money judgments (amounts from config / laws). Judge / authorized staff.

### 4.9 Law Code (Penal Code / NKZ)

Browse statutes used on charges and forms (seeded in SQL). Display language follows `Config.Locale`.

### 4.10 Admin

Supreme Court tools: **Role management** (assign/change DOJ roles) and **Audit log**.

First Supreme Court user: `Install/sql/04_first_supreme_court.sql`.

## 5. Outside the sidebar

### Archive stashes

1. Walk to any `Config.Archive.Locations` point (City Hall, PD, hospital, …)
2. Enter **your role password**
3. Opens **your** role stash (or personal stash for citizens)
4. Only **`document_a4`** by default (`AllowedItems`)

### Commitment / prison

After Guilty + custody: `/doj_commitment` (police / DOC / judges per config). Not a sidebar tab.

## 6. Commands & keybinds

| Command / key | Who | What |
|---------------|-----|------|
| **F5** (default) | Everyone with access | Open / close DOJ panel |
| `/doj_help` | Everyone | Short command list |
| `/doj_jury` | Citizens / players | Register for jury pool |
| `/doj_jury_odjava` | Players in pool | Leave pool (if not selected) |
| `/doj_commitment` | Custody / DOC / judges | Commitment orders after prison sentence |
| `/refreshnkz` | Console / admin | Reload penal code from database |

## 7. Role → panel access

| Role | Cases | Forms | Warrants | Bail | Hearings | Jury manage | Fines | Law | Admin |
|------|:-----:|:-----:|:--------:|:----:|:--------:|:-----------:|:-----:|:---:|:-----:|
| Supreme Court | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Judge | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | — |
| Prosecutor | ✓ | ✓ | ✓ | ~ | ✓ | — | ~ | ✓ | — |
| Defense / PD | ✓ | ✓ | — | ~ | ✓ | — | — | ✓ | — |
| Police | ~ | ✓ | request | — | ~ | — | — | ✓ | — |
| Citizen | ~ | limited | — | ~ | — | register only | — | ~ | — |

`~` = limited / view / situational. Exact form list = `Enums.FormsByRole` in `shared/enums.lua`.

## 8. Quick FAQ

**"I registered for jury — what now?"** Wait in the pool. A judge must open **Jury**, enter a **case number**, and select jurors.

**"I scheduled a Bail Hearing — where is the jury?"** Hearings ≠ Jury. Use **Jury** only for trials that need one.

**"Jury selection says not enough jurors."** Need at least `Config.Jury.minJurors` (default 6) with status `available`.

**"Panel shows Citizen but I ran SQL."** `doj_roles.citizenid` must equal the live framework id (ESX: full `users.identifier`). Relog.

**"Use on document does nothing / deletes item."** `consume = 0`, correct export casing, start **`nevera_printeri`**.

## 9. One-page cheat sheet

```text
OPEN PANEL     F5 / courthouse target
NEW CASE       Cases → + New Case → keep the number
PAPERWORK      Forms → fill → Print → document_a4
WARRANT        request → judge approve → police execute
BAIL           Bail tab + optional Bail Hearing
COURT TIME     Hearings → + Schedule (tell players in RP)
JURY SIGN-UP   /doj_jury
JURY PICK      Jury → case number → Random/Manual (min 6)
PRISON         /doj_commitment
FILE CABINET   Archive location → role password → only A4 docs
ROLES/AUDIT    Admin (Supreme Court)
```
