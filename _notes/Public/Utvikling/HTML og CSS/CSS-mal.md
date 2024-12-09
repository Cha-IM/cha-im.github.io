---
title: CSS-mal
feed: show
date: 09-12-2024
---
Det kan være praktisk å lage en CSS-mal som kan gjenbrukes på de forskjellige prosjektene dine. Etter hvert som du lager flere nettsider vil de se at det er mange CSS-regler som vil gå igjen, og da er det praktisk å ikke trenge å skrive de samm reglene på nytt hver gang du lager et nytt prosjekt. 

## CSS-mal for de mest vanlige HTML-elementene

Her er en enkel CSS-mal som dekker de grunnleggende stilene for `body`, overskrifter (`h1`–`h6`), og generell tekst:

```css
/* Enkel CSS-mal */

/* Global stil */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Body */
body {
  font-family: Arial, sans-serif; /* Standard font */
  line-height: 1.6;              /* Bedre lesbarhet */
  color: #333;                   /* Mørk tekstfarge */
  background-color: #f9f9f9;     /* Lys bakgrunn */
  padding: 10px;                 /* Litt innvendig marg */
}

/* Overskrifter */
h1, h2, h3, h4, h5, h6 {
  color: #222;                   /* Litt mørkere tekstfarge for overskrifter */
  margin-bottom: 10px;           /* Avstand under */
  line-height: 1.3;              /* God lesbarhet */
}

h1 {
  font-size: 2rem;               /* Største overskrift */
}

h2 {
  font-size: 1.75rem;
}

h3 {
  font-size: 1.5rem;
}

h4 {
  font-size: 1.25rem;
}

h5 {
  font-size: 1rem;
}

h6 {
  font-size: 0.875rem;
}

/* Avsnitt og tekst */
p {
  margin-bottom: 15px;           /* Avstand mellom avsnitt */
}

a {
  color: #007BFF;                /* Standard blå lenkefarge */
  text-decoration: none;         /* Ingen understrek */
}

a:hover {
  text-decoration: underline;    /* Understrek ved hover */
}

/* Listeelementer */
ul, ol {
  margin: 10px 0;
  padding-left: 20px;            /* Innrykk for lister */
}

li {
  margin-bottom: 5px;
}
```

### Hvordan bruke malen:

- Kopier denne CSS-en til en fil som heter `style.css`.
- Legg CSS-filen til HTML-en din ved å legge til denne linjen i `<head>`-seksjonen:
    
    ```html
    <link rel="stylesheet" href="style.css">
    ```
    

### Funksjoner i malen:

1. **Global regel (`*`)**:
    - Fjerner standard margin og padding, og setter `box-sizing` til `border-box` for enkel håndtering av elementstørrelser.
2. **Body**:
    - Gir en standard font, tekstfarge, bakgrunnsfarge og padding.
3. **Overskrifter**:
    - Størrelser og avstand for overskrifter (`h1`–`h6`) er tilpasset hierarkiet.
4. **Tekst og lenker**:
    - Avsnitt (`p`) får avstand mellom seg.
    - Lenker (`a`) har en fin blå farge og understreking ved hover.
5. **Lister**:
    - Innrykk for ul/ol-lister og små marginer mellom elementene.


