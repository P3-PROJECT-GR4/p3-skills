# Skabelon: docs/agents/issue-tracker.md

Brug GitHub-versionen, hvis gruppen bruger GitHub Issues. Bruger gruppen noget andet (fx lokale filer eller Jira uden CLI), så skriv en tilsvarende fil med samme overskrifter og de kommandoer eller den mappe, der gælder.

## GitHub

```markdown
# Issue tracker: GitHub

Issues og specs ligger som GitHub Issues i dette repo. Alt håndteres med `gh`, som selv finder repoet ud fra `git remote`.

- **Opret**: `gh issue create --title "..." --body "..."`. Brug en heredoc til flerlinjede beskrivelser.
- **Læs**: `gh issue view <nummer> --json number,title,body,comments`
- **List**: `gh issue list --state open --json number,title`
- **Under-issue**: `gh issue create --parent <forælder> ...`. Hvis det ikke virker, skrives `Part of #<forælder>` øverst i beskrivelsen.
- **Blokeret af**: hent det blokerende issues database-id med `gh api repos/{owner}/{repo}/issues/<nummer> --jq .id` og tilføj relationen med `gh api -X POST repos/{owner}/{repo}/issues/<blokeret>/dependencies/blocked_by -F issue_id=<database-id>`.
- **Kommentér**: `gh issue comment <nummer> --body "..."`
- **Luk**: `gh issue close <nummer> --comment "..."`

Vi bruger ikke labels eller triage. En spec er ét issue, og dens tickets er sub-issues med "blocked by"-relationer.
```

## Lokale filer

```markdown
# Issue tracker: lokale filer

Specs og tickets ligger som Markdown i `docs/issues/`. En spec er `docs/issues/<slug>/spec.md`, og dens tickets er `docs/issues/<slug>/<NN>-<slug>.md`, nummereret i den rækkefølge, de kan laves. Hver ticket har en linje `**Blokeret af:** …`.
```
