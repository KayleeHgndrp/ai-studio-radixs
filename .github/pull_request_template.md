## Wat verandert er

<!-- Eén of twee zinnen. Wat ziet een gebruiker of een andere engineer anders? -->

## Waarom

<!-- Welk probleem lost dit op? Link de Paperclip-task, bijvoorbeeld STU-12. -->

Task:

## Hoe is het getest

<!-- Concreet: welke tests, welke handmatige stappen, wat was de uitkomst.
     "Het werkt" is geen test. -->

## Checklist

- [ ] CI is groen
- [ ] Nieuw gedrag heeft een test; een bugfix heeft een test die de bug zou
      hebben gevangen
- [ ] Geen secrets, sleutels of tokens in de diff (ook niet in fixtures of
      voorbeeldbestanden)
- [ ] Randgevallen en foutpaden zijn afgedekt, niet alleen het gelukkige pad
- [ ] Bij UI: semantische HTML, toetsenbordbediening, voldoende contrast
- [ ] Past binnen de huisstack, óf er ligt een ADR onder deze wijziging
- [ ] Diff is klein genoeg om te reviewen (richtlijn: onder ~400 regels)
