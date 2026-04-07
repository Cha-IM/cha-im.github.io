---
title: Firebase cheat sheet
feed: show
date: 07-04-2026
---
Denne guiden inneholder kjappe forklaringer på det du trenger for å komme igang med Firebase i [[React]] eller [[Vite-vanilla]].
## Innhold
[[#Hvordan setter jeg opp Firebase i web-prosjektet mitt?]]
[[#Hvordan legger jeg inn data i Firebase-databasen min?]]

## Hvordan setter jeg opp Firebase i web-prosjektet mitt?

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

## Hvordan legger jeg inn data i Firebase-databasen min?

Det går an å legge inn data i databasen via Firebase-konsollen, men det er litt upraktisk og tidkrevende. Den enkleste måten er å opprette en fil som du kaller *populateDatabase.js*. I denne filen legger du inn kode for å sende data til databasen.

Funksjonen vi bruker for å sende data til databasen heter *addDoc*. I addDoc må vi også angi hvilken samling (*collection*) dokumentet (dataen) skal lagres i.

Her er et eksempel fra en database med hotellrom, der vi lagrer dokumentene i samlingen "hotelrooms":

```js
import { collection, addDoc } from "firebase/firestore";
import { db } from "./firebaseConfig.js";

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

Da sendes all informasjonen direkte til databasen.

## Hvordan henter jeg data fra databasen og viser det på nettsiden min?

For å hente data fra databasen bruker vi *getDocs*-metoden i Firebase. Denne henter ut et *snapshot* fra databasen, som inneholder en liste med all data fra databasen på det tidspunktet vi ber om denne (siden data i en database forandrer seg hele tiden).

Slik fungerer det:
```js
const snapshot = await getDocs(collection(db, "hotelrooms"));
```

Denne henter ut all info fra samlingen "hotelrooms". For å få ut spesifikk informasjon må vi gå gjennom lista med en forEach-løkke og hente ut enkeltinfo slik:

```js
snapshot.forEach((doc) => {
  console.log(doc.data().roomNumber, doc.data().roomType)
})
```

Denne koden vil skrive ut romnummer og romtype for alle hotellrommene i databasen.

### Vise databaseinnholdet på nettsiden

Hvis jeg vil vise det på nettsiden kan jeg gjøre det slik i Vite-vanilla:
```js
const app = document.querySelector("#app");
  
snapshot.forEach((doc) => {
  app.innerHTML += `${doc.data().roomNumber} - ${doc.data().roomType} <br>`
})
```

Merk at her bruker vi [Template Literals](https://www.w3schools.com/js/js_string_templates.asp) (backticks) for å kunne bruke JavaScript-logikk inne i en tekststreng, med bruk av \` \` og `${...}` for å legge variabler rett inn i teksten.