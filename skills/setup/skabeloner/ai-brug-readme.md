# Skabelon: docs/ai-brug/README.md

Kategorierne er faste, fordi `ai-log` og `ai-rapport` bruger dem. Skriv også en tom `docs/ai-brug/projektopsaetning.md` med overskrift og tabelhoved.

```markdown
# Brug af AI

Vi registrerer, hvad vi bruger AI til, så vi kan være åbne om det i rapporten. Vi noterer kun kategorien, ikke præcis hvad der blev lavet.

## Kategorier

| Kategori | Eksempler |
| -------- | --------- |
| Code review | Gennemgang af egen kode, forslag til forbedringer, fejlfund |
| Boilerplate-kode | Projektopsætning, gentagen standardkode |
| Idégenerering | Forslag til tilgange, design og løsninger |
| Rettelser | Hjælp til at finde og rette fejl |
| Dokumentation og planlægning | Glossary, ADR'er, specs, issues, formatbeskrivelser |

## Logfiler

Der er én logfil pr. feature i denne mappe, opkaldt efter feature-branchen: `feature/login` logges i `login.md`. Arbejde, der ikke hører til en feature, logges i `projektopsaetning.md`. Da hver feature-branch kun rører sin egen fil, giver loggen ingen merge-konflikter.

Hver brug af AI er én linje i tabellen. Samme kategori logges højst én gang pr. dag i samme fil:

| Dato | Kategori | Værktøj |
| ---- | -------- | ------- |
| 2026-01-15 | Code review | Claude Code |

Det gælder alle AI-værktøjer, også ChatGPT, Copilot og lignende. Har du brugt AI uden en agent, der logger, så tilføj linjen selv.

Til rapporten kan alle logfiler opsummeres med skill'en `ai-rapport`.
```

## projektopsaetning.md

```markdown
# AI-log: projektopsætning

| Dato | Kategori | Værktøj |
| ---- | -------- | ------- |
```
