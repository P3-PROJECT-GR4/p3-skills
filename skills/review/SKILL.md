---
name: review
description: Gennemgår gruppens kode eller diff mod GLOSSARY.md, ADR'erne og reglerne i CLAUDE.md. Forklarer hvorfor og peger på fil og linje, men retter ikke selv, fordi gruppen skriver koden. Brug den, når gruppen beder om code review, gennemgang eller feedback på deres kode.
---

# Review

Du gennemgår gruppens kode, så de selv kan rette den. Du skriver ikke rettelserne ind i filerne.

## 1. Find det, der skal gennemgås

- Nævner gruppen en fil, en mappe, en PR eller en branch, så brug den (`gh pr diff <nummer>`, `git diff <base>...HEAD`).
- Ellers: den aktuelle diff mod den branch, featuren skal merges til (typisk `git diff dev...HEAD`, se `docs/versionsstyring.md`), plus ucommittede ændringer.

Læs `CLAUDE.md`, `GLOSSARY.md`, `docs/adr/` og `docs/agents/domain.md`, hvis de findes. Har featuren en ticket eller spec, så læs den også.

## 2. Hvad du kigger efter

I prioriteret rækkefølge:

1. **Fejl**: forkert adfærd, kanttilfælde, der ikke er håndteret, fejl, der bliver slugt.
2. **Fortrolighed**: credentials, persondata, rigtige data eller udleveret materiale i koden, testdata eller commits.
3. **Strider mod en ADR**: sig hvilken, og om ADR'en bør genovervejes.
4. **Glossaryet**: navne, der ikke bruger kodenavnet under `_Kode_`, eller som bruger et ord under `_Avoid_`. Begreber i koden, der mangler i glossaryet.
5. **Reglerne i `CLAUDE.md`**: fx tal, der skulle stå i konfigurationen, eller sprogregler.
6. **Tests**: afprøver testene programmets adfærd udefra, som specen har aftalt, eller hænger de på detaljer i, hvordan koden er skrevet indeni, så de går i stykker ved enhver omskrivning? Mangler der tests for accepteringskriterierne?
7. **Læsbarhed og design**: kun det, der gør en reel forskel.

## 3. Skriv fundene

For hvert fund:

```
**<Kort titel>** ([fil.cs:42](sti/til/fil.cs:42))
Hvad: <det, der er galt, i én sætning>
Hvorfor: <hvorfor det er et problem, fx hvilket scenarie der går galt eller hvilken regel/ADR/term det strider mod>
Retning: <hvordan gruppen kan gribe det an, uden færdig kode>
```

- Peg altid på fil og linje.
- Forklar hvorfor. Det er det, gruppen lærer af.
- Et kort kodeuddrag må gerne illustrere en idé, men skriv ikke løsningen.
- Sortér efter alvor, og sig tydeligt, hvad der er fejl, og hvad der er forslag.
- Er der ingen fund i en kategori, så spring den over. Ros kort det, der er godt, hvis det er relevant.

Ret ikke i filerne, medmindre gruppen udtrykkeligt beder om det. Log brugen med `ai-log` ("Code review").
