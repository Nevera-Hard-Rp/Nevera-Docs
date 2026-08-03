# Printeri (nevera_printeri + bl_bridge)

Kad igrač u inventaru koristi (**Use**) ispunjeni `document_a4`, otvara ga **`nevera_printeri`** (prikazuje ispunjeni HTML obrazac). Bez tog resursa, Use na dokumentu ne radi.

`nevera_printeri` ovisi o **`bl_bridge`** (framework/inventory/target bridge) — printer se neće pokrenuti bez njega.

## Instalacija

Oba resursa dolaze uz kupljeni Nevera Court paket, u `Install/companion/`.

```
resources/[nevera]/bl_bridge/
resources/[nevera]/nevera_printeri/
resources/[nevera]/Nevera_Court/
```

### server.cfg redoslijed

```cfg
setr bl:framework   "qbx"     # qb | esx | qbx
setr bl:inventory   "ox"
setr bl:target      "ox"
setr bl:context     "ox"
setr bl:progressbar "ox"
setr bl:radial      "ox"
setr bl:notify      "ox"
setr bl:textui      "ox"

ensure bl_bridge
ensure nevera_printeri
ensure Nevera_Court
```

## Fizički printeri (mapa)

Printer objekti se postavljaju u svijetu (small/medium/large), mogu biti:

- **Javni** — svi mogu koristiti
- **Po poslu** — samo određeni job
- **Zaključani kodom** — treba kod koji postavi vlasnik pri zaključavanju

Printer troši papir i toner iz inventara igrača; oboje se pune preko `ox_target` interakcije na printeru.

## Simptomi kad printer nije pokrenut

Notify: *nevera_printeri must be started to view documents.* → `ensure nevera_printeri` (i `bl_bridge`), pa restart.
