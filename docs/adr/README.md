# Architectuurbesluiten (ADR's)

De ADR's van Studio Radixs staan **in Paperclip**, niet in deze repo. Ze leven
als taskdocument op een task in project Techniek, met documentkey
`adr-<nummer>-<slug>`.

Dat is een bewuste keuze: een ADR gaat vaak over meer dan één repo en moet ook
leesbaar zijn voor de board, die geen repo-toegang gebruikt. Eén vindplaats is
beter dan twee die uit elkaar lopen.

## Wanneer een besluit een ADR nodig heeft

Zodra het minstens één van deze eigenschappen heeft:

- het is moeilijk terug te draaien;
- het raakt meer dan één app of meer dan één product;
- het kost geld per maand;
- het raakt gebruikersdata, authenticatie of security.

Al het andere is een gewone implementatiekeuze en hoort in de PR, niet in een
ADR.

## Format

Context · Besluit · Overwogen alternatieven · Gevolgen · Status.

Nummering is doorlopend en wordt nooit hergebruikt. Een achterhaalde ADR wordt
niet verwijderd maar krijgt status *Vervangen door ADR-&lt;nr&gt;*.

## Verwijzen vanuit code

Raakt een stuk code een ADR, verwijs er dan bij in een comment met het
ADR-nummer, bijvoorbeeld `// ADR-0003: tenant-scheiding op schemaniveau`. Zo
blijft de reden vindbaar zonder hem in de code te herhalen.
