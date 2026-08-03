# Tok suda — uloge i postupak

## Tko što radi

| Uloga | Zadužen za |
|-------|-----------|
| Građanin | Ograničeni obrasci, plaćanje jamčevine, prijava u porotu, osobna arhiva |
| Policija | Affidavit, pre-filing, zahtjevi za naloge → čeka suca |
| Tužitelj (DA) | Otvara/vodi predmete, tužbe, naloge, ročišta |
| Obrana / javni branitelj | Zastupanje na predmetu, obrasci obrane, ročišta |
| Službenik (Clerk) | Podrška oko podnošenja / ročišta |
| Sudac | Odobrava naloge, jamčevinu, zakazuje ročišta, bira porotu, kazne, presude |
| Vrhovni sud | Sve što sudac + Admin (uloge) + audit log |

## Tipičan kazneni tok

```text
Uhićenje / Affidavit
  → Kaznena prijava (Criminal Pre-Filing / Complaint)
  → Predmet otvoren (broj spisa)
  → Zahtjev za nalog (opcionalno) → Sudac odobri → Izvršenje
  → Ročište za jamčevinu / HUT
  → Prijedlozi i ročišta
  → Suđenje / porota
  → Presuda
  → Nalog za pritvor (ako kriv + zatvor) → DOC / pritvor izvršava
  → Ispis obrazaca → arhivske police
```

## Otvaranje panela

| Način | Opis |
|-------|------|
| Tipka | `Config.UI.openKey` (zadano **F5**) |
| Sudnica | `ox_target` na `Config.Courthouse` zonama |
| Meniji | ox_lib context / radial (gdje je uključeno) |

## Arhiva

Arhiva **nije** jedan zajednički ormar za sve. Sastoji se od:

1. **Fizičkih točaka** koje postaviš na mapu (`Config.Archive.Locations`)
2. **Logičkih stashova** po ulozi + lozinci (neovisno o tome koju si točku koristio)

Svaki igrač na bilo kojoj arhivskoj točki otvara **svoj** stash uloge nakon **svoje** lozinke.

## Komande

| Komanda | Opis |
|---------|------|
| **F5** (zadano) | Otvori / zatvori DOJ panel |
| `/doj_help` | Popis DOJ komandi |
| `/doj_jury` | Prijava u porotu |
| `/doj_jury_odjava` | Odjava iz porote |
| `/doj_commitment` | Nalozi za pritvor (custody / DOC / suci) |
| `/refreshnkz` | Ponovno učitaj kazneni zakon iz baze (konzola/admin) |
