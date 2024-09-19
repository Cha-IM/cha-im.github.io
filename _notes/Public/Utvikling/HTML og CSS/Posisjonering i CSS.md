---
title: Posisjonering i CSS
feed: show
date: 19-09-2024
---
Posisjonering i CSS brukes til å kontrollere hvor elementer skal plasseres på en nettside. CSS gir deg flere forskjellige måter å styre dette på, avhengig av hvordan du vil at elementene skal oppføre seg i forhold til andre elementer og deres foreldre.

### Grunnleggende om CSS-posisjonering

For å kunne bruke posisjonering, trenger du å forstå de forskjellige **`position`**-verdiene og hvordan de påvirker elementers plassering på en nettside. Her er en oversikt over de viktigste posisjonsverdiene:

| **Verdi**       | **Beskrivelse**                                                                 |
|-----------------|---------------------------------------------------------------------------------|
| `static`        | Standardposisjonen – elementet plasseres i dokumentets naturlige flyt.           |
| `relative`      | Posisjonerer elementet relativt til hvor det normalt ville ha vært.              |
| `absolute`      | Posisjonerer elementet i forhold til nærmeste posisjonerte forelder.             |
| `fixed`         | Fester elementet til et fast punkt i nettleservinduet, selv når siden scroller.  |
| `sticky`        | Kombinerer egenskapene til `relative` og `fixed` – festes til en posisjon når det scroller forbi et visst punkt. |

### 1. **Static (Standardposisjon)**

`position: static;` er standardverdien for alle HTML-elementer. Dette betyr at elementer vil plasseres i henhold til den normale dokumentflyten, uten noen form for ekstra posisjonering.

Eksempel:
```css
div {
    position: static;
}
```
I dette tilfellet vil elementet vises der det naturlig plasseres i HTML-strukturen.

### 2. **Relative (Relativ posisjonering)**

`position: relative;` lar deg flytte et element fra sin normale posisjon i dokumentet uten å påvirke andre elementer. Elementet beholder sin plass i dokumentflyten, men du kan flytte det med **`top`**, **`right`**, **`bottom`** og **`left`**.

Eksempel:
```css
div {
    position: relative;
    top: 20px;  /* Flytter elementet 20px ned */
    left: 10px; /* Flytter elementet 10px til høyre */
}
```
Her vil elementet bli flyttet 20 piksler ned og 10 piksler til høyre fra sin opprinnelige posisjon.

### 3. **Absolute (Absolutt posisjonering)**

`position: absolute;` flytter et element ut av den normale dokumentflyten og plasserer det i forhold til nærmeste **posisjonerte** overordnede element. Hvis ingen overordnede elementer er posisjonert, vil elementet bli plassert i forhold til nettsidens rot (`<html>`-elementet).

Eksempel:
```css
div {
    position: absolute;
    top: 50px;
    left: 30px;
}
```
Dette vil plassere elementet 50 piksler ned og 30 piksler til høyre fra nærmeste posisjonerte overordnede element (eller hele siden, hvis ingen er posisjonert).

### 4. **Fixed (Fast posisjonering)**

`position: fixed;` plasserer elementet i forhold til nettleservinduet. Elementet vil være fast på dette stedet selv når brukeren scroller.

Eksempel:
```css
div {
    position: fixed;
    top: 0;
    right: 0;
}
```
Her vil elementet bli plassert i øverste høyre hjørne av nettleservinduet, og det vil forbli der uansett hvor mye brukeren scroller.

### 5. **Sticky (Klebrig posisjonering)**

`position: sticky;` kombinerer egenskapene til `relative` og `fixed`. Elementet oppfører seg som `relative` til du scroller det til en spesifisert posisjon, der det blir "klistrende" og oppfører seg som `fixed`.

Eksempel:
```css
div {
    position: sticky;
    top: 0;
}
```
Dette vil føre til at elementet oppfører seg som normalt inntil brukeren scroller det til toppen av vinduet. Når det når toppen, vil det forbli festet der til resten av siden scroller forbi det.

### Bruk av `z-index` med posisjonering

Når elementer overlapper hverandre, kan du bruke **`z-index`**-egenskapen til å bestemme hvilket element som vises øverst. Elementer med høyere `z-index` vil vises over de med lavere verdier.

Eksempel:
```css
div {
    position: absolute;
    top: 100px;
    left: 100px;
    z-index: 10;
}
```
Her vil elementet med `z-index: 10` vises over andre elementer med lavere `z-index`.


## Nærmeste Posisjonerte Element

Når du bruker `position: absolute;` i CSS, plasseres elementet i forhold til sitt nærmeste posisjonerte overordnede element. Det er viktig å forstå hva som menes med "nærmeste posisjonerte element" for å kunne bruke absolutt posisjonering effektivt.

#### Hva er et Posisjonert Element?

Et element anses som **posisjonert** hvis det har en `position`-verdi som ikke er `static`. Dette inkluderer verdier som `relative`, `absolute`, `fixed` og `sticky`. Med andre ord, for at et element skal betraktes som posisjonert, må det ha en eksplisitt posisjonsverdi angitt i CSS.

#### Hvordan Fungerer `position: absolute;`?

Når et element har `position: absolute;`, plasseres det i forhold til det nærmeste overordnede elementet som er posisjonert. Hvis det ikke finnes noen slike overordnede elementer, vil det plasseres i forhold til `body`-elementet (eller dokumentets rot).

#### Eksempel på Bruk

Anta at du har følgende HTML-struktur:

```html
<div class="container">
    <div class="box">Absolutt posisjonert</div>
</div>
```

Og tilhørende CSS:

```css
.container {
    position: relative;
    width: 300px;
    height: 200px;
    background-color: lightgray;
}

.box {
    position: absolute;
    top: 50px;
    left: 50px;
    width: 100px;
    height: 100px;
    background-color: coral;
}
```

Her skjer følgende:

1. **`.container`**-elementet har `position: relative;`. Dette betyr at det fungerer som referansepunktet for alle barnelementer med `position: absolute;`.

2. **`.box`**-elementet har `position: absolute;`. Dette betyr at det plasseres i forhold til det nærmeste posisjonerte overordnede elementet, som i dette tilfellet er `.container`.

3. **`.box`** vil derfor være plassert 50 piksler ned og 50 piksler til høyre fra den øverste venstre hjørnet av `.container`-elementet.

#### Hva Skjer Hvis Ingen Overordnede Elementer er Posisjonert?

Hvis det ikke finnes noen posisjonerte overordnede elementer (altså ingen av dem har `position`-verdier som ikke er `static`), vil elementet med `position: absolute;` bli plassert i forhold til dokumentets rot (`<html>`-elementet). 

Eksempel:
```html
<div class="box">Absolutt posisjonert</div>
```

```css
.box {
    position: absolute;
    top: 50px;
    left: 50px;
    width: 100px;
    height: 100px;
    background-color: coral;
}
```

I dette tilfellet, hvis `<div class="box">` er det eneste elementet med `position: absolute;`, vil det plasseres 50 piksler ned og 50 piksler til høyre fra øverste venstre hjørne av nettleservinduet.

## Oppsummering

Posisjonering i CSS gir deg kraftige verktøy for å styre hvor og hvordan elementer skal vises på nettsiden. Ved å bruke verdiene `static`, `relative`, `absolute`, `fixed` og `sticky`, kan du kontrollere både elementers plassering og hvordan de oppfører seg når siden blir scrollet. Kombinert med `z-index` kan du også styre hvilke elementer som skal ligge over andre i tilfeller av overlapping.

Når du bruker `position: absolute;`, er det viktig å forstå hvordan posisjonen beregnes i forhold til overordnede elementer. Elementet blir plassert i forhold til det nærmeste overordnede elementet som er posisjonert (med `position`-verdier som ikke er `static`). Hvis ingen slike elementer finnes, vil det plasseres i forhold til dokumentets rot. Dette gir deg fleksibilitet til å lage komplekse layouter med presis kontroll over plasseringen av elementer.

[[Eksempel på en websidelayout med posisjonerte elementer]]