---
title: Legge inn data i en Firebase-database
feed: show
date: 04-04-2024
---
**I NoSQL-databaser organiseres data i _samlinger_ som består av flere _dokumenter_. I denne artikkelen skal du lære to metoder for å opprette dokumenter i Cloud Firestore.**

![Modell av dokumentdatabase. Ei liste med ID-koder peker mot dokumenter med informasjon om forskjellige personer. Illustrasjon.](https://api.ndla.no/image-api/raw/WNSKXIE3.jpg?width=1024)
**Bilde:** Karl Arne Dalsaune

## Legge inn data i databasen

Du skal nå legge inn dataene fra bildet over i Firebase-databasen din. Lag en ny fil i samme mappe som du lagde *firebaseconfig.js* i forrige leksjon. Kall fila *legginndata.js*. Øverst i fila skriver du

```js
import { db } from "./firebaseconfig.js"
```


## Opprette et nytt dokument i databasen

Du skal nå skrive kode for å opprette et nytt dokument i databasen. Den enkleste måten å gjøre dette på er å bruke Firestore-funksjonene `addDoc()` og `collection()`. Dokumenter som opprettes med `addDoc()` får automatisk en unik ID, så du trenger ikke tenke på at dokumentet må ha en primærnøkkel.

### async/await
En viktig ting med funksjonene som er knyttet til Firestore, er at de er _asynkrone_. Det vil si at når en databaseoperasjon skal kjøre, vil programmet fortsette å kjøre neste kodelinje uten å vente på at kommunikasjonen med databasen er fullført. Derfor skriver vi ordet `await` foran disse funksjonene, slik at programmet venter til kommunikasjonen med databasen er fullført før neste kodelinje kjøres.

### addDoc()
`addDoc()` er en funksjon for å skrive data til databasen. Denne funksjonen tar inn to parametere: hvilken samling (collection) dataene skal skrives til, og hvilken data som skal skrives, slik:

```js
addDoc(_COLLECTION_, _DATA_);
```

Dataene skrives inn på formen

```js
{
	_FELTNAVN_1_: "_DATA_1_",
	_FELTNAVN_2_: "_DATA_2_"
}
```

`collection()` brukes inne i `addDoc()` for å angi hvilken database som skal brukes, og hvilken samling (_collection_) inne i databasen dataene skal skrives til. En samling i dokumentbaserte databaser tilsvarer som sagt omtrent en tabell i relasjonsdatabaser, og et dokument tilsvarer en rad. Koden for å lage en referanse til en elev blir derfor slik:

```js
collection(_DATABASE_, "_NAVN_PÅ_COLLECTION_");
```


## Husk å importere **Firebase****-funksjonene

Alle funksjonene du bruker som er spesielle for Firebase, og ikke generelle JavaScript-funksjoner, må importeres. Vi har allerede importert `initializeApp` fra _(...)/__firebase__-app.js_ og `getFirestore` fra _(...)/__firebase__-__firestore__.js_ i koden over. Når vi skal skrive kode videre, må vi huske å importere alle funksjoner vi ikke har brukt før fra _(...)/__firebase__-__firestore__.js_. For å bruke `addDoc()` og `collection()` må vi derfor importere dem øverst i js-filen, slik

```js
import { addDoc, collection} from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js"
//Husk å endre versjonsnummer til den versjonen av Firebase du har angitt i firebaseconfig.js
```

Foran hvert kodeeksempel videre i teksten er det lagt inn en kommentar med hvilke funksjoner som må importeres for at koden skal fungere.

### Legge inn en elev med addDoc()

Nå er du klar til å legge inn den første eleven i databasen. Skriv koden under nederst i scriptet ditt. Husk å skrive `await` foran funksjonen som starter kommunikasjon med databasen.

```js
// import { addDoc, collection } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

// Lager et nytt dokument i samlinga "elever"
await addDoc(
  collection(db, "elever"), {
    fornavn: "Rebecca",
    etternavn: "Thomasen",
    telefon: "12345678"
});
```

Lagre HTML-dokumentet og åpne det i en nettleser. Åpne inspiser-verktøyet for å sjekke at du ikke har noen feilmeldinger i konsollen, og se på Firestore-databasen din. Nå skal du finne et nytt dokument med dataene du la inn.

![Database i Cloud Firestore. Tre felt: et med overskriften "elevliste", et med overskriften "elever" og et der man får opp navnet og telefonnummeret til eleven Rebecca Thomasen. Skjermbilde.](https://api.ndla.no/image-api/raw/bNZI1wKp.png?width=1024)

*Dokumentet for eleven Rebecca Thomasen ligger i samlinga "elever".*
**Bilde:** Google

## Opprette et nytt dokument i databasen med egendefinert ID

`setDoc()` er en annen måte å opprette nye dokumenter i databasen på. `setDoc()` gir deg muligheten til å definere en egen primærnøkkel for hvert dokument i databasen, slik at du kan bruke for eksempel brukernavn, e-post eller en egendefinert ID (elev-ID, kundenummer) som primærnøkkel. `setDoc()` brukes i kombinasjon med `doc()` for å angi hvor dokumentet skal lagres i databasen, og hva som skal være primærnøkkelen.

### setDoc()
`setDoc()` er en funksjon for å skrive data til en spesifikk ID i databasen. Denne funksjonen tar inn to parametere: hvilket _dokument_ dataene skal skrives til (angitt med ID), og hvilken data som skal skrives, slik:

```js
setDoc(_DOCUMENT_, _DATA_);
```

Dataene skrives inn på formen

```js
{
	_FELTNAVN_1_: "_DATA_1_",
	_FELTNAVN_2_: "_DATA_2_"
}
```

`doc()` brukes inne i `setDoc()`, for å angi hvilken database som skal brukes, hvilken samling (collection) inne i databasen dataene skal skrives til, og hvilken ID dokumentet skal ha. Koden for å lage en referanse til en elev blir derfor slik:

```js
doc(_DATABASE_, "_NAVN_PÅ_COLLECTION_", "_ID_");
```

Merk at ID-en alltid må være definert som tekst, med anførselstegn. Hvis du ønsker å bruke nummer som ID, må du derfor også skrive tallet i anførselstegn, slik: `"3"`.

### Legge inn en elev med setDoc()

Nå er du klar til å legge inn en ny elev med egendefinert ID i databasen. Som ID velger vi å lage et brukernavn med de første bokstavene i etternavnet og de to første bokstavene i fornavnet. Importer funksjonene `setDoc` og `doc` fra _(...)/__firebase__-__firestore__.js_, og skriv koden under nederst i scriptet ditt. Husk å skrive `await` foran funksjonen som starter kommunikasjon med databasen.

```js
// import { setDoc, doc } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

// Lager et nytt dokument i samlinga "elever"
await setDoc(
  doc(db, "elever", "nilja"), {
    fornavn: "Jakob",
    etternavn: "Nilsen",
    epost: "jakob@nilsen.net"
  });
```

### Sende data til Firebase-databasen
For å sende dataen du har lagt inn i .js-fila til Firebase-databasen din, må koden kjøres i nettleseren. For å gjøre dette må du opprette en .html-fil. Opprett en ny fil i samme mappe som .js-filene dine som du kaller index.html. Legg inn nødvendig kode for å lage en webside (`<html>`, `<head>`, `<body>`). Du kan taste inn **!** (utropstegn) og trykke på enter for å få de nødvendige taggene automatisk i VS Code.

Inne i `<body>`-taggen legger du inn *legginndata.js* i en `<script>`-tag med `type=module`, slik:

```html
<script type="module" src="legglegginndata.js"></script>
```

Lagre HTML-dokumentet og åpne det i en nettleser. Åpne inspiser-verktøyet for å sjekke at du ikke har noen feilmeldinger i konsollen, og se på Firestore-databasen din. Nå skal du finne et nytt dokument med dataene du la inn. Legg merke til at ID-en til dokumentet er det samme som vi anga i koden ("nilja").

![Database i Cloud Firestore. Tre felt: et med overskriften "elevliste", et med overskriften "elever", der brukernavnet nilja ligger, og et med overskriften "nilja" der man får opp navnet og e-posten til eleven Jakob Nilsen. Skjermbilde.](https://api.ndla.no/image-api/raw/vFLRSMo2.png?width=1024)

*Dokumentet for eleven Jakob Nilsen har egendefinert ID.*
**Bilde:** Google


# NESTE LEKSJON 
➡️ [[Endre og slette dokumenter i databasen]]