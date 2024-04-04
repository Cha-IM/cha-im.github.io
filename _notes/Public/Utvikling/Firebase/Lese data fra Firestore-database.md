---
title: Lese data fra Firestore-database
feed: show
date: 04-04-2024
---
**Når vi skal hente data fra Cloud Firestore, kan vi hente ut ett enkelt dokument eller alle dokumentene i ei samling. Vi kan også bruke spørringer for å hente utvalgte dokumenter som oppfyller en eller flere betingelser.**

I leksjonen [[Legge inn data i en Firebase-database]] lærte du hvordan du legger inn data i databasen. I denne artikkelen skal du lære hvordan du henter data ut fra databasen og lager spørringer for å velge hvilke data du vil hente ut.

I denne leksjonen skal du bruke følgende Firebase-funksjoner:
```js
{ collection, doc, addDoc, setDoc, getDoc, getDocs, query, where, orderBy }
````

Pass på å importere disse fra _(...)/firebase-firestore.js_ i koden din.

For at du skal kunne ha data å jobbe med, kan du kopiere koden under til skriptet ditt for å legge inn fire elever i databasen din:

```js
//Importerer Firebase-funksjonene vi trenger
import { setDoc, doc } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

//Legger inn fire elever i databasen
await setDoc(
  doc(db, "elever", "thore"), {
    fornavn: "Rebecca",
    etternavn: "Thomasen",
    telefon: "12345678"
});
await setDoc(
  doc(db, "elever", "nilja"), {
    fornavn: "Jakob",
    etternavn: "Nilsen",
    epost: "jakob@nilsen.net"
});
await setDoc(
  doc(db, "elever", "moisa"), {
    fornavn: "Isa",
    etternavn: "Mo",
    epost: "isamo@mo.no",
    telefon: "23456789"
});
await setDoc(
  doc(db, "elever", "marga"), {
    fornavn: "Gabrielle",
    etternavn: "Martin",
    telefon: "45678901"
});
```

## Lese data fra databasen

I likhet med at det finnes flere måter å skrive data til databasen på, finnes det også flere måter å lese fra databasen på. De enkleste er `getDoc()` og `getDocs()`.

### Hente ut ett dokument fra databasen med getDoc()

`getDoc()` brukes til å hente ut enkeltdokumenter fra databasen og krever at du vet ID-en til dokumentet du skal hente. I likhet med `setDoc()` bruker `getDoc()` funksjonen `doc()` for å angi hvilket dokument som skal hentes ut. `getDoc()` returnerer et databaseobjekt, og derfor må du opprette en variabel for å lagre dataene som hentes ut.

Koden for å hente ut dokumentet vi lagde for eleven Jakob Nilsen, blir slik:

```js
// import { getDoc, doc } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

const doc = await getDoc(
  doc(db, "elever", "nilja")
);
console.log(
  "Document data:", 
  doc.data()
);
```

Merk at vi skriver `await` foran `getDoc()` for å sørge for at neste linje i koden ikke kjøres før kommunikasjonen med databasen er ferdig.

Resultatet blir skrevet ut slik i konsollen:

```shell
Document data:
>{fornavn: 'Jakob', etternavn: 'Nilsen', epost: 'jakob@nilsen.net'}
```


![Konsoll i nettleser med utskrift av elevdata fra Firestore. Skjermbilde.](https://api.ndla.no/image-api/raw/JhN44iQa.png?width=1024)
*Slik ser utskriften ut i "Inspiser"-vinduet til nettleseren.* **Bilde:** Google Chrome

### Hente ut enkeltdata
Når vi henter ut data fra databasen, kaller vi det vi henter ut et "snapshot", for det representerer et øyeblikksbilde av dataene i det øyeblikket vi henter dem ut fra databasen. `const doc` i koden over representerer et øyeblikksbilde av ett dokument i databasen (doc er her bare et variabelnavn og kan i utgangspunktet være hva som helst, men dette er et eksempel på et beskrivende variabelnavn). `doc.data()` henter ut alle dataene som er lagret i dokumentet og presenterer dem som et objekt. Om du vil hente ut enkeltdata, kan du angi det slik:

```js
console.log(
  "ID:", 
  doc.id,
  "Navn:", 
  doc.data().fornavn, 
  doc.data().etternavn
); 
```
Prøv å lime inn disse linjene i koden din og se hva som blir skrevet ut i konsollen.

### Hente ut alle dokumentene i ei samling med getDocs()

`getDocs()` brukes for å hente ut flere dokumenter på en gang fra databasen. Det kan være enten alle dokumentene i ei samling eller et utvalg basert på gitte kriterier (query). `getDocs()` returnerer ei liste (array) med databaseobjekter.

For å hente ut alle dokumentene i ei samling bruker vi `collection()` inne i `getDocs()` for å angi hvilken samling vi skal hente dokumentene fra. For å hente ut alle dokumentene i elevlista blir koden slik:

```js
// import { getDocs, collection } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

const snapshot = await getDocs(
  collection(db, "elever")
);

snapshot.forEach((doc) => {
  console.log(
    doc.data().fornavn, 
    doc.data().etternavn
  );
}); 
```

`snapshot.forEach()` er ei løkke som kjører en gang for hvert dokument (`docSnap`) i samlinga. I eksempelet skriver denne løkka ut fornavn og etternavn til alle elevene til konsollen:

![Konsollen i nettleseren med utskrift fra Firestore. Foto.](https://api.ndla.no/image-api/raw/fwUaBajb.png?width=1024)

*Utskrift av fornavn og etternavn til alle elever i databasen* **Bilde:** Google
