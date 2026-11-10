---
name: ai-log
description: Tilføjer én linje (dato, kategori, værktøj) i docs/ai-brug/<feature>.md, når en agent har løst en opgave. Brug den automatisk til sidst i en opgave i repos, hvor CLAUDE.md beder om at logge AI-brug, eller når gruppen beder om at logge.
---

# AI-log

Du registrerer, at AI er brugt, uden at notere, hvad der præcis blev lavet.

## 1. Find filen

```bash
git branch --show-current
```

- Starter branchen med `feature/`, er filen `docs/ai-brug/<resten>.md`. `feature/login-side` giver `docs/ai-brug/login-side.md`.
- Ellers er filen `docs/ai-brug/projektopsaetning.md`.

Findes filen ikke, så opret den:

```markdown
# AI-log: <feature eller "projektopsætning">

| Dato | Kategori | Værktøj |
| ---- | -------- | ------- |
```

## 2. Vælg kategori

Brug præcis én af disse (står der andre i `docs/ai-brug/README.md`, gælder de):

| Kategori | Når |
| -------- | --- |
| Code review | Gennemgang af gruppens kode, forslag til forbedringer, fejlfund |
| Boilerplate-kode | Projektopsætning, gentagen standardkode |
| Idégenerering | Forslag til tilgange, design og løsninger, vejledning |
| Rettelser | Hjælp til at finde og rette fejl |
| Dokumentation og planlægning | Glossary, ADR'er, specs, issues, formatbeskrivelser |

Har opgaven dækket flere kategorier, så log én linje pr. kategori.

## 3. Tilføj linjen

```
| ÅÅÅÅ-MM-DD | <Kategori> | <Værktøj> |
```

- Datoen er dagens dato.
- Værktøjet er det, du kører i, fx `Claude Code`.
- **Spring linjen over**, hvis samme dato og kategori allerede står i filen.
- Skriv ingen detaljer om, hvad der blev lavet.

Tilføj linjen nederst i tabellen. Stage ikke og commit ikke filen for gruppen; den kommer med, når et gruppemedlem stager og committer resten. Nævn i én sætning, at linjen er tilføjet (eller sprunget over).
