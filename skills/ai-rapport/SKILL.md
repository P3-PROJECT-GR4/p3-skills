---
name: ai-rapport
description: Samler alle AI-logfiler i docs/ai-brug/ til et kort afsnit til projektrapporten med fordeling pr. kategori og værktøj. Brug den, når gruppen skal beskrive sin brug af AI i rapporten.
---

# AI-rapport

Du laver et kort, ærligt afsnit til rapporten om gruppens brug af AI, ud fra logfilerne.

## 1. Saml data

Læs alle `docs/ai-brug/*.md` undtagen `README.md`. Hver tabellinje `| dato | kategori | værktøj |` er én registrering. Featuren er filnavnet uden `.md` (`projektopsaetning` er arbejde uden for en feature).

Logfilerne kan ligge på forskellige branches. Spørg, om du skal tage den aktuelle branch eller samle fra flere (fx `git show origin/dev:docs/ai-brug/<fil>.md`), og sig hvilke branches du har brugt.

Tæl:

- antal registreringer pr. kategori
- antal registreringer pr. værktøj
- første og sidste dato
- evt. hvilke features der brugte AI mest (kun antal, ingen detaljer)

## 2. Skriv afsnittet

Vis tabellerne og et udkast på dansk, fx:

```markdown
## Brug af AI

Vi har registreret vores brug af AI-værktøjer løbende fra {første dato} til {sidste dato}. Hver gang et værktøj blev brugt til en opgave, noterede vi dato, kategori og værktøj, men ikke hvad der præcis blev lavet. Samme kategori blev højst noteret én gang pr. dag pr. feature, så tallene viser, hvor ofte vi har brugt AI til noget, ikke hvor meget.

| Kategori | Registreringer |
| -------- | -------------- |
| … | … |

| Værktøj | Registreringer |
| ------- | -------------- |
| … | … |

{2-4 sætninger om mønsteret, fx hvad AI mest blev brugt til, og at gruppen selv har skrevet implementeringskoden, hvis det står i CLAUDE.md.}
```

Hold dig til tallene. Gæt ikke på, hvad der blev lavet, og pynt ikke på det. Afsnittet er et udkast, som gruppen selv retter til.

Log brugen med `ai-log` ("Dokumentation og planlægning").
