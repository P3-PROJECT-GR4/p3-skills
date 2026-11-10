# Guide til p3-skills

Repoet er sat op med p3-skills. Guiden forklarer, hvordan I arbejder med skills'ene fra idé til færdig kode, og hvad de forskellige dokumenter er til.

En skill kaldes ved at skrive `/p3-skills:<navn>` i Claude Code, fx `/p3-skills:grill`. Nogle af dem bruger Claude også selv, når det passer.

## Flowet

1. **`grill`**: afklar idéen og begreberne.
2. **`til-spec`**: skriv det ned som en spec.
3. **`til-tickets`**: del specen op i opgaver.
4. **`skridt`**: implementér en ticket selv, ét skridt ad gangen.
5. **`review`**: få koden gennemgået før en pull request.
6. **`ai-log`**: kører efter hver opgave.
7. **`ai-rapport`**: bruges, når rapporten skal skrives.

I behøver ikke køre hele flowet hver gang. En lille rettelse kræver ikke en spec, men en ny feature har godt af hele vejen.

## Skills'ene

### `grill`: afklar, før I bygger

Brug den, når I har en idé, en feature eller et designvalg, der ikke er helt på plads. Claude stiller spørgsmål i runder, nummereret og med en anbefaling til hvert. I kan svare kort, fx "1 ja, 2 nej, vi vil hellere …".

Claude slår selv fakta op i koden og dokumentationen. Beslutningerne er jeres. Undervejs skriver Claude de afklarede begreber i `GLOSSARY.md` og store beslutninger som ADR'er.

> `/p3-skills:grill Vi vil have, at brugere kan booke et lokale i op til to timer`

### `til-spec`: fra samtale til spec

Brug den lige efter `grill`, i samme samtale. Claude samler det, I har talt om, til en spec: problem, løsning, user stories, beslutninger og hvad der er uden for scope.

Før specen skrives, aftaler I, hvordan featuren skal testes. Fokus er på få, generelle tests, der afprøver en hel del af programmets adfærd udefra, fx "en booking, der overlapper en anden, bliver afvist", frem for mange små tests af enkelte funktioner. Så kan I ændre koden indeni uden at skulle skrive testene om.

Derefter ser I specen som udkast, og når I godkender den, bliver den oprettet som et GitHub-issue.

### `til-tickets`: del arbejdet op

Brug den på et spec-issue, fx `/p3-skills:til-tickets #12`. Claude deler specen op i små opgaver. Hver opgave giver noget, der virker fra ende til anden og kan vises frem, fx "en bruger kan se ledige lokaler" med alt, hvad det kræver af data, logik, brugerflade og test. Det er i modsætning til opgaver som "lav hele databasen først", hvor intet virker, før alle dele er færdige.

Hver opgave viser, hvilke andre opgaver den venter på. Claude peger også på, hvad der kan laves samtidig af forskellige gruppemedlemmer, og hvor I risikerer merge-konflikter, fordi to opgaver rører den samme kode. Når I er enige, bliver opgaverne oprettet som sub-issues under specen.

### `skridt`: implementér selv med hjælp

Brug den, når I skal i gang med en ticket, fx `/p3-skills:skridt #14`. Claude lægger en plan og guider jer ét skridt ad gangen: hvad, hvorfor og hvor i koden, plus et hint. I skriver koden selv, og Claude tjekker hvert skridt, før I går videre.

### `review`: få koden gennemgået

Brug den, før I åbner en pull request. Claude gennemgår jeres ændringer mod glossaryet, ADR'erne og reglerne i `CLAUDE.md` og leder efter fejl, fortrolighedsproblemer og manglende tests. Hvert fund peger på fil og linje og forklarer hvorfor. Claude retter ikke selv; det gør I.

> Claude Code har sin egen indbyggede `/review`. Skriv det fulde navn `/p3-skills:review`.

### `ai-log`: log brugen af AI

Kører normalt af sig selv, når Claude har løst en opgave. Den tilføjer én linje med dato, kategori og værktøj i `docs/ai-brug/<feature>.md`. Har I brugt et andet AI-værktøj (ChatGPT, Copilot …), så tilføj linjen selv.

### `ai-rapport`: til rapporten

Samler alle logfilerne til et kort afsnit med tabeller over kategorier og værktøjer, som I selv retter til.

## Dokumenterne

| Fil | Hvad den er til |
| --- | --------------- |
| `CLAUDE.md` | Reglerne, som Claude læser ved starten af hver session: fortrolighed, commits, versionsstyring, hvem der skriver koden. Retter I den, gælder ændringen fra næste session. |
| `GLOSSARY.md` | Projektets ordliste. Hvert begreb har en dansk term, en kort definition, navnet i koden (`_Kode_`) og de ord, I har valgt fra (`_Avoid_`). Den sikrer, at I, rapporten og koden kalder det samme for det samme. |
| `docs/adr/` | ADR'er: én kort fil pr. vigtig beslutning med hvad I valgte og hvorfor. Kun beslutninger, der er svære at rulle tilbage, overraskende uden kontekst og et reelt valg mellem alternativer. De er gode at henvise til i rapporten. |
| `docs/agents/` | Korte instruktioner til Claude om jeres issue tracker og domænedokumenter. I skal sjældent røre dem. |
| `docs/ai-brug/` | Logfilerne over AI-brug, én pr. feature, og en README med kategorierne. |
| `docs/versionsstyring.md` | Jeres branches, og hvor mange reviews en pull request kræver. |

Holder I dokumenterne ajour, bliver Claudes hjælp bedre. Ændrer et begreb eller en beslutning sig, så opdatér glossaryet og ADR'en med det samme. `grill` gør det for jer, når I bruger den.

## Forkortelser og ord

| Ord | Betydning |
| --- | --------- |
| **ADR** | Architecture Decision Record: en kort registrering af en arkitekturbeslutning og begrundelsen for den. |
| **Spec** | Specifikation: en beskrivelse af en feature, før den bygges. |
| **Ticket** | En afgrænset opgave, her et GitHub-issue under en spec. |
| **Sub-issue** | Et issue, der hører under et andet issue på GitHub. |
| **PR** | Pull request: en anmodning om at flette en branch ind i en anden, som de andre reviewer. |
| **Review** | Gennemgang og godkendelse af en anden persons ændringer. |
| **Branch** | En separat udviklingslinje i git, fx `feature/login`. |
| **Commit / stage** | At gemme ændringer i git / at markere dem som klar til commit. Claude må stage, kun I committer. |
| **`gh`** | GitHub CLI: GitHubs kommandolinjeværktøj, som skills'ene bruger til issues. |
| **CLI** | Command-Line Interface: et program, der bruges fra terminalen. |

## Regler at huske

- Læg aldrig følsomme data i repoet eller i en samtale med Claude.
- Claude committer, pusher og merger aldrig. Læs de stagede filer igennem, og commit selv.
- Hvis I har valgt det, skriver I selv koden. Claude forklarer, gennemgår og vejleder.
