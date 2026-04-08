---
title: Firebase cheat sheet
feed: show
date: 07-04-2026
---
Denne guiden inneholder kjappe forklaringer på det du trenger for å komme igang med Firebase i [[React]] eller [[Vite-vanilla]].
## Innhold
- <a href="#en"> Hvordan setter jeg opp Firebase i web-prosjektet mitt?</a>
- <a href="#to">Hvordan legger jeg inn data i Firebase-databasen min?</a>
- <a href="#tre">Hvordan henter jeg data fra databasen og viser det på nettsiden min?</a>



<h2 id="en"> Hvordan setter jeg opp Firebase i web-prosjektet mitt?</h2>

For et Vite-prosjekt (React eller Vanilla) må du først installere Firebase i prosjektet ditt med npm:

```shell
npm firebase
```

Så må du hente ut Firebase-konfigasjonen din slik:
1. Gå til [firebase.google.com](https://firebase.google.com/)
2. Opprett et prosjekt hvis du ikke har, eller gå inn på prosjektet ditt
3. Gå inn på *Settings* og scroll ned til du ser en kode som ser slik ut:

```js
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "_API_KEY_",
  authDomain: "_PROJECT_ID_.firebaseapp.com",
  projectId: "_PROJECT_ID_",
  storageBucket: "_PROJECT_ID_.appspot.com",
  messagingSenderId: "_SENDER_ID_",
  appId: "_APP_ID_",
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
```

4. Kopier denne koden.
5. Opprett en ny fil i prosjektet ditt som du kaller *firebaseConfig.js*
6. Lim inn koden.
7. Legg til denne koden på slutten av fila:

```js
import { getFirestore } from "firebase/firestore";
const db = getFirestore(app);
export { db };
```

I alle filene der du skal bruke Firebase legger du inn denne koden øverst i fila:
```js
import { db } from "./firebaseConfig.js"
```



<h2 id="to">Hvordan legger jeg inn data i Firebase-databasen min?</h2> 

Det går an å legge inn data i databasen via Firebase-konsollen, men det er litt upraktisk og tidkrevende. Den enkleste måten er å opprette en fil som du kaller *populateDatabase.js*. I denne filen legger du inn kode for å sende data til databasen.

Funksjonen vi bruker for å sende data til databasen heter *addDoc*. I addDoc må vi også angi hvilken samling (*collection*) dokumentet (dataen) skal lagres i.

Her er et eksempel fra en database med hotellrom, der vi lagrer dokumentene i samlingen "hotelrooms":

```js
// populateDatabase.js

import { db } from "./firebaseConfig.js";
import { collection, addDoc } from "firebase/firestore";

addDoc(collection(db, "hotelrooms"), {
    floor: 1,
    roomNumber: 101,
    roomType: "single",
    noOfBeds: 1,
    price: 1000,
    hasBalcony: true,
    hasSeaView: false,
    description: "Cozy room with city view",
    isAvailable: true
})
  
addDoc(collection(db, "hotelrooms"), {
    floor: 1,
    roomNumber: 102,
    roomType: "double",
    noOfBeds: 2,
    price: 1500,
    hasBalcony: true,
    hasSeaView: false,
    description: "Cozy room with city view",
    isAvailable: true
})
  
addDoc(collection(db, "hotelrooms"), {
    floor: 1,
    roomNumber: 201,
    roomType: "suite",
    noOfBeds: 4,
    price: 2000,
    hasBalcony: true,
    hasSeaView: true,
    description: "Spacious suite with sea view",
    isAvailable: true
})
```

Denne fila skal **ikke** kobles til en HTML-fil eller en annen JS-fil, men skal kun kjøres en gang. For å kjøre den, åpner du terminalen og skriver:
```shell
node ./populateDatabase.js
```

Da sendes all informasjonen direkte til databasen. Når du har kjørt koden en gang kan det være lurt å kommentere ut alle kodelinjene, slik at det ikke går an å kjøre koden en gang til, da dette vil føre til duplikater i databasen. Merk koden og hold inn <kbd>Ctrl</kbd> og trykk <kbd>K</kbd> og så <kbd>C</kbd> for å kommentere ut koden.


<h2 id="tre">Hvordan henter jeg data fra databasen og viser det på nettsiden min?</h2>

For å hente data fra databasen bruker vi *getDocs*-metoden i Firebase. Denne henter ut et *snapshot* fra databasen, som inneholder all data fra den valgte somlingen på det tidspunktet vi ber om denne (siden data i en database forandrer seg hele tiden). Snapshot er et spesielt objekt i Firebase-biblioteket som ligner på en liste. For å gjøre det enklere å forstå, kan vi gjøre om snapshotet til en liste før vi fortsetter å jobbe med det.

Slik fungerer det (husk å importere *getDocs* øverst i js-fila di):
```js
import { getDocs, collection } from "firebase/firestore";

const snapshot = await getDocs(collection(db, "hotelrooms"));
const hotelrooms = snapshot.docs; // Vi gjør om snapshotet til en vanlig liste
```

Da har vi en liste med all dataen fra samlingen "hotelrooms". For å få ut spesifikk informasjon må vi gå gjennom lista med en forEach-løkke og hente ut enkeltdata slik:

```js
hotelrooms.forEach((room) => {
  console.log(room.data().roomNumber, room.data().roomType)
})
```

Denne koden vil skrive ut romnummer og romtype for alle hotellrommene i databasen.

### Pro-tip: Slipp å bruke .data() hver gang

Hvis du vil slippe å skrive `.data()` hver gang du skal bruke informasjonen, kan du transformere listen med en gang du har hentet den. Dette gjør vi med `.map()`-metoden. Da lager vi en ren liste med objekter som inneholder akkurat det vi trenger:

```js
const snapshot = await getDocs(collection(db, "hotelrooms"));

const hotelrooms = snapshot.docs.map((room) => {
    return {
        id: doc.id,       // Vi tar med ID-en i tilfelle vi trenger den senere
        ...doc.data()     // Vi "sprer" alle feltene fra data() inn i objektet
    };
});

// Nå kan vi bruke listen helt uten .data()!
hotelrooms.forEach((room) => {
    console.log(room.roomNumber, room.roomType);
});
```

---
#### SIDEBAR: .map()-metoden vs .forEach()-metoden
*`.map()` og `.forEach()` er to arraymetoder (metoder som brukes på lister) i JavaScript som ligner på hverandre. Begge kjører en funksjon på alle elementene i en liste, men forskjellen er at `.map()` returnerer en ny liste, mens `.forEach()` ikke returnerer noen ting.* 

*`.map()` brukes dermed når vi vil gjøre om eller transformere dataen i en liste, mens `.forEach()` brukes når vi skal gå gjennom lista og gjøre en handling for hvert element.*

---
### Vise databaseinnholdet på nettsiden

Hvis jeg vil vise det på nettsiden kan jeg gjøre det slik i Vite-vanilla:
```js
const app = document.querySelector("#app");
  
hotelrooms.forEach((room) => {
  app.innerHTML += `${room.roomNumber} - ${room.roomType} <br>`
})
```

*Merk at her bruker vi [Template Literals](https://www.w3schools.com/js/js_string_templates.asp) (backticks) for å kunne bruke JavaScript-logikk inne i en tekststreng, med bruk av \` \` og `${...}` for å legge variabler rett inn i teksten.*

Her er hele koden for å hente data og skrive den ut på nettsiden:

```js
// main.js

import './style.css'
import { db } from "./firebaseConfig.js";
import { getDocs, collection, query, where, orderBy } from "firebase/firestore";

const app = document.querySelector("#app");

const snapshot = await getDocs(collection(db, "hotelrooms"));

const hotelrooms = snapshot.docs.map((room) => {
    return {
        id: room.id,       
        ...room.data()     
    };
});
  
hotelrooms.forEach((room) => {
  app.innerHTML += `${room.roomNumber} - ${room.roomType} <br>`
})
```

I `app.innerHTML` kan jeg legge inn mer avansert HTML. For eksempel kan jeg legge infoen inn i en tabell, slik:

```js
let tableHTML = `
  <table>
    <tr>
      <th>Room number</th>
      <th>Room Type</th>
      <th># of beds</th>
    </tr>
`
  
hotelrooms.forEach((room) => {
  tableHTML += `
  <tr>
    <td>${room.roomNumber}</td>
    <td>${room.roomType}</td>
    <td>${room.noOfBeds}</td>
  </tr>
  `
})

tableHTML += `</table>`
  
app.innerHTML = tableHTML;
```
