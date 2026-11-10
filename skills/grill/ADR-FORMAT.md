# Format for ADR'er

ADR'er ligger i `docs/adr/` og nummereres fortløbende: `0001-slug.md`, `0002-slug.md` osv. Find det højeste nummer i mappen og læg én til. Opret mappen, når den første ADR skal skrives. Titel og slug skrives på dansk uden æ, ø og å i filnavnet.

## Skabelon

```markdown
# {Kort titel på beslutningen}

{1-3 sætninger: hvad er konteksten, hvad besluttede vi, og hvorfor.}
```

Mere skal der ikke til. En ADR kan være ét afsnit. Værdien ligger i at have skrevet ned, _at_ der blev truffet en beslutning, og _hvorfor_.

## Valgfrie afsnit

Tag dem kun med, når de tilføjer noget:

- **Status** (`foreslået | vedtaget | forældet | erstattet af ADR-NNNN`): når en beslutning tages op igen.
- **Overvejede alternativer**: når de fravalgte muligheder er værd at huske.
- **Konsekvenser**: når der er effekter længere nede, som ikke er åbenlyse.

## Hvornår en ADR

Alle tre skal gælde:

1. **Svær at rulle tilbage.**
2. **Overraskende uden kontekst.**
3. **Et reelt valg mellem alternativer.**

Typiske eksempler:

- **Arkitekturens form**: "Vi har én monolit med moduler, ikke microservices."
- **Hvordan dele taler sammen**: "Frontend og backend taler via REST, ikke gRPC."
- **Teknologivalg med binding**: database, framework, hosting. Ikke hvert bibliotek.
- **Grænser og scope**: "Vi gemmer ikke persondata, kun anonyme id'er." Fravalgene er lige så værdifulde som tilvalgene.
- **Bevidste afvigelser fra det oplagte**: alt, hvor en fornuftig læser ville antage det modsatte.
- **Krav, der ikke kan ses i koden**: krav fra kurset, vejlederen eller en samarbejdspartner.
- **Fravalgte alternativer, når grunden ikke er åbenlys**, så ingen foreslår dem igen om en måned.
