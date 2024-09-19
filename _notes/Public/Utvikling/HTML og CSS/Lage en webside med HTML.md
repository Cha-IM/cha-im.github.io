---
title: Lage en webside med HTML
feed: show
date: 19-09-2024
---
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/FtrfbxRZ5rA?si=B5ads0UJ6qkYrIcL" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
### Introduksjon til HTML

HTML (*HyperText Markup Language*) er grunnstrukturen i alle nettsider. Det brukes til å organisere innhold som tekst, bilder, lenker, knapper og mye mer. HTML består av **tagger** som brukes til å definere de ulike delene av en nettside.

En HTML-tagg ser slik ut:

```html
<tagg>Innhold</tagg>
```

- **Start-tagg**: `<tagg>` – Angir begynnelsen på elementet.
- **Innhold**: Tekst eller annet innhold som er plassert mellom start- og slutt-taggene.
- **Slutt-tagg**: `</tagg>` – Angir slutten på elementet (merk skråstreken `/`).

Noen HTML-tagger har ikke innhold, og disse kalles **selvlukkende tagger**, for eksempel `<img />` (for bilder) og `<br />` (for linjeskift).

HTML-dokumenter består av tre hoveddeler:
1. **Doctype-deklarasjon** – Definerer at dette er et HTML5-dokument:
   ```html
   <!DOCTYPE html>
   ```
2. **HTML-struktur** – Deler dokumentet i en **head** og en **body**:
   - **Head**-seksjonen inneholder metadata om nettsiden, som tittel, skriftsnitt og lenker til CSS-filer.
   - **Body**-seksjonen inneholder selve innholdet som vises i nettleseren.

Her er et eksempel på et enkelt HTML-dokument:
```html
<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Min Webside</title>
</head>
<body>
    <h1>Velkommen til min nettside!</h1>
    <p>Dette er et eksempel på en enkel HTML-side.</p>
</body>
</html>
```

Nå som du har en forståelse av hvordan HTML fungerer, kan vi se nærmere på noen av de mest nyttige HTML-taggene i en oversikt.

| **Kategori**           | **Tagg**           | **Beskrivelse**                               | **Eksempel**                      |
|------------------------|--------------------|-----------------------------------------------|-----------------------------------|
| **Struktur**           | `<html>`           | Ytre innpakning for HTML-dokumentet           | `<html lang="no">`                |
|                        | `<head>`           | Inneholder metadata om dokumentet             | `<head> ... </head>`              |
|                        | `<body>`           | Innholdet som vises på nettsiden              | `<body> ... </body>`              |
|                        | `<title>`          | Setter tittelen i nettleserfanen              | `<title>Min nettside</title>`     |
| **Tekstformatering**    | `<h1> - <h6>`      | Overskrifter (h1 størst, h6 minst)            | `<h1>Dette er en overskrift</h1>` |
|                        | `<p>`              | Avsnitt                                        | `<p>Dette er et avsnitt.</p>`     |
|                        | `<strong>`         | Fet tekst (sterkt fremhevet)                  | `<strong>Viktig tekst</strong>`   |
|                        | `<em>`             | Kursiv tekst (emphasis)                       | `<em>Viktig informasjon</em>`     |
|                        | `<br>`             | Linjeskift                                    | `Første linje<br>Andre linje`     |
| **Lenker og bilder**    | `<a>`              | Oppretter en lenke                           | `<a href="https://eksempel.com">Besøk oss</a>` |
|                        | `<img>`            | Viser et bilde                                | `<img src="bilde.jpg" alt="Et bilde">` |
| **Lister**             | `<ul>`             | Uordnet liste (punktliste)                    | `<ul><li>Punkt 1</li><li>Punkt 2</li></ul>` |
|                        | `<ol>`             | Ordnet liste (nummerert liste)                | `<ol><li>Første</li><li>Andre</li></ol>` |
| **Tabeller**           | `<table>`          | Oppretter en tabell                           | `<table> ... </table>`            |
|                        | `<tr>`             | Rad i en tabell                               | `<tr> ... </tr>`                  |
|                        | `<td>`             | Celle i en tabellrad                          | `<td>Innhold</td>`                |
| **Formularkomponenter** | `<form>`           | Skjema for brukerinndata                      | `<form action="/submit"> ... </form>` |
|                        | `<input>`          | Brukerinndatafelt                            | `<input type="text" name="navn">` |
|                        | `<button>`         | Knapp                                         | `<button>Send inn</button>`       |

Denne tabellen dekker noen av de mest nyttige og grunnleggende HTML-taggene med eksempler på hvordan de kan brukes.


### HTML-tagger med attributter

I tillegg til å definere innholdet i en nettside, kan HTML-tagger også inkludere **attributter** som gir mer informasjon eller funksjonalitet til elementene. Attributter skrives inne i start-taggen og består av et **navn** og en **verdi**.

Her er et eksempel på en HTML-tagg med attributter:
```html
<a href="https://example.com" target="_blank">Besøk Example</a>
```

- **`href`**: Dette attributtet spesifiserer URL-en som lenken peker til.
- **`target`**: Bestemmer hvordan lenken åpnes. I dette tilfellet åpnes den i en ny fane ved bruk av verdien `_blank`.

Attributter gjør HTML-taggene mer dynamiske og fleksible. De kan brukes til å sette alt fra lenker, bilder og formater til funksjoner som å åpne eksterne ressurser eller legge til stilklasser og ID-er for CSS og JavaScript.

Eksempler på vanlige attributter:
- **`src`**: Brukes for å spesifisere kilde (source) for medier som bilder eller videoer, for eksempel i `<img>`:
  ```html
  <img src="bilde.jpg" alt="Et bilde av en solnedgang" />
  ```
- **`alt`**: Gir en beskrivelse av et bilde hvis det ikke kan vises, og er viktig for tilgjengelighet:
  ```html
  <img src="bilde.jpg" alt="Et bilde av en solnedgang" />
  ```
- **`class`**: Brukes til å knytte et element til en CSS-klasse:
  ```html
  <p class="tekststil">Dette er en avsnittstekst.</p>
  ```
- **`id`**: Unik identifikator for et element, ofte brukt sammen med CSS eller JavaScript:
  ```html
  <div id="header">Dette er toppteksten.</div>
  ```

Attributter gir deg muligheten til å tilpasse HTML-elementene ytterligere for spesifikke oppgaver, som navigasjon, layout, eller interaktivitet.