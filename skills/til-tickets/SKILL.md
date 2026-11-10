---
name: til-tickets
description: Deler en spec, en plan eller samtalen op i små opgaver, der hver giver noget, der virker fra ende til anden og kan vises frem. Forhandler opdelingen med gruppen og opretter opgaverne som GitHub sub-issues til spec-issuet med indbyggede "blocked by"-relationer. Brug den efter til-spec, eller når gruppen vil have tickets.
disable-model-invocation: true
---

# Til tickets

Du deler arbejdet op i **tickets**: små opgaver, der hver giver noget, der virker fra ende til anden, og som hver angiver, hvilke andre tickets den venter på.

Læs `docs/agents/issue-tracker.md`. Findes den ikke, så sig, at gruppen kan køre `setup` først.

**Sådan taler du med gruppen:** Brug almindelige ord og forklar idéen bag opdelingen, når du præsenterer den. Brug ikke fagudtryk som "vertical slice", "tracer bullet", "lodret skive" eller "expand–contract". Sig i stedet fx "hver opgave giver noget, der virker og kan vises frem".

## Proces

### 1. Saml konteksten

Arbejd ud fra samtalen. Giver gruppen et spec-issue (nummer eller URL), så læs hele beskrivelsen og kommentarerne:

```bash
gh issue view <nummer> --json number,title,body,comments
```

### 2. Kend koden

Udforsk koden, hvis du ikke har gjort det. Titler og beskrivelser bruger ordene fra `GLOSSARY.md` og respekterer ADR'erne. Kig efter oprydning i den eksisterende kode, der gør resten lettere at bygge. Den bliver sin egen ticket og kommer først.

### 3. Del arbejdet op

Hver ticket skal:

- **Virke fra ende til anden.** Den tager alt det med, en lille del af featuren kræver: data, logik, API, brugerflade og test. Undgå opdelinger efter lag ("lav hele databasen først"), hvor intet virker, før alle tickets er færdige.
- **Kunne vises frem.** En færdig ticket kan afprøves eller demonstreres for sig selv, fx på et vejledermøde.
- **Være lille.** Én person eller et par kan lave den i en overskuelig periode.

Giv hver ticket dens **blokeret af**: de tickets, der skal være færdige, før den kan begynde. En ticket uden blokeringer kan starte med det samme.

**Undtagelse: ændringer, der rammer hele koden.** En mekanisk ændring, der rører mange steder på én gang (omdøb et begreb, skift en delt type), kan ikke laves som én lille ticket uden at alt går i stykker undervejs. Del den i tre trin, og forklar gruppen hvorfor: først en ticket, der tilføjer den nye form ved siden af den gamle; så tickets, der flytter koden over del for del, mens alt stadig virker; og til sidst en ticket, der fjerner den gamle form.

### 4. Forhandl med gruppen

Vis opdelingen som en nummereret liste:

```
1. **<Titel>**
   Blokeret af: ingen
   Giver: <det, der virker, når den er færdig>

2. **<Titel>**
   Blokeret af: 1
   Giver: …
```

Forklar kort, hvorfor du har delt sådan op, og gør gruppen opmærksom på:

- **Hvad der kan laves samtidig**: hvilke tickets forskellige gruppemedlemmer kan arbejde på på samme tid, og hvor mange der kan være i gang på én gang.
- **Risiko for merge-konflikter**: tickets, der sandsynligvis rører de samme filer eller det samme modul. Foreslå en rækkefølge eller en fælles ticket, der laves først.

Spørg:

- Er størrelsen rigtig (for store, for små)?
- Venter hver ticket kun på det, den virkelig har brug for?
- Skal nogle slås sammen eller deles?

Gentag, til gruppen godkender opdelingen.

### 5. Opret som sub-issues

Opret tickets i rækkefølge, så de blokerende kommer først og har numre, de andre kan pege på. Hver ticket er et sub-issue til spec-issuet:

```bash
gh issue create --parent <spec-nummer> --title "<titel>" --body-file - <<'EOF'
<ticket-beskrivelse>
EOF
```

Virker `--parent` ikke i gruppens version af `gh`, så skriv `Part of #<spec-nummer>` øverst i beskrivelsen og sig det.

Tilføj derefter "blocked by"-relationerne med GitHubs indbyggede afhængigheder. API'et skal have det blokerende issues **database-id**, ikke dets nummer:

```bash
BLOKERER_ID=$(gh api repos/{owner}/{repo}/issues/<blokerende-nummer> --jq .id)
gh api -X POST repos/{owner}/{repo}/issues/<blokeret-nummer>/dependencies/blocked_by -F issue_id=$BLOKERER_ID
```

Fejler det, så skriv afsnittet "Blokeret af" i beskrivelsen i stedet og sig det.

Brug ingen labels. Luk og ændr ikke spec-issuet. Vis til sidst en liste med links, og log brugen med `ai-log` ("Dokumentation og planlægning").

## Skabelon til en ticket

```markdown
## Spec

#<spec-nummer>

## Hvad der skal bygges

Det, der skal virke, når ticketen er færdig, set fra brugerens side. Ikke en liste over lag.

## Accepteringskriterier

- [ ] Kriterie 1
- [ ] Kriterie 2

## Blokeret af

- #<nummer>, eller "Ingen (kan starte med det samme)". Udelad afsnittet, når relationerne er sat i GitHub.
```

Ingen filstier og ingen kodeuddrag; de forælder hurtigt. Undtagelse: et uddrag fra en prototype, der udtrykker en beslutning mere præcist end tekst.
