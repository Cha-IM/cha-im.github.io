---
title: Embedded JavaScript
feed: show
date: 22-10-2024
---

Når du bruker **EJS (Embedded JavaScript)** som templatemotor i en Express.js-applikasjon, får du muligheten til å lage dynamiske HTML-sider ved å injisere data i maler. Dette er nyttig hvis du vil unngå å lage statiske HTML-sider for hver rute og heller bruke en mal som kan gjenbrukes med forskjellig innhold.

### 1. Installer EJS

Først må du installere EJS i prosjektet ditt:

```bash
npm install ejs
```

### 2. Konfigurer Express til å bruke EJS

I `app.js`-filen må du konfigurere Express til å bruke EJS som templatemotor. Du kan også fjerne den statiske serveringen av HTML-sider fra `public`-mappen, siden vi nå skal bruke `.ejs`-filer.

Oppdater `app.js` slik:

```javascript
const express = require('express');
const path = require('path');
const app = express();
const PORT = 3000;

// Sett 'views'-mappen som standardmappe for maler (EJS-filer)
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');

// Rute for hjemmesiden
app.get('/', (req, res) => {
  res.render('index', { title: 'Welcome', message: 'Welcome to my static website!' });
});

// Rute for "about"-siden
app.get('/about', (req, res) => {
  res.render('about', { title: 'About Us', message: 'This is the about page of our website.' });
});

// Start serveren
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

### 3. Opprett EJS-maler

Opprett en ny mappe som heter `views` i rotmappen din. Denne mappen vil inneholde alle EJS-malene dine.

```bash
mkdir views
```

#### Opprett `index.ejs`:

```html
<!-- views/index.ejs -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><%= title %></title>
  <link rel="stylesheet" href="/styles.css">
</head>
<body>
  <h1><%= message %></h1>
  <a href="/about">Learn more about us</a>
</body>
</html>
```

#### Opprett `about.ejs`:

```html
<!-- views/about.ejs -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><%= title %></title>
  <link rel="stylesheet" href="/styles.css">
</head>
<body>
  <h1><%= title %></h1>
  <p><%= message %></p>
  <a href="/">Go back to Home</a>
</body>
</html>
```

### 4. Behold statisk CSS

Selv om vi ikke bruker HTML-filer fra `public`-mappen lenger, kan vi fortsatt bruke Express til å servere CSS- og andre statiske filer derfra.

Legg til følgende for å sikre at Express serverer CSS-filer:

```javascript
app.use(express.static(path.join(__dirname, 'public')));
```

Dette sikrer at vi fortsatt kan bruke CSS-filen `styles.css` i `public`-mappen.

### 5. Start serveren på nytt

Start serveren igjen:

```bash
node app.js
```

### 6. Test i nettleseren

- Gå til [http://localhost:3000](http://localhost:3000) for å se hjemmesiden.
- Klikk på lenken for å navigere til "about"-siden på [http://localhost:3000/about](http://localhost:3000/about).


### **Ekstra**: Legg til data fra serveren (simulere en database)

I stedet for å hardkode meldinger og data i ruter, kan du simulere en enkel database ved å lagre data i en lokal JavaScript-fil eller JSON-fil, og deretter sende denne informasjonen til EJS-malene. Dette vil gjøre applikasjonen mer dynamisk.

Eksempel: Du kan lage en "team"-side hvor informasjon om teammedlemmer vises dynamisk fra et JSON-objekt.

#### Eksempel:
```javascript
// app.js
const team = [
  { name: "Alice", role: "Developer" },
  { name: "Bob", role: "Designer" },
  { name: "Charlie", role: "Project Manager" }
];

app.get('/team', (req, res) => {
  res.render('team', { title: 'Our Team', members: team });
});
```

I `team.ejs` kan du loope gjennom teammedlemmene:

```html
<!-- views/team.ejs -->
<h1><%= title %></h1>
<ul>
  <% members.forEach(function(member) { %>
    <li><%= member.name %> - <%= member.role %></li>
  <% }) %>
</ul>
```


### Oppsummering

Ved å bruke **EJS** som templatemotor, kan du nå dynamisk generere HTML-sider basert på data sendt fra serveren. Du har lært å sette opp EJS, opprette maler, og injisere data fra Express-ruter ved å bruke `res.render()`. Dette gir mer fleksibilitet og reduserer repetisjon i HTML-koden din.