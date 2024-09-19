---
title: Eksempel på en websidelayout med posisjonerte elementer
feed: show
date: 19-09-2024
---


Her er et eksempel på en enkel nettside med et header, en navigasjonsmeny, et hovedinnholdsområde og en footer. Layouten er laget ved hjelp av forskjellige posisjoneringsmetoder i CSS.

#### HTML-struktur:
```html
<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Eksempel Layout</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header class="header">
        <h1>Min Nettside</h1>
    </header>
    <nav class="navbar">
        <ul>
            <li><a href="#">Hjem</a></li>
            <li><a href="#">Om oss</a></li>
            <li><a href="#">Tjenester</a></li>
            <li><a href="#">Kontakt</a></li>
        </ul>
    </nav>
    <main class="main-content">
        <section class="article">
            <h2>Artikkel Tittel</h2>
            <p>Dette er en eksempelartikkel som inneholder innhold. Her kan du plassere all relevant informasjon som skal vises til besøkende på nettsiden din.</p>
        </section>
    </main>
    <footer class="footer">
        <p>&copy; 2024 Min Nettside. Alle rettigheter reservert.</p>
    </footer>
</body>
</html>
```

#### CSS for Layout:
```css
/* Resetting margin and padding for better control */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
}

/* Header styling */
.header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background-color: #333;
    color: white;
    text-align: center;
    padding: 10px 0;
    z-index: 1000;
}

/* Navbar styling */
.navbar {
    position: fixed;
    top: 60px; /* Just under the header */
    left: 0;
    width: 100%;
    background-color: #444;
    color: white;
    padding: 10px 0;
}

.navbar ul {
    list-style: none;
    display: flex;
    justify-content: center;
}

.navbar li {
    margin: 0 15px;
}

.navbar a {
    color: white;
    text-decoration: none;
}

/* Main content styling */
.main-content {
    margin-top: 120px; /* Space for header and navbar */
    padding: 20px;
}

/* Article section styling */
.article {
    background-color: #f9f9f9;
    padding: 20px;
    border-radius: 5px;
}

/* Footer styling */
.footer {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    background-color: #333;
    color: white;
    text-align: center;
    padding: 10px 0;
}
```

### Hvordan Layouten Fungerer

1. **Header (`.header`)**:
   - Plassert med `position: fixed;`, slik at den alltid vises øverst på siden.
   - Har `z-index: 1000;` for å sikre at den vises over andre elementer.
   - Dekker hele bredden av vinduet og er 60 piksler høy.

2. **Navbar (`.navbar`)**:
   - Også med `position: fixed;` og plassert rett under headeren med `top: 60px;`.
   - Plasserer navigasjonslenkene horisontalt og sentrert.
   - Dekker hele bredden av vinduet.

3. **Main Content (`.main-content`)**:
   - Har en `margin-top` på 120 piksler for å unngå overlapping med headeren og navbaren.
   - Gir plass til innholdet under navigasjonsmenyen.

4. **Footer (`.footer`)**:
   - Plassert med `position: fixed;` og alltid nederst på siden.
   - Dekker hele bredden av vinduet og har en fast høyde.

Dette eksemplet viser hvordan du kan bruke CSS posisjonering for å lage en enkel og funksjonell layout. Header og footer er alltid synlige, mens hovedinnholdet og navigasjonen plasseres dynamisk i forhold til hverandre.

**Her ser du et interaktivt eksempel på denne layouten:**
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="bGPXRqg" data-pen-title="layout-med-position" data-editable="true" data-user="kadalsaune" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/kadalsaune/pen/bGPXRqg">
  layout-med-position</a> by kadalsaune (<a href="https://codepen.io/kadalsaune">@kadalsaune</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>