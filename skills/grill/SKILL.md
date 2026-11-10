---
name: grill
description: Grundigt interview i runder om en plan, et design eller en idé, der samtidig skærper projektets ordforråd. Opdaterer GLOSSARY.md løbende og opretter ADR'er i docs/adr/, når en beslutning er svær at rulle tilbage. Brug den, når gruppen vil grilles, stressteste en idé, afklare begreber eller skrive i glossary eller ADR'er.
---

# Grill

Interview gruppen grundigt, indtil I har en fælles forståelse. Undervejs bygger du projektets domænemodel: begreber skrives i `GLOSSARY.md`, så snart de er afklaret, og de få store beslutninger skrives som ADR'er.

Læs `GLOSSARY.md`, `docs/adr/` og `docs/agents/domain.md`, hvis de findes, før første runde.

## Spørg i runder

Tænk på samtalen som et træ af beslutninger, hvor hver beslutning åbner for dem, der hænger på den. I hver runde stiller du alle de spørgsmål, der kan besvares nu, fordi det, de bygger på, allerede er afgjort. Spørgsmål, der afhænger af et svar, du ikke har fået endnu, venter til en senere runde.

**Sådan taler du med gruppen:** Brug almindelige ord. Begreber som "beslutningstræ" eller "frontier" er til dig; gruppen skal bare se spørgsmålene.

Nummerér spørgsmålene og giv din anbefaling til hvert. Vent så på svarene.

```
❓ **S1** - **<titel>**: <spørgsmålet, gerne flere afsnit og valgmuligheder>

➡️ <din anbefaling>

---

❓ **S2** - **<titel>**: <spørgsmålet>

➡️ <din anbefaling>
```

Formulér hvert spørgsmål, så "ja" betyder, at anbefalingen accepteres. Gruppen kan svare kort, fx "1 ja, 2 nej fordi …".

Hvert svar ændrer træet. Find igen de spørgsmål, der nu kan besvares, og stil næste runde. Et spørgsmål, der afhænger af et andet, som stadig er åbent i denne runde, hører til en senere runde.

## Fakta er dit job, beslutninger er gruppens

Spørg aldrig gruppen om noget, du selv kan slå op i koden, dokumentationen eller værktøjerne. Har et spørgsmål brug for en fakta, så find den (send gerne en subagent ud) og stil imens resten af rundens spørgsmål. Beslutningerne er gruppens: læg dem frem og vent.

Du er færdig, når der ikke er flere åbne spørgsmål: alle grene er besøgt, og intet er antaget i stilhed. Handl ikke på resultatet, før gruppen bekræfter, at I er enige.

## Undervejs: skærp ordforrådet

- **Udfordr mod glossaryet.** Bruger gruppen et ord, der strider mod `GLOSSARY.md`, så sig det med det samme: "Jeres glossary definerer 'booking' som X, men I lader til at mene Y. Hvilken er det?"
- **Skærp uklare ord.** Foreslå én præcis term, når et ord er vagt eller dækker flere ting: "Mener I 'bruger' som den, der logger ind, eller den, der betaler?"
- **Brug konkrete scenarier.** Find på kanttilfælde, der tvinger grænserne mellem begreberne frem.
- **Krydstjek med koden.** Siger gruppen, at noget virker på én måde, så tjek om koden er enig, og påpeg det, hvis den ikke er.

## Skriv i GLOSSARY.md med det samme

Når et begreb er afklaret, så skriv det ind med det samme i stedet for at samle op til sidst. Følg [GLOSSARY-FORMAT.md](GLOSSARY-FORMAT.md). Opret filen, når det første begreb er på plads.

`GLOSSARY.md` er en ordliste og intet andet: ingen implementeringsdetaljer, ingen spec, ingen kladder.

## ADR'er kun sjældent

Tilbyd kun en ADR, når alle tre gælder:

1. **Svær at rulle tilbage**: det koster noget at ombestemme sig senere.
2. **Overraskende uden kontekst**: en senere læser vil undre sig over, hvorfor det blev sådan.
3. **Et reelt valg**: der var rigtige alternativer, og I valgte ét af bestemte grunde.

Mangler én af dem, så spring ADR'en over. Følg [ADR-FORMAT.md](ADR-FORMAT.md).

Når en beslutning eller et begreb ændrer sig, så opdatér også de dokumenter, der bygger på det (fx ADR'er og formatbeskrivelser), i samme ombæring.

## Afslut

Log brugen med `ai-log` (typisk "Idégenerering" eller "Dokumentation og planlægning"). Næste skridt er ofte `til-spec`.
