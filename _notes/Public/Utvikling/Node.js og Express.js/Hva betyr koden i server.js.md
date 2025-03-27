---
title: Hva betyr koden i server.js?
feed: show
date: 22-10-2024
---

Her er en linje-for-linje forklaring av koden:

#### **server.js:**
```javascript
const express = require('express');
```
- Denne linjen importerer Express-rammeverket, som brukes til å bygge webapplikasjoner og håndtere HTTP-forespørsler. Vi bruker `require` for å hente Express-modulen og lagrer den i variabelen `express`.

```javascript
const app = express();
```
- Her initialiseres en ny Express-applikasjon ved å kalle `express()`-funksjonen. Denne `app`-variabelen representerer selve Express-applikasjonen som vi skal konfigurere for å håndtere ulike ruter og tjenester.

```javascript
const path = require('path');
```
- Denne linjen importerer den innebygde `path`-modulen i Node.js, som hjelper til med å håndtere og manipulere fil- og mappestier. Dette gjør det enklere å sikre at vi bruker riktige stier på tvers av ulike operativsystemer.

```javascript
const PORT = 3000;
```
- Her defineres et portnummer som serveren skal kjøre på. I dette tilfellet er det satt til `3000`, men det kan endres til et annet nummer om ønskelig.

```javascript
app.use(express.static(path.join(__dirname, 'public')));
```
- Denne linjen bruker Express' `static`-middleware for å betjene statiske filer som HTML, CSS, bilder, og JavaScript fra mappen `public`. 
- `path.join(__dirname, 'public')` kombinerer nåværende mappe (`__dirname`) med undermappen `public`, og sikrer at stien til den statiske mappen er korrekt.
- Når denne middleware er konfigurert, vil alle filer i `public`-mappen være tilgjengelige for brukere via nettleseren uten å måtte spesifisere en egen rute.

```javascript
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```
- Denne linjen starter serveren ved å lytte etter forespørsler på porten som er definert av variabelen `PORT` (i dette tilfellet `3000`).
- `listen()`-funksjonen tar en funksjon som blir kalt når serveren starter, og denne funksjonen logger en melding til konsollen som bekrefter at serveren kjører og er tilgjengelig på `http://localhost:3000`.

---

**Oppsummert:**
- Denne koden oppretter en enkel Express-server som kjører på port 3000.
- Den serverer statiske filer fra `public`-mappen.
- Når serveren starter, vil den gi en beskjed i konsollen som forteller hvor den er tilgjengelig.
