---
name: til-spec
description: Samler den aktuelle samtale til en spec og udgiver den som GitHub-issue efter godkendelse. Intet nyt interview, kun syntese af det, I allerede har talt om. Brug den efter grill, eller når gruppen beder om en spec.
disable-model-invocation: true
---

# Til spec

Du laver samtalen og din forståelse af koden om til en spec. Interview ikke gruppen igen. Saml det, I allerede ved. Det eneste, du afstemmer, er, hvordan featuren skal testes.

**Sådan taler du med gruppen:** Brug almindelige ord, og forklar idéen bag dine forslag. Brug ikke fagudtryk som "seam" eller "testindgang"; beskriv i stedet, hvad testene afprøver, og hvor i programmet de gør det.

Læs `docs/agents/issue-tracker.md` for at se, hvor specs udgives. Findes den ikke, så sig, at gruppen kan køre `setup` først, og spørg, om specen skal udgives som GitHub-issue med `gh` eller bare vises.

## Proces

### 1. Kend koden

Udforsk repoet, hvis du ikke allerede har gjort det. Brug ordene fra `GLOSSARY.md` (de danske termer i teksten, kodenavnene, når du taler om kode) og aldrig ordene under _Avoid_. Respektér ADR'erne i `docs/adr/`, og sig det tydeligt, hvis specen strider mod én.

### 2. Aftal, hvordan featuren testes

Fokus er på få, generelle tests, der afprøver en hel del af programmets adfærd udefra, fx "en booking, der overlapper en anden, bliver afvist", frem for mange små tests af enkelte funktioner. Så kan gruppen ændre koden indeni uden at skulle skrive testene om.

Find det sted i programmet, testene skal kalde: et offentligt API, en service, et kommandolinjeprogram eller en side i brugerfladen. Foretræk steder, der findes i forvejen, og vælg det, der dækker mest adfærd på én gang. Jo færre forskellige steder testene skal kalde ind, jo bedre.

Vis gruppen dit forslag nummereret og med din anbefaling: hvilken adfærd der testes, hvor testene kalder ind, og hvorfor. Vent på et ja, før du skriver specen.

### 3. Skriv udkastet

Skriv specen efter skabelonen nedenfor og vis den som udkast i samtalen. Tilpas, til gruppen godkender den.

### 4. Udgiv

Efter godkendelse oprettes ét GitHub-issue med specen som beskrivelse:

```bash
gh issue create --title "Spec: <titel>" --body-file - <<'EOF'
<specen>
EOF
```

Brug ingen labels og ingen triage. Vis linket til issuet. Log brugen med `ai-log` ("Dokumentation og planlægning"). Næste skridt er `til-tickets`.

## Skabelon

```markdown
## Problem

Problemet, som brugeren oplever det, set fra brugerens side.

## Løsning

Løsningen, set fra brugerens side.

## User stories

En LANG, nummereret liste. Hver i formen:

1. Som <aktør> vil jeg <funktion>, så <gevinst>.

Listen skal dække alle sider af featuren, også fejl, kanttilfælde og de aktører, der let bliver glemt (administrator, udvikler, underviser, testperson).

## Implementeringsbeslutninger

De beslutninger, der er truffet, fx:

- moduler, der bygges eller ændres, og deres grænseflader
- tekniske afklaringer fra gruppen
- arkitekturbeslutninger
- ændringer i skema og datamodel
- API-kontrakter
- konkrete samspil mellem dele

Ingen filstier og ingen kodeuddrag; de forælder hurtigt. Undtagelse: hvis en prototype har givet et uddrag, der udtrykker en beslutning mere præcist end tekst (en tilstandsmaskine, en datatype, et skema), så tag de vigtige dele med og skriv, at det kommer fra en prototype.

## Testbeslutninger

- Hvad der gør en god test her: kun ydre adfærd, ikke implementeringsdetaljer.
- Hvilken adfærd der testes, og hvor i programmet testene kalder ind, som det blev aftalt med gruppen.
- Hvilke moduler der testes.
- Eksisterende tests i repoet, der kan bruges som forbillede.

## Uden for scope

Det, specen bevidst ikke dækker.

## Noter

Alt andet, der er værd at vide.
```
