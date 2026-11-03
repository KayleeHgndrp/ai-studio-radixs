# @radixs/tsconfig

Gedeelde TypeScript-basisconfiguratie. Het charter schrijft TypeScript met
`strict: true` voor; dit package is de plek waar dat één keer staat in plaats
van in elke app opnieuw.

## Gebruik

In de `tsconfig.json` van een app of package:

```json
{
  "extends": "@radixs/tsconfig/base.json",
  "compilerOptions": {
    "module": "nodenext",
    "moduleResolution": "nodenext",
    "outDir": "dist"
  },
  "include": ["src"]
}
```

Voeg `@radixs/tsconfig` toe als `devDependency` met `"*"` als versie; npm
workspaces linkt het dan naar deze map.

## Wat de basis bewust niet zet

- **`module` / `moduleResolution`** — die verschillen per doel. Een Node-service
  wil `nodenext`, een bundelde webapp wil `bundler`. Zet dit per app.
- **`lib`** — volgt uit `target` (dus geen DOM). Een webapp voegt zelf
  `"lib": ["ES2023", "DOM", "DOM.Iterable"]` toe.
- **`noEmit` / `outDir`** — hangt af van of de app zelf bundelt of via `tsc`
  bouwt.

## Over de strenge vlaggen

Naast `strict` staan `noUncheckedIndexedAccess` en
`exactOptionalPropertyTypes` aan. Die vangen precies de fouten die in review
makkelijk over het hoofd worden gezien: een array-index die `undefined` kan
zijn, en het verschil tussen "ontbrekende key" en "key met waarde
`undefined`".

Ze zijn streng, en dat is te verdedigen omdat we greenfield beginnen — ze
achteraf aanzetten op een bestaande codebase is veel duurder. Wil een app er
een uitzetten, dan hoort daar een regel uitleg bij in de `tsconfig.json` van die
app, zodat de volgende reviewer weet waarom.
