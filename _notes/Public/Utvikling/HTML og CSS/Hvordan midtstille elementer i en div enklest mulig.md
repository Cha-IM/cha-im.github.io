---
title: Hvordan midtstille elementer i en div enklest mulig
feed: show
date: 09-12-2024
---

For å midtstille teksten i en `<div>` både vertikalt og horisontalt, kan du bruke **CSS Flexbox**. Dette er den enkleste og mest moderne måten å gjøre det på.

---

### Eksempel med CSS Flexbox

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Midtstille tekst</title>
  <style>
    .centered-div {
      display: flex;               /* Aktiverer flexbox */
      justify-content: center;     /* Horisontal midtstilling */
      align-items: center;         /* Vertikal midtstilling */
      height: 200px;               /* Eksempelhøyde */
      width: 200px;                /* Eksempelbredde */
      background-color: #f0f0f0;   /* Lys bakgrunn */
      border: 1px solid #ccc;      /* Ramme for synlighet */
    }
  </style>
</head>
<body>
  <div class="centered-div">
    Midtstilt tekst
  </div>
</body>
</html>
```

---

### Forklaring av CSS-reglene:

1. **`display: flex;`**  
    Aktiverer flexbox på elementet.
    
2. **`justify-content: center;`**  
    Sørger for at innholdet midtstilles horisontalt.
    
3. **`align-items: center;`**  
    Sørger for at innholdet midtstilles vertikalt.
    
4. **`height` og `width`**  
    Setter en fast størrelse på `<div>`-en for å demonstrere midtstilling. Du kan bruke prosentverdier, `vh`/`vw`, eller `auto` avhengig av behov.
    

---

### Alternativ: Bruke CSS Grid

Du kan også bruke CSS Grid hvis du foretrekker det:

```css
.centered-div {
  display: grid;                  /* Aktiverer grid-layout */
  place-items: center;            /* Midtstiller både vertikalt og horisontalt */
  height: 200px;
  width: 200px;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
}
```

Grid-metoden er enda mer kompakt når du bare vil midtstille innholdet.

---

Begge metodene fungerer godt for moderne nettlesere. Velg den som passer best til ditt prosjekt! 😊