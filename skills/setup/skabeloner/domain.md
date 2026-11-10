# Skabelon: docs/agents/domain.md

Tilføj egne formatbeskrivelser under "Læs før du går i gang", hvis gruppen har nogen (fx `docs/<format>.md`).

```markdown
# Domænedokumentation

## Læs før du går i gang

- **`GLOSSARY.md`** i roden: projektets ordforråd. Hvert begreb har en dansk term, en definition, et engelsk kodenavn under _Kode_ og de ord, vi undgår, under _Avoid_.
- **`docs/adr/`**: beslutninger, der berører det område, du arbejder i.

Filerne oprettes, når der er noget at skrive i dem. Findes de ikke endnu, så gå videre uden dem.

## Brug glossaryets ord

Når du navngiver et domænebegreb (i et issue, en test, en klasse), bruges kodenavnet fra `GLOSSARY.md`, og ingen af dem, der står under _Avoid_. Mangler begrebet, er det et tegn på, at det skal afklares og tilføjes, fx med skill'en `grill`.

## Gør opmærksom på konflikter med ADR'er

Hvis dit forslag strider mod en ADR, så sig det tydeligt i stedet for at gå uden om den:

> _Strider mod ADR-0002 (…), men bør genovervejes, fordi …_
```
