# ai-studio-radixs

Monorepo van Studio Radixs. Eén repo, meerdere apps en gedeelde packages, beheerd
met npm workspaces.

Deze repo bevat alleen code en configuratie. Strategie, planning en
architectuurbesluiten staan in Paperclip, niet hier.

## Vereisten

| Tool | Versie |
| --- | --- |
| Node.js | zoals vastgelegd in [`.nvmrc`](.nvmrc) — `nvm use` |
| npm | 11 of hoger (komt met Node 24) |

De Node-versie staat gepind in `.nvmrc` en CI leest datzelfde bestand. Vertrouw
niet op de versie die op je machine staat.

## Starten

```bash
nvm use
npm install
npm run verify
```

`npm run verify` draait dezelfde stappen als CI: lint, typecheck, test, build —
over de root en alle workspaces, en slaat stappen over die een workspace niet
heeft.

## Indeling

```
apps/           uitrolbare applicaties (één map per app)
packages/       gedeelde libraries en configuratie
docs/adr/       verwijzing naar de architectuurbesluiten
.github/        CI-workflow, PR-template, CODEOWNERS
```

Een nieuwe app of package is een map met een eigen `package.json` onder `apps/`
respectievelijk `packages/`. Door de workspace-globs wordt die automatisch
meegenomen in `npm install` en in CI; je hoeft de CI-workflow er niet voor aan te
passen.

Scripts die een workspace mag aanbieden en die CI dan oppakt: `lint`,
`typecheck`, `test`, `build`. Alle vier zijn optioneel per workspace.

## Werkafspraken

Kort samengevat; de volledige afspraken staan in [CONTRIBUTING.md](CONTRIBUTING.md).

- `main` is altijd releasebaar en beschermd. Werk gaat via een pull request.
- Branchnamen: `feat/<slug>`, `fix/<slug>`, `chore/<slug>`.
- Commits volgen [Conventional Commits](https://www.conventionalcommits.org/).
- CI moet groen zijn voordat er gemerged wordt.
- Geen secrets in de repo — ook niet in tests of voorbeeldbestanden. Zie
  [`.env.example`](.env.example).

Het volledige technische kader (ADR-proces, huisstack, reviewchecklist,
releaseproces) is het **Techniek-charter**, een taskdocument op Paperclip-task
STU-3. Deze repo volgt dat charter; waar de repo en het charter verschillen,
wint het charter en hoort de repo bijgewerkt te worden.

## Licentie

Propriëtair, alle rechten voorbehouden. Zie [LICENSE.md](LICENSE.md).
