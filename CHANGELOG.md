# Changelog

Alle noemenswaardige wijzigingen aan deze repo staan hier. Het formaat volgt
[Keep a Changelog](https://keepachangelog.com/) en de versienummers volgen
[Semver](https://semver.org/). We blijven op `0.x` zolang er geen externe
gebruikers zijn.

Een release is een git tag `vX.Y.Z` op `main` plus een GitHub Release met notes
die uit de Conventional Commits volgen.

## [Niet uitgebracht]

## [0.1.0] — 2026-11-03

De werkende repo-baseline. Nog geen applicatiecode: dit is het fundament
waarop `apps/*` landt.

### Toegevoegd

- npm workspaces (`apps/*`, `packages/*`) met Node gepind op 24 via `.nvmrc`.
- `npm run verify` — één opdracht die lokaal en in CI hetzelfde doet: lint,
  typecheck, test en build over root en alle workspaces.
- CI-workflow (GitHub Actions) die `.nvmrc` leest en `verify` draait.
- Branch protection op `main`: pull request verplicht, `verify` als vereiste
  check, geen force-push, lineaire historie, ook voor admins.
- `@radixs/tsconfig` — gedeelde TypeScript-basis met `strict` plus
  `noUncheckedIndexedAccess` en `exactOptionalPropertyTypes`.
- PR-template met de reviewchecklist uit het charter, en `CODEOWNERS`.
- Dependabot voor npm en GitHub Actions, wekelijks en gebundeld.
- `CONTRIBUTING.md` met de branch-, commit-, review- en releaseafspraken.
- Expliciet licentiebesluit: propriëtair, alle rechten voorbehouden.
- `.env.example` met alleen sleutelnamen; `.env*` staat in `.gitignore`.
