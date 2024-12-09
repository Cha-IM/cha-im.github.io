---
title: CSS-maler og klasser
feed: show
date: 09-12-2024
---
Det kan være praktisk å lage en CSS-mal som kan gjenbrukes på de forskjellige prosjektene dine. Etter hvert som du lager flere nettsider vil de se at det er mange CSS-regler som vil gå igjen, og da er det praktisk å ikke trenge å skrive de samm reglene på nytt hver gang du lager et nytt prosjekt. I tillegg kan det være lurt å lage egne klasser for de CSS-reglene du bruker ofte, som justering av tekst, størrelse og avstander, farger osv. Du finner eksempler på dette i denne artikkelen.

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


## CSS-regler for klasser

Her er en liste over noen vanlige klasser som kan være nyttige å inkludere i en standard CSS-fil. Disse klassene er generelle og kan brukes på ulike typer elementer for å tilpasse utseendet uten å lage nye spesifikke stiler hver gang.

---

### 1. **Typografi-klasser**

Brukes for å justere tekstens utseende og plassering.

```css
/* Sentralisert tekst */
.text-center {
  text-align: center;
}

.text-left {
  text-align: left;
}

.text-right {
  text-align: right;
}

/* Uthevet tekst */
.text-bold {
  font-weight: bold;
}

.text-italic {
  font-style: italic;
}

.text-uppercase {
  text-transform: uppercase;
}

.text-lowercase {
  text-transform: lowercase;
}

.text-capitalize {
  text-transform: capitalize;
}
```

---

### 2. **Margin og padding**

For enkel avstandskontroll.

```css
/* Margin */
.mt-1 { margin-top: 5px; }
.mb-1 { margin-bottom: 5px; }
.ml-1 { margin-left: 5px; }
.mr-1 { margin-right: 5px; }

.mt-2 { margin-top: 10px; }
.mb-2 { margin-bottom: 10px; }
.ml-2 { margin-left: 10px; }
.mr-2 { margin-right: 10px; }

/* Padding */
.pt-1 { padding-top: 5px; }
.pb-1 { padding-bottom: 5px; }
.pl-1 { padding-left: 5px; }
.pr-1 { padding-right: 5px; }

.pt-2 { padding-top: 10px; }
.pb-2 { padding-bottom: 10px; }
.pl-2 { padding-left: 10px; }
.pr-2 { padding-right: 10px; }
```

---

### 3. **Farger**

For å bruke på bakgrunner, tekst, eller grenser.

```css
/* Tekstfarger */
.text-primary {
  color: #007BFF; /* Blå */
}

.text-secondary {
  color: #6C757D; /* Grå */
}

.text-success {
  color: #28A745; /* Grønn */
}

.text-danger {
  color: #DC3545; /* Rød */
}

.text-warning {
  color: #FFC107; /* Gul */
}

/* Bakgrunnsfarger */
.bg-primary {
  background-color: #007BFF;
}

.bg-secondary {
  background-color: #6C757D;
}

.bg-success {
  background-color: #28A745;
}

.bg-danger {
  background-color: #DC3545;
}

.bg-warning {
  background-color: #FFC107;
}
```

---

### 4. **Layout**

Klasser for layoutjustering.

```css
/* Flexbox */
.flex {
  display: flex;
}

.flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.flex-column {
  display: flex;
  flex-direction: column;
}

.flex-space-between {
  display: flex;
  justify-content: space-between;
}

/* Usynlig element */
.hidden {
  display: none;
}
```

---

### 5. **Størrelser**

For rask justering av bredde, høyde, eller størrelse på elementer.

```css
/* Bredde */
.w-25 { width: 25%; }
.w-50 { width: 50%; }
.w-75 { width: 75%; }
.w-100 { width: 100%; }

/* Høyde */
.h-25 { height: 25%; }
.h-50 { height: 50%; }
.h-75 { height: 75%; }
.h-100 { height: 100%; }

/* Full skjerm */
.full-screen {
  width: 100vw;
  height: 100vh;
}
```

---

### 6. **Knapper**

For enkle og gjenbrukbare knappstiler.

```css
/* Primær knapp */
.btn {
  display: inline-block;
  padding: 10px 20px;
  font-size: 1rem;
  text-align: center;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.btn-primary {
  background-color: #007BFF;
  color: white;
}

.btn-secondary {
  background-color: #6C757D;
  color: white;
}

.btn-success {
  background-color: #28A745;
  color: white;
}

.btn-danger {
  background-color: #DC3545;
  color: white;
}
```

---

### 7. **Skygger og grenser**

For å gi dybde til elementene.

```css
/* Skygger */
.shadow-sm {
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

.shadow-md {
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.shadow-lg {
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.2);
}

/* Grenser */
.border {
  border: 1px solid #ddd;
}

.border-rounded {
  border-radius: 5px;
}

.border-circle {
  border-radius: 50%;
}
```

---

### Hvordan bruke disse klassene:

Disse klassene gir deg fleksibilitet til raskt å style elementer uten å måtte lage nye CSS-regler. For eksempel:

```html
<div class="text-center mt-2">
  <button class="btn btn-success">Klikk meg</button>
</div>
```

Disse klassene kan tilpasses og utvides etter behov. Dette oppsettet fungerer som en god start for nesten enhver nettside! 😊