---
title: Twitter-klone i Express.js
feed: hide
date: 29-10-2024
---

### **Oppgave: Bygg en Twitter-klone med Express.js**

I dag skal dere lage en enkel app som fungerer som Twitter. Dere vil kunne skrive innlegg som vises på siden, men i motsetning til ekte Twitter, lagrer vi innleggene bare i minnet på serveren (de forsvinner når serveren restartes).

### **Steg 1: Opprett Express-prosjektet**

1. Åpne terminalen (for eksempel ved å bruke terminalen i VS Code).
2. Skriv inn følgende kommando for å bruke `express-generator` til å sette opp et Express-prosjekt. `npx` sørger for at dere får tilgang til verktøyet uten å installere det globalt:

   ```bash
   npx express-generator twitter-clone --no-view
   ```

   Dette lager en mappe som heter `twitter-clone` med en ferdig prosjektstruktur.

3. **Gå inn i mappen**:

   ```bash
   cd twitter-clone
   ```

4. **Installer nødvendige pakker** for å kjøre prosjektet:

   ```bash
   npm install
   ```

Nå er prosjektet opprettet, og vi er klare til å lage ruter for å lagre og hente innlegg.

---

### **Steg 2: Lag en Liste for Innlegg**

Innleggene skal lagres i en liste midlertidig. Vi gjør dette ved å opprette en variabel for å holde innleggene.

1. Åpne `app.js` i prosjektmappen.
2. Øverst i filen, legg til en tom liste kalt `posts`. Dette vil være vår “database” for innlegg (kun i minnet):

   ```javascript
   // app.js

   const posts = []; // Liste for å lagre innlegg midlertidig
   ```

---

### **Steg 3: Opprett Ruter for å Hente og Lage Innlegg**

Nå skal vi lage to ruter:
- En **GET-rute** som gir oss alle innlegg.
- En **POST-rute** som lar oss legge til nye innlegg.

1. Åpne `routes/index.js`.
2. **Lag en liste** for å lagre innlegg midlertidig:
```javascript
const posts = []; // Liste for å lagre innlegg midlertidig
```
3. **Lag GET-ruten** som henter alle innleggene:

   ```javascript
   const express = require('express');
   const router = express.Router();

   // GET-rute for å hente alle innlegg
   router.get('/posts', (req, res) => {
     res.json(posts); // Sender listen over innlegg som JSON
   });
   ```

4. **Lag POST-ruten** for å legge til nye innlegg:

   ```javascript
   // POST-rute for å lage et nytt innlegg
   router.post('/posts', (req, res) => {
     const { username, content } = req.body; // Henter brukernavn og innhold fra forespørselen
     
     // Sjekk at både brukernavn og innhold er fylt ut
     if (!username || !content) {
       return res.status(400).json({ error: 'Brukernavn og innhold er påkrevd' });
     }

     // Lag et nytt innlegg som objekt
     const newPost = {
       id: posts.length + 1,
       username,
       content,
       timestamp: new Date().toLocaleString()
     };

     posts.push(newPost); // Legger til det nye innlegget i listen
     res.status(201).json(newPost); // Sender tilbake det nye innlegget
   });
   ```

5. **Legg til støtte for ruter** i `app.js` for at serveren skal kunne bruke rutene vi definerte i `routes/index.js`. Legg til denne linjen i `app.js`:

   ```javascript
  var router = express.Router();
   ```

---

### **Steg 4: Lag HTML-Siden for Innlegg**

Nå skal vi lage en enkel HTML-side som lar oss skrive innlegg og vise dem. Dette gjør vi i `public`-mappen, der vi legger til en ny fil kalt `index.html`.

1. Gå til `public`-mappen i prosjektet.
2. Opprett en ny fil som heter `index.html`.
3. Skriv inn følgende HTML-kode i `index.html`:

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>Twitter-klone</title>
     <link rel="stylesheet" href="/stylesheets/style.css">
   </head>
   <body>
     <h1>Twitter-klone</h1>

     <!-- Skjema for å lage et nytt innlegg -->
     <form id="postForm">
       <input type="text" id="username" placeholder="Brukernavn" required>
       <textarea id="content" placeholder="Skriv ditt innlegg her..." required></textarea>
       <button type="submit">Publiser</button>
     </form>

     <!-- Område for å vise innlegg -->
     <div id="postsContainer"></div>

     <script src="/javascripts/app.js"></script>
   </body>
   </html>
   ```

---

### **Steg 5: Lag JavaScript for å Håndtere Innlegg på Klientsiden**

Vi skal nå lage JavaScript for å hente og sende innlegg fra `index.html`.

1. Gå til `public/javascripts`-mappen.
2. Opprett en fil som heter `app.js`.
3. Skriv inn følgende kode:

   ```javascript
   // public/javascripts/app.js

   // Hente og vise innleggene
   async function fetchPosts() {
     const response = await fetch('/posts');
     const posts = await response.json();
     const postsContainer = document.getElementById('postsContainer');
     postsContainer.innerHTML = '';

     posts.forEach(post => {
       const postElement = document.createElement('div');
       postElement.innerHTML = `
         <h3>${post.username}</h3>
         <p>${post.content}</p>
         <small>${post.timestamp}</small>
         <hr>
       `;
       postsContainer.appendChild(postElement);
     });
   }

   // Legge til nytt innlegg
   document.getElementById('postForm').addEventListener('submit', async (e) => {
     e.preventDefault();
     const username = document.getElementById('username').value;
     const content = document.getElementById('content').value;

     const response = await fetch('/posts', {
       method: 'POST',
       headers: {
         'Content-Type': 'application/json',
       },
       body: JSON.stringify({ username, content }),
     });

     if (response.ok) {
       document.getElementById('username').value = '';
       document.getElementById('content').value = '';
       fetchPosts(); // Oppdater innleggene etter publisering
     }
   });

   // Kaller funksjonen for å vise innlegg når siden lastes
   fetchPosts();
   ```

Få en nærmere forklaring av denne koden her: [[Forklaring av koden for å håndtere innlegg i Twitter-klonen]]

---

### **Steg 6: Start Serveren og Test Applikasjonen**

1. I terminalen, **start serveren**:

   ```bash
   npm start
   ```

2. Åpne nettleseren og gå til `http://localhost:3000`.

3. **Test funksjonaliteten** ved å skrive et brukernavn og et innlegg i skjemaet, trykke på "Publiser", og se innleggene vises på siden.

---

### **Ekstra: Styling med CSS**

Hvis dere vil, kan dere lage enkel styling. Lag en `style.css`-fil i `public/stylesheets`-mappen og legg til noe enkel CSS:

```css
/* public/stylesheets/style.css */

body {
  font-family: Arial, sans-serif;
  margin: 20px;
}

h1 {
  color: #1DA1F2;
}

form {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin-bottom: 20px;
}

input, textarea, button {
  margin: 5px 0;
  padding: 10px;
}

#postsContainer {
  max-width: 500px;
}

#postsContainer div {
  border: 1px solid #ddd;
  padding: 10px;
  margin: 5px 0;
}
```

---

Nå har dere en fungerende Twitter-klone som kan lagre og vise innlegg – en flott måte å lære grunnleggende konsepter i Express.js og frontend-utvikling.