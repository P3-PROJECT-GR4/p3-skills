# Skabelon: docs/versionsstyring.md

Vælg den variant, der passer til gruppens branch-strategi, og udfyld `{{…}}`.

## Variant A: main, dev og feature-branches

```markdown
# Versionsstyring

## Branches

| Branch | Formål |
| ------ | ------ |
| `main` | Kun versioner, der virker. Hver merge til `main` er en ny version. |
| `dev` | Udviklingsbranchen, hvor features samles og afprøves sammen. |
| `feature/<feature>` | Én branch pr. feature, oprettet fra `dev`, fx `feature/login`. |

Brug korte navne med små bogstaver og bindestreger efter `feature/`, uden æ, ø og å. Hvis featuren hører til et issue, så nævn issue-nummeret i PR'en (fx `Closes #8`).

## Arbejdsgang

1. Opret `feature/<feature>` fra den nyeste `dev`.
2. Commit og push til din feature-branch.
3. Åbn en pull request fra `feature/<feature>` til `dev`.
4. Mindst {{REVIEWS_DEV}} fra gruppen reviewer og godkender, før der merges til `dev`.
5. Når `dev` virker og er klar til en ny version, åbnes en pull request fra `dev` til `main`. Den skal have mindst {{REVIEWS_MAIN}} godkendte reviews.

## Regler for `main`

- Ingen direkte commits eller push til `main`. Ændringer kommer kun ind via en pull request fra `dev`.
- En pull request til `main` skal have mindst {{REVIEWS_MAIN}} godkendte reviews fra andre end den, der åbnede den. {{BEGRUNDELSE, fx "Så kan der udgives en version, selvom et par stykker er væk."}}

## Regler for `dev`

- En pull request til `dev` skal have mindst {{REVIEWS_DEV}} godkendt review, før den merges.

## Agenter

En agent må stage ændringer, men aldrig committe, pushe, merge eller åbne pull requests mod `main` eller `dev`.
```

## Variant B: main og feature-branches

Som variant A, men uden `dev`: feature-branches oprettes fra `main`, og pull requests går direkte til `main` med mindst {{REVIEWS_MAIN}} godkendte reviews.

## Variant C: gruppens egen strategi

Beskriv branches, hvor de oprettes fra, hvor pull requests går hen, og hvor mange reviews hver kræver, med samme overskrifter som ovenfor. Afsnittet "Agenter" skal altid med.
