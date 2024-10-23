---
title: Express Generator
feed: show
date: 22-10-2024
---

Du kan bruke **npx** til å generere et nytt Express.js-prosjekt med **Express Generator**, som er et verktøy som gjør det enkelt å sette opp et grunnleggende Express-prosjekt med forhåndsdefinerte strukturer og konfigurasjoner. Her er en trinnvis guide for hvordan du gjør det:

### 1. Installer Express Generator

Du kan installere Express Generator globalt på systemet ditt, eller bruke **npx** for å kjøre det uten å installere det globalt. Det anbefales å bruke **npx** for å unngå globale installasjoner. Slik gjør du det:

```bash
npx express-generator my-express-app
```

Dette vil opprette en ny mappe kalt `my-express-app` med alle nødvendige filer og mapper for et grunnleggende Express-prosjekt.

### 2. Naviger til prosjektmappen

Gå inn i den opprettede mappen:

```bash
cd my-express-app
```

### 3. Installer avhengigheter

Kjør følgende kommando for å installere de nødvendige avhengighetene som ble definert i `package.json`-filen:

```bash
npm install
```

### 4. Start serveren

Etter at avhengighetene er installert, kan du starte serveren:

```bash
npm start
```

Som standard vil serveren lytte på port 3000. Du kan åpne nettleseren din og navigere til [http://localhost:3000](http://localhost:3000) for å se den genererte Express-applikasjonen.

### 5. Prosjektstruktur

Når du oppretter prosjektet med **Express Generator**, vil du ha en struktur som ligner på følgende:

```
my-express-app/
├── app.js            # Hovedfilen for applikasjonen
├── bin/
│   └── www           # Fil for å starte serveren
├── public/           # Statisk innhold (CSS, JS, bilder)
│   ├── images/
│   ├── javascripts/
│   └── stylesheets/
├── routes/           # Definerte ruter
│   ├── index.js
│   └── users.js
├── views/            # Templater (f.eks. EJS, Pug)
│   ├── error.ejs
│   └── index.ejs
├── package.json      # Prosjektkonfigurasjon og avhengigheter
└── README.md         # Prosjektbeskrivelse
```

### 6. Redigere ruter og visninger

Du kan nå begynne å redigere rutene i `routes`-mappen og oppdatere visningene i `views`-mappen. Standardruten er definert i `routes/index.js`, og du kan tilpasse den etter behov.

### Eksempel på en enkel rute

I `routes/index.js` kan du for eksempel oppdatere standard GET-ruten til å sende en annen melding:

```javascript
const express = require('express');
const router = express.Router();

/* GET home page. */
router.get('/', (req, res) => {
  res.render('index', { title: 'My Express App' }); // Endre tittelen her
});

module.exports = router;
```

### Oppsummering

Ved å bruke **npx express-generator** kan du raskt sette opp en grunnleggende Express.js-applikasjon med en strukturert mappeoppsett og forhåndsdefinerte filer. Dette er en effektiv måte å komme i gang med utviklingen av Express-baserte applikasjoner, slik at du kan fokusere på å bygge funksjonaliteten i stedet for å sette opp grunnleggende konfigurasjoner.