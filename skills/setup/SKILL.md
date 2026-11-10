---
name: setup
description: Sætter et gruppeprojekts repo op til at arbejde med agenter. Spørger sig igennem issue tracker, branches og reviews, gruppestørrelse, sprog og stack, og om gruppen selv skriver koden, og skriver derefter regler i CLAUDE.md og docs til agenter, AI-log og versionsstyring. Brug den, når et nyt projekt skal i gang, eller når gruppen beder om setup, opstart eller opsætning.
disable-model-invocation: true
---

# Setup

Du sætter et repo op, så gruppen og dens agenter arbejder efter de samme regler. Du skriver:

- et afsnit med regler i `CLAUDE.md` ([skabelon](skabeloner/claude-md.md))
- `docs/agents/issue-tracker.md` ([skabelon](skabeloner/issue-tracker.md))
- `docs/agents/domain.md` ([skabelon](skabeloner/domain.md))
- `docs/ai-brug/README.md` og `docs/ai-brug/projektopsaetning.md` ([skabelon](skabeloner/ai-brug-readme.md))
- `docs/versionsstyring.md` ([skabelon](skabeloner/versionsstyring.md))
- `docs/guide.md`: en guide til gruppen om flowet, skills'ene og dokumenterne ([skabelon](skabeloner/guide.md)). Kopiér den uændret. Har gruppen valgt, at agenten må skrive koden, så tilpas kun afsnittet om `skridt` og den sidste regel under "Regler at huske".

`GLOSSARY.md` og `docs/adr/` oprettes ikke her. Det gør `grill`, når det første begreb eller den første beslutning er på plads.

## 1. Se dig om først

Find selv det, du kan slå op, før du spørger:

- Findes `CLAUDE.md`, `AGENTS.md`, `docs/` eller `.gitignore` allerede? Læs dem, så du bygger videre i stedet for at overskrive.
- `git remote -v` og `git branch -a`: er der en GitHub-remote, og findes `dev` allerede?
- `gh repo view --json nameWithOwner,visibility,owner` og `gh api repos/{owner}/{repo} --jq .owner.type`: er det et org- eller personligt repo, og er det privat?
- Hvilke sprog og frameworks bruger koden (`package.json`, `*.csproj`, `pyproject.toml` osv.)?

## 2. Spørg i runder

Stil spørgsmålene nummererede, med din anbefaling under hvert, og formulér dem, så "ja" betyder, at anbefalingen accepteres. Spring spørgsmål over, som du allerede kan besvare ud fra repoet, men nævn hvad du fandt.

1. **Projektet**: Hvad hedder projektet, og hvad er det i én sætning?
2. **Gruppen**: Hvor mange er I i gruppen?
3. **Issue tracker**: GitHub Issues via `gh` (anbefalet, hvis der er en GitHub-remote), lokale Markdown-filer i `docs/issues/`, eller noget andet?
4. **Branch-strategi**: `main` + `dev` + `feature/<feature>` (anbefalet til grupper på 4 eller flere), `main` + `feature/<feature>`, eller jeres egen?
5. **Reviews**: Hvor mange godkendte reviews kræves pr. branch? Anbefal 1 til `dev` og et flertal af de øvrige gruppemedlemmer til `main` (fx 4 ved 7 personer), så en version kan udgives, selvom et par stykker er væk.
6. **Sprog**: Dokumentation på dansk og kode på engelsk (anbefalet), eller noget andet?
7. **Stack**: Hvilke sprog, frameworks og testværktøjer? Foreslå det, du fandt i repoet.
8. **Hvem skriver koden**: Skriver I selv implementeringskoden, så agenten forklarer, gennemgår og vejleder (anbefalet til læringsprojekter)? Eller må agenten skrive kode, og i så fald med hvilke regler?

Spørg **ikke** direkte til samarbejdspartnere, virksomheder eller kunder.

## 3. Fortrolighed

Standardreglen i `CLAUDE.md` gælder altid: følsomme data lægges aldrig i repoet eller i en agent-session. Sig det kort, når du præsenterer udkastet.

Hvis gruppen af sig selv nævner en samarbejdspartner, en virksomhed, testpersoner eller andre følsomme data, så tag en kort snak om:

- **Hvad der er følsomt**: rå data, logfiler, navne, IP-adresser, credentials, kundeoplysninger, udleveret materiale.
- **Hvor det ligger**: uden for repoet. Tilbyd at tilføje mapper eller filtyper til `.gitignore` (fx `data/`, `*.env`, `udleveret/`), men læs aldrig selv indholdet.
- **Egne formatbeskrivelser frem for originaler**: gruppen (eller agenten ud fra en beskrivelse) skriver sin egen beskrivelse af et format i `docs/`, i stedet for at kopiere partnerens materiale ind.
- **Syntetiske data**: test og demo med opdigtede værdier.

Skriv det, gruppen beslutter, som ekstra punkter under "Fortrolighed" i `CLAUDE.md`. Hvis gruppen ikke nævner noget, så nøjes med standardreglen.

## 4. Vis udkast, og skriv

Vis en kort oversigt over de filer, du vil skrive, og de vigtigste valg. Skriv filerne, når gruppen siger ja. Brug skabelonerne og udfyld felterne; fjern vejledningen i _kursiv_. Findes en fil allerede, så flet ind i stedet for at overskrive, og vis forskellen.

Reglerne i `CLAUDE.md` skal mindst dække: fortrolighed, at kun mennesker committer (agenten må stage), versionsstyring (agenten pusher, merger og åbner aldrig PR mod de beskyttede branches), logning af AI-brug, hvem der skriver koden (og at agenten forklarer hvorfor og peger på fil og linje), og at dokumentationen holdes ajour.

Stage filerne med `git add`, men commit ikke. Sig, at et gruppemedlem skal læse dem igennem og committe.

## 5. Branches og branch-regler (valgfrit)

Tilbyd, hvis strategien har en `dev`, og den ikke findes:

- **Opret `dev`**: `git branch dev main`. Push den kun, hvis gruppen udtrykkeligt siger ja.

Tilbyd at prøve at sætte branch-regler op på GitHub, men advar først:

> Private repos i en organisation på GitHubs gratisplan kan ikke få rulesets eller branch protection. Det samme gælder private personlige repos uden Pro (som studerende kan få gratis via GitHub Education). Offentlige repos kan godt. Hvis det ikke kan lade sig gøre, står reglerne stadig i `docs/versionsstyring.md`, og gruppen må overholde dem selv.

Opret kun regler efter et ja. Et ruleset pr. beskyttet branch, fx for `main`:

```bash
gh api -X POST repos/{owner}/{repo}/rulesets --input - <<'EOF'
{
  "name": "main",
  "target": "branch",
  "enforcement": "active",
  "conditions": { "ref_name": { "include": ["refs/heads/main"], "exclude": [] } },
  "rules": [
    { "type": "deletion" },
    { "type": "non_fast_forward" },
    { "type": "pull_request", "parameters": {
        "required_approving_review_count": 4,
        "dismiss_stale_reviews_on_push": true,
        "require_code_owner_review": false,
        "require_last_push_approval": false,
        "required_review_thread_resolution": false } }
  ]
}
EOF
```

Får du `403` eller `Upgrade to GitHub Pro or make this repository public`, så er det planen, der stopper det. Sig det, og gå videre. Et ruleset kan ikke kræve, at PR'er til `main` kommer fra `dev`. Det er en aftale i `docs/versionsstyring.md`.

## 6. Afslut

Log brugen med `ai-log` (kategori "Dokumentation og planlægning"), og opsummér, hvad der er skrevet, hvad der er staged, og hvad gruppen selv skal gøre (læse igennem, committe, evt. pushe `dev`). Slut med at pege på `docs/guide.md` som stedet, hvor alle i gruppen kan læse, hvordan de kommer videre, typisk med `grill`.
