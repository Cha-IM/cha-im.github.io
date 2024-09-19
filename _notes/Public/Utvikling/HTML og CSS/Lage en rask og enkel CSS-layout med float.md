---
title: Lage en rask og enkel CSS-layout med float
feed: show
date: 19-09-2024
---
  
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="YzEeZvx" data-pen-title="bilde-med-float" data-editable="true" data-user="ndla" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ndla/pen/YzEeZvx">
  bilde-med-float</a> by NDLA (<a href="https://codepen.io/ndla">@ndla</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
**Float** er et attributt i CSS som brukes til å få elementer til å "flyte" ved siden av hverandre, for eksempel for å få bilder til å flyte ved siden av tekst. Du kan se et eksempel på det i Codepen-rammen over. Om du klikker på CSS-fanen, ser du at i CSS-reglene `.bildeTilVenstre` og `.bildeTilHoyre` er det brukt `float: left` og `float: right` for å få bildene til å flyte til venstre og til høyre for teksten. Om du klikker på knappen "0.5x" under "Result"-rammen kan du se hele layouten på en side. Da får du en bedre følelse av hvordan elementene er plassert i forhold til hverandre.

## Eksempel 1: vertikal meny

Float kan brukes for å få hele seksjoner av nettsiden til å flyte ved siden av hverandre, for eksempel en sidemeny.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="abVqJjZ" data-pen-title="sidemeny-med-float" data-editable="true" data-user="ndla" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ndla/pen/abVqJjZ">
  sidemeny-med-float</a> by NDLA (<a href="https://codepen.io/ndla">@ndla</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>


I eksemplet over brukes `float: left` i CSS-reglene `nav` og `main` for å få sidemenyen `<nav>` og hovedinnholdet `<main>` til å flyte ved siden av hverandre. I CSS-koden har `nav` bredde satt til 35 prosent (`width: 35%;`), og main har bredde satt til 65 prosent (`width: 65%;`). Til sammen blir dette 100 prosent bredde, som betyr at de to elementene til sammen dekker hele bredden til elementet de ligger inne i, i dette tilfellet `<body>`.

Under disse to elementene ligger en tekst som viser hvor innholdet i `<main>` er hentet fra. Dette ligger inne i en `<footer>`. For å sørge for at `<footer>` ikke flyter ved siden av de andre elementene, men blir plassert for seg selv under de to flytende elementene, må vi legge inn koden `clear: left;` i CSS-regelen for elementet. Prøv å se hva som skjer med bunnteksten hvis du fjerner denne CSS-regelen.

### `box-sizing: border-box;`

Elementer som flyter ved siden av hverandre, kan til sammen ha maksbredde på 100 prosent av elementet de ligger inne i. Hvis bredden blir over 100 prosent, vil elementet lengst til høyre legges på neste ledige plass under de andre flytende elementene. Dette kan også skje hvis man har brukt padding på elementene, da padding legges til bredden på utsiden av elementet. For å unngå dette kan du bruke CSS-egenskapen `box-sizing: border-box;`. Denne egenskapen gjør at padding i stedet legges innenfor kanten på elementene, slik at bredden på hvert element ikke blir påvirket. Det er vanlig å legge denne koden inne i velgeren `*`, slik at denne egenskapen gjelder for hele nettsiden.

I rammen over er en slik regel lagt inn øverst i CSS-koden. Prøv å fjerne denne regelen og se hva som skjer.

## Eksempel 2: horisontal meny
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="ZEarewY" data-pen-title="layout-med-float" data-editable="true" data-user="ndla" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ndla/pen/ZEarewY">
  layout-med-float</a> by NDLA (<a href="https://codepen.io/ndla">@ndla</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

Vi kan også bruke float til å få elementer til å flyte ved siden av hverandre inne i et element, for eksempel i en horisontal meny.

I en horisontal meny flyter lenkene ved siden av hverandre. Det kan lages ved å legge menylenkene i ei punktliste `<ul>`. I CSS setter vi `float:left;` i regelen `nav li`, noe som vil påvirke alle `<li>`-elementer som ligger inne i `<nav>`-elementet. Da får vi lenkene til å flyte ved siden av hverandre i stedet for under hverandre. I samme regel fjerner vi kulepunktene med `list-style-type: none;`.

For at lenkene i menyen skal holde seg inne i `<nav>`-elementet, må også dette elementet ha `float: left;`. Hvis ikke, registrerer ikke nettleseren at det ligger noe inne i `<nav>`-elementet. Dette kan du se hvis du fjerner `float: left` fra `nav`. Prøv det. Hva skjer? Den grå boksen rundt lenkene forsvinner. Det er fordi lenkene (`li`) ikke lenger registreres inne i `nav`-boksen, og derfor vises de ikke boksen.


*Denne teksten er opprinnelig publisert på [ndla.no]([Lage en rask og enkel CSS-layout med float - Konseptutvikling og programmering - NDLA](https://ndla.no/subject:1:1352b19e-e706-4480-a728-c6b0a57ba8ae/topic:1:f7b88f8c-5f2f-4ea8-bdcf-1bd4811c37b3/topic:1:df9278b0-7252-4a62-a39c-3107d7f319f1/resource:c8e50788-7ef0-4a32-ba89-d882a8e25451))*