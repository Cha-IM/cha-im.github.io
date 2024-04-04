---
title: Endre og slette dokumenter i databasen
feed: show
date: 04-04-2024
---
## Endre et dokument i databasen

Hvis du trenger å endre data i et dokument som allerede er lagret i databasen, kan du bruke funksjonen `updateDoc()`. Med `updateDoc()` kan du endre innholdet i felt i et dokument, eller du kan legge til nye felt. `updateDoc()` har samme syntaks (skrivemåte) som `setDoc()`:

```js
updateDoc(_DOCUMENT_, _DATA_);
```

Som med `setDoc()` bruker vi `doc()` for å hente ut dokumentet:

```js
updateDoc(doc(_DATABASE_, "_COLLECTION_", "_ID_"), { _FELTNAVN_: "_DATA_" });
```
Vi kan for eksempel endre etternavn og legge til telefonnummer til eleven Jakob Nilsen, som vi nettopp la til. Importer først funksjonen `updateDoc` fra _(...)/__firebase__-__firestore__.js,_ og skriv følgende kode nederst i scriptet ditt:

```js
// import { updateDoc, doc } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

// Endrer feltet "etternavn" i dokumentet og legger til feltet "telefon"
await updateDoc(
  doc(db, "elever", "nilja"), {
    etternavn: "Nilssen",
    telefon: "2233445"
});
```

Vi har nå endret etternavnet fra Nilsen (én S) til Nilssen (to S-er) og lagt til et telefonnummer. Alle andre felt forblir uendret.

### Slette et felt

Vi kan også bruke `updateDoc()` for å slette felt. Vi må da bruke funksjonen `deleteField()` inne i `updateDoc()`, slik:

```js
feltnavn: deleteField()
```

Vi kan se i databasen at e-posten til Jakob Nilssen fortsatt er med en S, så den er sannsynligvis feil. For å slette e-posten skriver du koden under. Husk å importere `deleteField()`.

```js
// import { updateDoc, doc, deleteField } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

// Sletter feltet "epost" fra dokumentet
await updateDoc(
  doc(db, "elever", "nilja"), {
    epost: deleteField()
});
```

Da vil hele e-postfeltet i dokumentet slettes.

## Slette et dokument

For å slette et helt dokument kan du bruke funksjonen `deleteDoc()`. Denne funksjonen har ganske lik skrivemåte som `setDoc()` og `updateDoc()`, men her trenger du ikke å angi noen felt siden alle skal slettes. For å slette et dokument trenger du å vite ID-en til dokumentet. For å slette eleven Jakob Nilssen fra databasen skriver du koden under. Husk å importere `deleteDoc()`.

```js
// import { deleteDoc, doc } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

// Sletter dokumentet med ID-en "nilja"
await deleteDoc(
  doc(db, "elever", "nilja")
);
```

Dokumentet er nå slettet fra databasen.


# NESTE LEKSJON
➡️ [[Lese data fra Firestore-database]]