---
title: Forklaring av koden for å håndtere innlegg i Twitter-klonen
feed: show
date: 29-10-2024
---

Her er en oppdelt gjennomgang av `app.js`-koden i JavaScript som håndterer innleggene i Twitter-klonen. Vi skal ta den steg for steg, med en forklaring på hver del, og også gå gjennom hvorfor og hvordan `async/await` brukes.

---

### **Introduksjon til `app.js`**

Denne filen (plassert i `public/javascripts/app.js`) håndterer klientsiden av applikasjonen, altså hvordan vi:
1. Henter og viser eksisterende innlegg.
2. Sender nye innlegg til serveren.

Her er hele koden i tre deler for en lettere gjennomgang:

---

### **Del 1: Hente og Vise Innlegg**

Første delen er funksjonen `fetchPosts()`. Den henter innleggene fra serveren og viser dem på siden.

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
```

**Forklaring linje for linje:**

1. `async function fetchPosts()` – Vi definerer `fetchPosts()` som en `async`-funksjon. Dette betyr at vi kan bruke `await` inne i denne funksjonen, som gjør koden enklere å lese når vi venter på data.
2. `const response = await fetch('/posts');` – Her bruker vi `fetch()` for å hente innlegg fra serveren. Ved å legge til `await` venter koden til vi får svar fra serveren før vi går videre.
3. `const posts = await response.json();` – Vi konverterer responsen til JSON-format (data vi kan bruke i JavaScript). `await` brukes for å vente på at JSON-parsingen fullføres.
4. `const postsContainer = document.getElementById('postsContainer');` – Henter HTML-elementet der innleggene skal vises.
5. `postsContainer.innerHTML = '';` – Fjerner eventuelle gamle innlegg før vi legger til de nyeste.
6. `posts.forEach(post => { ... })` – Går gjennom hvert innlegg og legger til HTML for å vise innlegget.
7. `postElement.innerHTML = ...` – Lager en `div` for hvert innlegg, med brukernavn, innhold, og tidsstempel, og legger dette inn i `postsContainer`.

---

### **Del 2: Legge til Et Nytt Innlegg**

Den andre delen er skjemaet som lar brukeren sende inn et nytt innlegg, og hvordan vi håndterer innsendingen med JavaScript.

```javascript
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
```

**Forklaring linje for linje:**

1. `document.getElementById('postForm').addEventListener('submit', async (e) => { ... });` – Vi legger til en hendelse (event listener) for skjemaet, som kjører funksjonen når brukeren trykker "Publiser".
2. `e.preventDefault();` – Hindrer at siden lastes inn på nytt når skjemaet sendes inn, slik at vi kan håndtere dataen direkte med JavaScript.
3. `const username = document.getElementById('username').value;` – Henter brukernavnet som brukeren skrev inn i feltet.
4. `const content = document.getElementById('content').value;` – Henter innholdet (selve tweeten) som brukeren skrev inn.
5. `const response = await fetch('/posts', { ... });` – Sender en `POST`-forespørsel til serveren med det nye innlegget. `await` brukes for å vente til serveren har mottatt og behandlet forespørselen.
   - `method: 'POST'` – Angir at vi skal sende data med `POST`.
   - `headers: { 'Content-Type': 'application/json' }` – Forteller serveren at dataene vi sender er i JSON-format.
   - `body: JSON.stringify({ username, content })` – Sender brukernavn og innhold som JSON.
6. `if (response.ok) { ... }` – Sjekker om serveren svarte med status `200 OK`, som betyr at innlegget ble lagret.
7. `fetchPosts();` – Etter et vellykket innlegg kaller vi `fetchPosts()` på nytt for å vise det nye innlegget på siden.

---

### **Del 3: Hente Innlegg Når Siden Lastes**

Til slutt kaller vi `fetchPosts()` når siden lastes, slik at vi alltid ser de nyeste innleggene:

```javascript
// Kaller funksjonen for å vise innlegg når siden lastes
fetchPosts();
```

Dette er enkelt, men viktig! Når nettsiden lastes, henter denne linjen alle innleggene fra serveren og viser dem.

---

### **Hvorfor Vi Bruker `async/await`**

I denne koden bruker vi `async/await` for å håndtere **asynkrone operasjoner**. `fetch()`-forespørsler til serveren er **asynkrone** fordi det tar litt tid å sende og motta data fra serveren. Uten `async/await` ville vi måtte bruke `.then()` for å håndtere disse operasjonene, som kan gjøre koden mer komplisert å lese og forstå.

**Hvordan fungerer `async/await`:**
- `async` markerer en funksjon som asynkron. Dette lar oss bruke `await` inni funksjonen.
- `await` sier "vent på dette til det er ferdig før vi fortsetter". Det gir oss mulighet til å skrive asynkron kode på en lineær, lettlest måte – som om koden kjører synkront.

---

### **Oppsummering**

Vi har nå sett hvordan vi kan dele opp koden i håndterbare deler:

1. **Hente innlegg fra serveren** og vise dem.
2. **Legge til nye innlegg** ved å sende data til serveren.
3. **Laste inn innlegg automatisk** når siden åpnes.

Dette gir oss en Twitter-lignende funksjonalitet på en enkel måte, samtidig som vi lærer viktige konsepter som asynkron programmering med `async/await`.
