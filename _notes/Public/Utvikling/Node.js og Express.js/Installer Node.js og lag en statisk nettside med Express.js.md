---
title: Installer Node.js og lag en statisk nettside med Express.js
feed: show
date: 22-10-2024
---
Her er en grunnleggende guide til hvordan du kan sette opp en statisk webside med Express.js.

### 1. Installer Node.js og Express.js

Først må du ha Node.js installert på maskinen din. Du kan sjekke om du har Node.js ved å skrive følgende kommando i terminalen:

```bash
node -v
```

Hvis du ikke har Node.js installert, kan du laste det ned fra [nodejs.org](https://nodejs.org).

Deretter oppretter du en ny mappe for prosjektet ditt og installerer Express.js:

```bash
mkdir express-static-site
cd express-static-site
npm init -y
npm install express
```

### 2. Opprett en grunnleggende server med Express.js

I mappen din, opprett en fil som heter `app.js`. Denne filen vil inneholde koden for å sette opp serveren.

```javascript
// app.js
const express = require('express');
const app = express();
const path = require('path');

// Angi portnummer
const PORT = 3000;

// Middleware for å tjene statiske filer fra 'public'-mappen
app.use(express.static(path.join(__dirname, 'public')));

// Start serveren
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```
Les mer om denne koden her: [[Hva betyr koden i server.js?]]

### 3. Opprett en mappe for statiske filer

Lag en mappe som heter `public`. Dette er stedet hvor vi skal lagre alle statiske filer, som HTML, CSS, og bilder.

Skriv dette i terminalen:

```bash
mkdir public
```

eller opprett en mappe i *Explorer*.vinduet i VS Code som du kaller **public**.

### 4. Opprett HTML og CSS

Lag en enkel `index.html`-fil inne i `public`-mappen:

```html
<!-- public/index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Express Static Site</title>
  <link rel="stylesheet" href="/styles.css">
</head>
<body>
  <h1>Welcome to my static website!</h1>
  <p>This is a simple static web page served using Express.js</p>
</body>
</html>
```

Lag også en `styles.css`-fil i `public`-mappen:

```css
/* public/styles.css */
body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
  text-align: center;
  padding: 50px;
}

h1 {
  color: #333;
}

p {
  color: #666;
}
```

### 5. Start serveren

Gå tilbake til terminalen og start Express-serveren ved å kjøre følgende kommando:

```bash
node app.js
```

Serveren vil kjøre på [http://localhost:3000](http://localhost:3000), og du kan åpne denne adressen i nettleseren din for å se din statiske webside.

### Oppsummering

Du har nå satt opp en grunnleggende Express.js-applikasjon som serverer en statisk HTML-side med tilhørende CSS. Alle statiske filer (HTML, CSS, bilder, osv.) vil bli servert fra `public`-mappen, og Express håndterer dette for deg med `express.static()`-middleware.

Dersom du vil legge til flere statiske sider eller ressurser, kan du bare legge dem til i `public`-mappen!