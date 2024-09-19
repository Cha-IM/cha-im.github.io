---
title: Hvordan bruke CSS til å endre utseendet på nettsiden
feed: show
date: 19-09-2024
---
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/-JC0s0v9M3c?si=y76p6m0vrhXqsEXh" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
### Introduksjon til CSS

CSS (Cascading Style Sheets) brukes for å style og formatere HTML-elementer på en nettside. CSS består av regler som definerer hvordan elementer skal vises visuelt. Hver regel er bygget opp av en **selektor**, en **egenskap** og en **verdi**. 

#### Eksempel på en CSS-regel:
```css
h1 {
    color: blue;
    font-size: 24px;
}
```

- **Selektor**: `h1` – Definerer hvilke elementer som skal styles (i dette tilfellet overskriften `<h1>`).
- **Egenskap**: `color`, `font-size` – Angir hva som skal endres (i dette eksemplet fargen og skriftstørrelsen).
- **Verdi**: `blue`, `24px` – Spesifiserer hvordan egenskapen skal endres (fargen settes til blå, og skriftstørrelsen til 24 piksler).

### Nyttige CSS-regler

| **Egenskap**          | **Beskrivelse**                                          | **Eksempel**                                   |
|-----------------------|----------------------------------------------------------|------------------------------------------------|
| **`color`**           | Endrer tekstfargen.                                      | `color: red;`                                  |
| **`background-color`**| Setter bakgrunnsfarge.                                   | `background-color: lightblue;`                 |
| **`font-size`**       | Bestemmer størrelsen på teksten.                         | `font-size: 16px;`                             |
| **`font-family`**     | Angir skrifttypen for teksten.                           | `font-family: Arial, sans-serif;`              |
| **`text-align`**      | Justerer tekstens plassering (venstre, høyre, senter).    | `text-align: center;`                          |
| **`margin`**          | Definerer ytre avstand (mellom elementer).               | `margin: 10px;`                                |
| **`padding`**         | Definerer indre avstand (innenfor et element).           | `padding: 15px;`                               |
| **`border`**          | Legger til en kantlinje rundt et element.                | `border: 1px solid black;`                     |
| **`width`**           | Setter bredden til et element.                           | `width: 100%;`                                 |
| **`height`**          | Angir høyden på et element.                              | `height: 50px;`                                |
| **`display`**         | Bestemmer hvordan et element skal vises (blokkelement, inline, osv.). | `display: flex;` `display: block;` |
| **`position`**        | Kontrollerer plasseringen av et element (statisk, relativ, absolutt, fast, sticky). | `position: absolute;` |
| **`flex`**            | Brukes for å lage fleksible layout-strukturer.           | `display: flex;` `justify-content: center;`    |
| **`overflow`**        | Bestemmer hvordan innhold utenfor et element skal håndteres (skjult, rullet, synlig). | `overflow: hidden;`                            |
| **`opacity`**         | Angir gjennomsiktigheten til et element.                 | `opacity: 0.5;` (50% gjennomsiktighet)         |
| **`z-index`**         | Bestemmer elementers stablingsrekkefølge (for overlappende elementer). | `z-index: 10;`                                |

### Hvordan bruke CSS:
Du kan bruke CSS på tre ulike måter:
1. **Inline-stiler** – Direkte i HTML-elementene (anbefales ikke for store prosjekter):
   ```html
   <h1 style="color: red;">Tittel</h1>
   ```

2. **Interne stiler** – I en `<style>`-tagg i HTML-dokumentets `<head>`:
   ```html
   <style>
       h1 {
           color: red;
       }
   </style>
   ```

3. **Eksterne stiler** – I en separat CSS-fil som lenkes til HTML-dokumentet (anbefales):
   ```html
   <link rel="stylesheet" href="style.css">
   ```

Ved å bruke eksterne stiler kan du enkelt holde HTML- og CSS-koden din ryddig og adskilt, noe som gjør det enklere å jobbe med større prosjekter.