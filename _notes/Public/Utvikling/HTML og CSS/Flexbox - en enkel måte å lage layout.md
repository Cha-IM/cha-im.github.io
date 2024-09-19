---
title: Flexbox - en enkel måte å lage layout
feed: show
date: 19-09-2024
---
Flexbox, eller Flexbox Layout, er en CSS-teknikk som gjør det enklere å lage fleksible og responsive layoutstrukturer. Flexbox gir deg kontroll over hvordan elementer skal distribueres og justeres i en container, og det er spesielt nyttig for å håndtere layout i en-dimensjonale rekkefølger – enten horisontalt eller vertikalt.

#### Hvordan Flexbox Fungerer

Flexbox brukes på en beholder (container) som inneholder flex-elementer. Flex-elementene vil automatisk tilpasse seg og fordele plassen i henhold til de spesifikke egenskapene du angir i CSS.

### 1. **Grunnleggende Terminologi**

- **Flex Container**: Den ytre containeren som omslutter flex-elementene. Denne defineres med `display: flex;` eller `display: inline-flex;`.
- **Flex Items**: De innvendige elementene i flex-containeren som du ønsker å styre.

### 2. **Definere en Flex Container**

For å bruke Flexbox må du først definere en flex container ved å bruke `display: flex;`:

```css
.container {
    display: flex;
}
```

### 3. **Flexbox Egenskaper for Flex Container**

- **`flex-direction`**: Bestemmer retningen på flex-elementene.
  - `row` (standard): Elementene plasseres horisontalt.
  - `column`: Elementene plasseres vertikalt.
  - `row-reverse`: Elementene plasseres horisontalt, men i omvendt rekkefølge.
  - `column-reverse`: Elementene plasseres vertikalt, men i omvendt rekkefølge.

  ```css
  .container {
      flex-direction: row;
  }
  ```

- **`flex-wrap`**: Bestemmer om flex-elementene skal brytes til neste linje.
  - `nowrap` (standard): Elementene vil ikke brytes til ny linje.
  - `wrap`: Elementene vil brytes til en ny linje om nødvendig.
  - `wrap-reverse`: Elementene vil brytes til en ny linje i omvendt rekkefølge.

  ```css
  .container {
      flex-wrap: wrap;
  }
  ```

- **`flex-flow`**: En kortform for å sette både `flex-direction` og `flex-wrap`.

  ```css
  .container {
      flex-flow: row wrap;
  }
  ```

- **`justify-content`**: Justerer flex-elementene langs hovedaksen (den retningen elementene plasseres i).
  - `flex-start` (standard): Justerer elementene til starten av containeren.
  - `center`: Justerer elementene i midten av containeren.
  - `space-between`: Fordeler elementene med lik avstand mellom dem.
  - `space-around`: Fordeler elementene med lik avstand rundt dem.
  - `space-evenly`: Fordeler elementene med lik avstand mellom dem og på kanten.

  ```css
  .container {
      justify-content: center;
  }
  ```

- **`align-items`**: Justerer flex-elementene langs tverraksen (perpendikulær til hovedaksen).
  - `stretch` (standard): Streker elementene for å fylle containerens høyde.
  - `flex-start`: Justerer elementene til toppen av containeren.
  - `center`: Justerer elementene i midten av containeren.
  - `flex-end`: Justerer elementene til bunnen av containeren.
  - `baseline`: Justerer elementene etter baseline.

  ```css
  .container {
      align-items: center;
  }
  ```

- **`align-content`**: Justerer linjene i en flex-container (brukes når det er flere linjer med flex-elementer).
  - `stretch` (standard): Streker linjene for å fylle containerens høyde.
  - `flex-start`: Justerer linjene til starten av containeren.
  - `center`: Justerer linjene i midten av containeren.
  - `space-between`: Fordeler linjene med lik avstand mellom dem.
  - `space-around`: Fordeler linjene med lik avstand rundt dem.
  - `space-evenly`: Fordeler linjene med lik avstand mellom dem og på kanten.

  ```css
  .container {
      align-content: space-between;
  }
  ```

### 4. **Flexbox Egenskaper for Flex Items**

- **`flex-grow`**: Bestemmer hvor mye et flex-element skal vokse i forhold til de andre elementene.
  - Standardverdi er `0` (ikke vokse).

  ```css
  .item {
      flex-grow: 2;
  }
  ```

- **`flex-shrink`**: Bestemmer hvor mye et flex-element skal krympe i forhold til de andre elementene.
  - Standardverdi er `1` (kan krympe).

  ```css
  .item {
      flex-shrink: 1;
  }
  ```

- **`flex-basis`**: Angir den opprinnelige størrelsen på et flex-element før eventuell vekst eller krymping.
  - Standardverdi er `auto`.

  ```css
  .item {
      flex-basis: 200px;
  }
  ```

- **`flex`**: En kortform for `flex-grow`, `flex-shrink` og `flex-basis`. 
  - Eksempel: `flex: 1 1 200px;` betyr `flex-grow: 1`, `flex-shrink: 1` og `flex-basis: 200px`.

  ```css
  .item {
      flex: 1 1 200px;
  }
  ```

- **`align-self`**: Overstyrer `align-items` for et spesifikt flex-element.
  - Verdier som `auto`, `flex-start`, `center`, `flex-end`, `baseline`, `stretch`.

  ```css
  .item {
      align-self: center;
  }
  ```

### Eksempel på Flexbox Layout

Her er et eksempel på en enkel layout med Flexbox:

#### HTML:
```html
<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flexbox Layout</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
    </div>
</body>
</html>
```

#### CSS:
```css
.container {
    display: flex;
    flex-direction: row; /* Plasserer elementene horisontalt */
    justify-content: space-around; /* Fordeler elementene med lik avstand rundt */
    align-items: center; /* Justerer elementene i midten av containerens høyde */
    height: 100vh; /* Full høyde på visningsvinduet */
    background-color: lightgray;
}

.item {
    background-color: coral;
    color: white;
    padding: 20px;
    width: 100px;
    text-align: center;
}
```

### Oppsummering

Flexbox gir deg kraftige verktøy for å lage fleksible og responsive layoutstrukturer. Ved å bruke flex-containerens egenskaper (`flex-direction`, `flex-wrap`, `justify-content`, `align-items`, `align-content`) og flex-item-egenskaper (`flex-grow`, `flex-shrink`, `flex-basis`, `align-self`), kan du enkelt kontrollere hvordan elementene plasseres og tilpasser seg i en beholder.

Her er et interaktivt eksempel på en enkel flexbox-layout. Prøv å endre CSS-koden for å se hvordan de ulike flex-egenskapene endrer layouten.
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="BagXZwQ" data-pen-title="enkel-flexbox-layout" data-editable="true" data-user="kadalsaune" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/kadalsaune/pen/BagXZwQ">
  enkel-flexbox-layout</a> by kadalsaune (<a href="https://codepen.io/kadalsaune">@kadalsaune</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>