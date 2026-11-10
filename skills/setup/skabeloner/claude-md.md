# Skabelon: CLAUDE.md-afsnit

Udfyld felterne i `{{…}}` ud fra svarene, og fjern de afsnit, gruppen har fravalgt. Teksten i _kursiv_ er vejledning til dig og skal ikke med i filen. Findes `CLAUDE.md` i forvejen, så indsæt afsnittene under projektets egen overskrift og bevar alt, der står der.

```markdown
# {{PROJEKTNAVN}}

{{EN SÆTNING OM PROJEKTET}}

## Fortrolighed

Følsomme data må aldrig lægges i dette repo eller deles i en agent-session. Det gælder bl.a. persondata, credentials og API-nøgler, IP-adresser og hostnavne, rå data og materiale, som andre har givet os i fortrolighed. Brug syntetiske eller anonymiserede eksempler. Hvis en opgave ser ud til at kræve rigtige følsomme data, så stop og spørg i stedet for at hente eller indsætte dem.
{{EKSTRA FORTROLIGHEDSREGLER}}
_Kun hvis gruppen har nævnt en samarbejdspartner eller følsomme data: tilføj fx "Materiale fra {{PARTNER}} ligger aldrig i repoet. Hvis en agent får det at læse, skriver den sin egen beskrivelse af formatet og kopierer aldrig indholdet." og hvilke mapper der er gitignoret._

## Commits: kun mennesker

En agent må aldrig selv committe. Den må gerne stage ændringer, men et gruppemedlem skal altid læse de stagede filer igennem og committe selv.

## Versionsstyring

{{KORT BESKRIVELSE AF BRANCHES OG REVIEWS, fx: "`main` får kun versioner, der virker, `dev` er udviklingsbranchen, og features udvikles på `feature/<feature>` fra `dev`. Pull requests til `dev` kræver mindst {{REVIEWS_DEV}} godkendt review. Ændringer kommer kun ind på `main` via en pull request fra `dev`, som kræver mindst {{REVIEWS_MAIN}} godkendte reviews."}} En agent må aldrig pushe, merge eller åbne pull requests mod {{BESKYTTEDE BRANCHES, fx `main` eller `dev`}}. Se `docs/versionsstyring.md`.

## Log brugen af AI

Når en agent har løst en opgave, tilføjer den én linje (dato, kategori, værktøj) i `docs/ai-brug/<feature>.md`, hvor `<feature>` er navnet på den aktuelle `feature/`-branch. Uden for en feature-branch bruges `docs/ai-brug/projektopsaetning.md`. Kategorien er én af dem i `docs/ai-brug/README.md`, og der noteres ikke, præcis hvad der blev lavet. Skill'en `ai-log` fra p3-skills gør det. Linjen stages og committes af et gruppemedlem som alt andet.

## Vi skriver koden selv

_Kun hvis gruppen selv skriver koden. Ellers erstattes afsnittet af "## Kode fra agenter" med gruppens egne regler._

- En agent skriver ikke implementeringskode, medmindre den bliver bedt om det. Dens rolle er at forklare, gennemgå vores kode, foreslå tilgange, skrive dokumentation og issues og finde fejl. Kodeeksempler skal være korte og illustrere en idé, ikke være en færdig løsning skrevet ind i filerne.
- Forklar hvorfor, ikke kun hvad. Ved forslag og fejlfund peges der på fil og linje, så vi selv kan rette det.

## Kode og domæne

- {{SPROGREGEL, fx "Dokumentation er på dansk, kode er på engelsk. Brug kodenavnet fra `GLOSSARY.md` og aldrig ordene under _Avoid_."}}
- Stack: {{STACK}}.
- Spørg før ændringer, der er svære at rulle tilbage: nye afhængigheder, ændringer i delte kontrakter eller databaseskema, og ændringer, der strider mod en ADR i `docs/adr/`.
- Hold dokumentationen ajour. Når en beslutning eller et begreb ændrer sig, opdateres `GLOSSARY.md` og ADR'erne i samme ombæring.

## Agent skills

### Issue tracker

{{ISSUE TRACKER-SÆTNING, fx "Issues ligger i repoets GitHub Issues og håndteres med `gh`."}} Se `docs/agents/issue-tracker.md`.

### Domain docs

Én `GLOSSARY.md` og `docs/adr/` i roden af repoet. Se `docs/agents/domain.md`.
```
