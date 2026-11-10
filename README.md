# p3-skills

Danske skills til Claude Code til gruppeprojekter på universitetet. De sætter et repo op med fælles regler for gruppen og dens agenter, fører jer fra idé over spec til tickets, logger brugen af AI til rapporten og hjælper jer med at skrive og gennemgå koden selv.

Flowet er udviklet i et P3-projekt på AAU og bygger delvist på [Matt Pococks skills](https://github.com/mattpocock/skills).

## Installation

I Claude Code:

```
/plugin marketplace add P3-PROJECT-GR4/p3-skills
/plugin install p3-skills@p3-skills
```

Skills'ene kaldes med `/p3-skills:<navn>`, fx `/p3-skills:setup`. Dem uden `disable-model-invocation` kan Claude også selv bruge, når det passer.

Kræver [GitHub CLI](https://cli.github.com) (`gh`) logget ind, hvis I bruger GitHub Issues.

## Sådan hænger de sammen

```
setup  →  grill  →  til-spec  →  til-tickets  →  skridt / review
                                                   ↘ ai-log (efter hver opgave)
                                                       ↘ ai-rapport (til rapporten)
```

## Skills

| Skill | Hvad den gør |
| ----- | ------------ |
| `setup` | Spørger sig igennem issue tracker, branch-strategi og reviews, gruppestørrelse, sprog og stack, og om I selv skriver koden. Skriver regler i `CLAUDE.md` (fortrolighed, kun mennesker committer, versionsstyring, AI-log, "vi skriver koden selv", ajourført dokumentation) og `docs/agents/`, `docs/ai-brug/` og `docs/versionsstyring.md`, plus en guide til gruppen i `docs/guide.md`. Kan oprette `dev` og prøve at sætte branch-regler op på GitHub. |
| `grill` | Interviewer jer i runder med nummererede spørgsmål og en anbefaling til hvert. Slår selv fakta op; beslutningerne er jeres. Opdaterer `GLOSSARY.md` løbende (dansk term, definition, `_Kode_`, `_Avoid_`) og skriver ADR'er i `docs/adr/` for de få beslutninger, der er svære at rulle tilbage. |
| `til-spec` | Samler samtalen til en spec: problem, løsning, user stories, implementerings- og testbeslutninger, uden for scope og noter. Aftaler med jer, hvordan featuren testes, med fokus på få, generelle tests af programmets adfærd. Viser udkastet og udgiver det som GitHub-issue efter godkendelse. |
| `til-tickets` | Deler specen op i små opgaver, der hver giver noget, der virker fra ende til anden og kan vises frem. Forhandler opdelingen med jer, peger på parallelisering og konfliktrisici, og opretter dem som sub-issues med GitHubs "blocked by"-relationer. |
| `ai-log` | Tilføjer `\| dato \| kategori \| værktøj \|` i `docs/ai-brug/<feature>.md` efter en opgave. Springer over, hvis samme dato og kategori allerede står der. Ingen detaljer om, hvad der blev lavet. |
| `ai-rapport` | Samler alle AI-logfiler til et kort afsnit til rapporten med fordeling pr. kategori og værktøj. |
| `review` | Gennemgår jeres kode eller diff mod glossary, ADR'er og regler. Forklarer hvorfor og peger på fil og linje, men retter ikke selv. |
| `skridt` | Guider jer gennem en implementering ét skridt ad gangen og tjekker hvert skridt, uden at skrive løsningen for jer. |

Ingen af skills'ene bruger labels eller triage.

## Principper

- **Fortrolighed**: følsomme data lægges aldrig i repoet eller i en agent-session. Arbejder I med en samarbejdspartner, skriver I jeres egne formatbeskrivelser i stedet for at kopiere deres materiale ind.
- **Kun mennesker committer**: agenten må stage, men et gruppemedlem læser igennem og committer.
- **I skriver koden selv** (hvis I vælger det): agenten forklarer, gennemgår og vejleder.
- **Åbenhed om AI**: brugen logges løbende, så den kan beskrives ærligt i rapporten.

## Licens

MIT, se [LICENSE](LICENSE). `grill`, `til-spec` og `til-tickets` bygger på Matt Pococks MIT-licenserede skills; se [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
