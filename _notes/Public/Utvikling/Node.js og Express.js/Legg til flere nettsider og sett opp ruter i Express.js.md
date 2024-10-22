---
title: Legg til flere nettsider og sett opp ruter i Express.js
feed: show
date: 22-10-2024
---

Her er hvordan du kan legge til en ny side (f.eks. `about.html`) og sette opp ruter for å håndtere forskjellige sider i Express.js.

### 1. Legg til en ny side (about.html)

Opprett en ny fil som heter `about.html` i `public`-mappen:

```html
<!-- public/about.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About Us</title>
  <link rel="stylesheet" href="/styles.css">
</head>
<body>
  <h1>About Us</h1>
  <p>This is the about page of our website.</p>
  <a href="/">Go back to Home</a>
</body>
</html>
```

### 2. Modifiser serveren for å legge til ruter

Vi kan bruke Express-ruter til å håndtere forskjellige URL-stier. Oppdater `server.js`-filen for å håndtere to forskjellige sider: hovedsiden (`index.html`) og den nye `about.html`-siden.

```javascript
// server.js
const express = require('express');
const app = express();
const path = require('path');

// Angi portnummer
const PORT = 3000;

// Serve statiske filer fra 'public'-mappen
app.use(express.static(path.join(__dirname, 'public')));

// Rute for hjemmesiden (index.html)
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

// Rute for 'about' siden (about.html)
app.get('/about', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'about.html'));
});

// Start serveren
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

### 3. Navigasjon mellom sider

I både `index.html` og `about.html` kan du legge til lenker slik at brukeren kan navigere mellom sidene. Vi har allerede lagt til en lenke i `about.html`. Legg nå til en lenke i `index.html` for å navigere til `about.html`:

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
  <a href="/about">Learn more about us</a>
</body>
</html>
```

### 4. Start serveren på nytt

Hvis serveren allerede kjører, må du stoppe den (trykk `Ctrl+C` i terminalen), og deretter starte den på nytt:

```bash
node server.js
```

### 5. Test i nettleseren

- Åpne [http://localhost:3000](http://localhost:3000) for å se hjemmesiden.
- Klikk på lenken "Learn more about us" for å navigere til `about.html`.
- På `about.html`, klikk på "Go back to Home" for å gå tilbake til hovedsiden.

### Oppsummering

Du har nå lært å legge til flere sider i din Express.js-applikasjon, og du har satt opp ruter for å håndtere flere URL-stier. Express bruker funksjonen `app.get()` til å definere hva som skal skje når brukeren besøker forskjellige URL-er, og vi har nå opprettet en enkel side for både hjemmesiden og "om oss"-siden.