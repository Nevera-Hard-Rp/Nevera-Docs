# Nevera Court — Pregled

**Department of Justice (DOJ)** sustav za ozbiljni pravni RP na FiveM-u. Policija, tužitelji, obrana, suci, službenici i građani provode kazneni i građanski postupak kroz jedan resurs:

- Otvaranje i vođenje predmeta s automatskim brojevima spisa
- Ispuna, potpis, ispis i arhiviranje službenih A4 sudskih obrazaca
- Zahtjev i izvršenje uhidbenih / nalog za pretragu
- Jamčevina, zakazivanje ročišta, izbor porote
- Unos presuda i izdavanje **naloga za pritvor** (hard RP predaja u zatvor)
- Izračun kazni, pregled kaznenog zakona (NKZ), zapisi u Discord

## Podržani frameworki

ESX · QBCore · Qbox · Standalone (`Config.Framework = 'auto'`)

## Jezici

`en` · `hr` · `de` · `fr` · `es` — puni UI + A4 obrasci + NKZ nazivi (`Config.Locale`)

## Ovisnosti

| Resource | Obavezno |
|----------|----------|
| `oxmysql` | Da |
| `ox_lib` | Da |
| Framework (ESX/QB/Qbox) ili standalone | Da |
| `ox_inventory` | Da (ispis/arhiva) |
| **`nevera_printeri`** | Da — vidi [Printeri](printeri.md) |
| **`bl_bridge`** | Da — ovisnost printera |
| `ox_target` | Preporučeno |

## Instalacija

Puna instalacijska uputa dolazi uz kupljeni resurs (`Install/README.md`). Ovdje su glavne točke:

1. Kopiraj `Nevera_Court`, `nevera_printeri`, `bl_bridge` u `resources/`
2. Pokreni SQL redom: `sql/01 → 02 → 03 → 04`
3. Dodaj `document_a4` item u inventory (vidi Install paket)
4. `ensure` redoslijed u `server.cfg`: `bl_bridge → nevera_printeri → Nevera_Court`
5. Prvi Vrhovni Sud postavi kroz `04_first_supreme_court.sql`

Detalji: [Tok suda](court-flow.md) · [Printeri](printeri.md)
