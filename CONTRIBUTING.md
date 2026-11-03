# Bijdragen aan ai-studio-radixs

Deze afspraken volgen het Techniek-charter (taskdocument op Paperclip-task
STU-3). Dit bestand is de praktische uitwerking voor deze repo.

## Branches en commits

`main` is altijd releasebaar en is beschermd: geen directe pushes, een pull
request is verplicht en CI moet groen zijn.

Branchnamen:

| Prefix | Waarvoor |
| --- | --- |
| `feat/<slug>` | nieuwe functionaliteit |
| `fix/<slug>` | bugfix |
| `chore/<slug>` | onderhoud, config, dependencies |
| `docs/<slug>` | alleen documentatie |

Commits volgen Conventional Commits: `feat:`, `fix:`, `chore:`, `docs:`,
`refactor:`, `test:`. Daarmee zijn release notes automatisch af te leiden uit de
geschiedenis.

Elke commit die door een agent wordt gemaakt eindigt op exact:

```
Co-Authored-By: Paperclip <noreply@paperclip.ing>
```

## Pull requests

Houd een PR klein — richtlijn: onder ongeveer 400 regels diff. Is het groter,
splits het eerst op.

De PR-beschrijving zegt **wat** er verandert, **waarom**, en **hoe het getest
is**. Het PR-template vraagt daar om.

### Hoe de review werkt

De CTO reviewt het werk van de engineers. De review wordt vastgelegd op de
Paperclip-task, niet als GitHub-approval.

Dat is een bewuste keuze: alle agents in deze company werken via één gedeelde
GitHub-identiteit. GitHub staat niet toe dat de auteur van een PR zijn eigen PR
goedkeurt, dus een harde eis van "één GitHub-approval" zou elke agent-PR
blokkeren. Daarom dwingt branch protection af wat machinaal te controleren is
(PR verplicht, CI groen, geen force-push naar `main`), en is het inhoudelijke
reviewverdict de review op de task.

De reviewchecklist staat in §4 van het charter. Samengevat:

1. Doet het aantoonbaar wat de acceptatiecriteria vragen.
2. Randgevallen en foutpaden zijn afgedekt, niet alleen het gelukkige pad.
3. Geen secrets, sleutels of tokens in de diff.
4. Nieuw gedrag heeft een test; een bugfix heeft een test die de bug zou hebben
   gevangen.
5. Bij UI: semantische HTML, toetsenbordbediening, voldoende contrast.
6. Geen N+1-queries en geen onbegrensde queries of loops over gebruikersdata.
7. Past binnen de huisstack, of er ligt een ADR.

**Definition of Done** — acceptatiecriteria aantoonbaar gehaald, CI groen,
review goedgekeurd, gemerged in `main`, de deliverable staat als work product op
de task, en als er een besluit in zat is de ADR geschreven.

## CI

CI draait op elke PR naar `main` en op elke push naar `main`:

```bash
npm ci
npm run verify
```

`verify` is de enige opdracht die je lokaal nodig hebt om te weten of CI groen
wordt. Hij draait lint, typecheck, test en build over de root en alle
workspaces, en slaat per workspace over wat er niet is (`--if-present`).

Voeg je een workspace toe, dan wordt die automatisch meegenomen. Draai een
nieuwe stap nooit alleen in CI zonder hem ook aan `verify` toe te voegen — CI en
lokaal moeten hetzelfde doen.

## Dependencies

- Voeg een dependency alleen toe als die een echt probleem oplost dat we niet in
  een paar regels zelf schrijven.
- Een dependency met terugkerende kosten of met toegang tot gebruikersdata
  vereist een ADR en board-approval vóór gebruik.
- Lockfile (`package-lock.json`) hoort bij de commit die de dependency toevoegt.

## Secrets

Nooit secrets in de repo, ook niet in een testfixture of een voorbeeldbestand.

- `.env.example` bevat **alleen sleutelnamen**, nooit waardes.
- Echte waardes gaan via Paperclip secret-proposals.
- `.env*` staat in `.gitignore`, met `.env.example` als uitzondering.

## ADR's

Een technisch besluit krijgt een ADR zodra het minstens één van deze
eigenschappen heeft: het is moeilijk terug te draaien, het raakt meer dan één
app, het kost geld per maand, of het raakt gebruikersdata, authenticatie of
security. Al het andere is een gewone implementatiekeuze en hoort in de PR.

ADR's leven in Paperclip — zie [docs/adr/README.md](docs/adr/README.md).

## Releases

Zie §5 van het charter. Kort:

- Semver, we blijven op `0.x` zolang er geen externe gebruikers zijn.
- Een release is een git tag `vX.Y.Z` op `main` plus een GitHub Release met
  notes uit de Conventional Commits. `CHANGELOG.md` wordt bijgehouden.
- Gate vóór release: CI groen, review goedgekeurd, migraties terugdraaibaar.
- Rollback: de vorige tag opnieuw uitrollen. Forward-fix alleen bij een
  triviale fout.
- Een productie-deploy met kosten of klantimpact vereist board-approval in
  Paperclip.
