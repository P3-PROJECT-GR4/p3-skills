# Format for GLOSSARY.md

## Struktur

```markdown
# {Projektets navn}

{En eller to sætninger om, hvad projektet er, og hvorfor det findes.}

## {Gruppe af begreber}

**Booking**:
En reservation af et lokale i et bestemt tidsrum.
_Kode_: `Booking`
_Avoid_: Reservation, aftale

**Lokale**:
Et rum, der kan bookes, med en fast kapacitet.
_Kode_: `Room`
_Avoid_: Sal, rum (som kodenavn)
```

Hvert begreb har:

- **Dansk term** i fed med kolon.
- **Definition** på en eller to sætninger. Hvad det _er_, ikke hvad det gør.
- **`_Kode_`**: det engelske navn, begrebet har i koden. Er koden på dansk, skrives kodenavnet stadig her.
- **`_Avoid_`**: de ord, der også bruges om det samme, men som vi har valgt fra. Det gælder både danske og engelske ord.

## Regler

- **Vær bestemt.** Findes flere ord for samme ting, så vælg det bedste og skriv resten under _Avoid_.
- **Hold definitionerne korte.** En eller to sætninger.
- **Kun projektets egne begreber.** Generelle programmeringsbegreber (timeout, fejltype, cache) hører ikke hjemme her, selvom projektet bruger dem meget.
- **Skriv antagelser som antagelser.** Har gruppen gættet på, hvordan noget virker, så skriv "… er vores antagelse" i definitionen.
- **Grupér under overskrifter**, når der opstår naturlige klynger. Er alle begreber i ét område, er en flad liste fint.

## Flere kontekster

De fleste repos har én `GLOSSARY.md` i roden. Har repoet flere tydeligt adskilte dele, kan der i stedet være en `GLOSSARY-MAP.md` i roden, der peger på en `GLOSSARY.md` i hver del og beskriver, hvordan delene hænger sammen. Er det uklart, hvilken kontekst et begreb hører til, så spørg.
