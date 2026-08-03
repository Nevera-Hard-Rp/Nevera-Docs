# Nevera Court — Exports & Integration

Useful for MDT and other third-party resources. **The resource name in `exports['…']` must match the actual folder name** on your server.

Primary export names are English. Croatian names exist only as legacy aliases — `Config.Locale` does not rename exports.

## Export reference

| Export | Module |
|--------|--------|
| `MDT_GetProvider` / `MDT_IsFelon` / `MDT_HasWarrant` / `MDT_NotifyWarrant` / `MDT_NotifyCase` / `MDT_NotifyVerdict` / `MDT_CreateIncident` | MDT bridge |
| `GetLaws` / `GetLaw` / `GetCategories` | Laws (NKZ) |
| `GetCase` / `GetActiveCasesForCitizen` | Cases |
| `HasActiveWarrant` / `GetActiveWarrants` | Warrants |
| `HasActiveBail` / `GetBailForCase` | Bail |
| `IssueFine` / `GetPendingFines` | Fines |
| `GetPlayerRoles` / `HasRole` | Roles |
| `CreateCommitmentOrder` / `CanExecuteCommitment` | Prison |
| `GetJury` / `CountAvailableJurors` | Jury |
| `GetHearingsForCase` / `GetNextHearing` | Hearings |
| `GetFormById` / `GetFormsForCase` / `CreateFormProgrammatically` / `GetBakedFormHtml` | Forms |

**Legacy HR aliases** (identical functions): `GetZakoni` → `GetLaws`, `GetZakon` → `GetLaw`, `GetKategorije` → `GetCategories`, `GetFormaById` → `GetFormById`. Prefer the English names in new integrations.

## Restricted exports

`IssueFine`, `CreateFormProgrammatically`, `CreateCommitmentOrder`, `CanExecuteCommitment`, and `GetBakedFormHtml` only answer calls from **this resource itself** or from a resource name listed in `Config.MDT.trustedInvokers`. Everything else gets `nil`/`false` back and a `BLOCKED …` line in console.

If your MDT or other integration's calls are being silently rejected, add its resource name to `Config.MDT.trustedInvokers` — see [Configuration](configuration.md).

## Usage example

```lua
local laws = exports['Nevera_Court']:GetLaws()
local law  = exports['Nevera_Court']:GetLaw('NKZ-304')
local cats = exports['Nevera_Court']:GetCategories()
```

Events and NUI callbacks use English names too (`nevera_court:…`, `getCases`, `printForm`, …).
