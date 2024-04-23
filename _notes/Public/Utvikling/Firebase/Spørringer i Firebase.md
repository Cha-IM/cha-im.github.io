---
title: Spørringer i Firebase
feed: show
date: 23-04-2024
---
Spørringer er en måte å hente ut spesifikke dokumenter i en database som møter en betingelse, f.eks. "skriv ut alle personer over 18 år" eller "skriv ut alle jentene i databasen, sortert etter etternavn".
## Hente ut utvalgte dokumenter i ei samling med query()

Med `query()` kan vi lage spørringer mot databasen. En spørring er en betingelse for å filtrere, begrense eller sortere dataene som skrives ut. Dette fungerer i utgangspunktet på samme måte som i SQL. For eksempel kan vi hente ut bare elever som er registrert med e-post, eller vi kunne ha hentet ut bare elever som har matematikk som et av sine fag. For å lage en spørring kan vi bruke funksjonene `where()`, `orderBy()`, `startAt()`, `startAfter()`, `endAt()`, `limit()` eller `limitToLast()`.

For eksempel kan vi lage en spørring for å hente ut alle elever, sortert på etternavn:

```js
// import { collection, query, orderBy } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

query(
  collection(db, "elever"), 
  orderBy("etternavn")
);

```

Vi kan også lage en spørring for å bare hente ut elever som er registrert med e-post:

```js
// import { collection, query, where } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

query(
  collection(db, "elever"), 
  where("epost", "!=", "undefined")
);
```

Betingelsen `where("epost", "!=", "undefined")` betyr at e-post skal være ikke lik (`!=`) "undefined". Det vil si at spørringen utelukker elever som ikke har registrert e-post (`epost == undefined`).

Vi skal nå bruke denne spørringen opp mot databasen og skrive ut resultatet:

```js
// import { getDocs, collection, query, where } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js";

const querySet = await getDocs(
  query(
    collection(db, "elever"), 
    where("epost", "!=", "undefined")
  )
); // returnerer en liste med dokumenter som møter betingelsen, som lagres i listen/arrayen querySet

// Går gjennom alle dokumenter returnert av spørringen
querySet.forEach((docu) => {
  // Skriver ut data fra hvert av dokumentene til konsollen
  console.log(
    docu.data().fornavn, 
    docu.data().etternavn, 
    docu.data().epost
  );
});
```


`querySet.forEach()` skriver ut alle resultatene av spørringen i konsollen:

![Konsollen i nettleseren med utskrift fra Firestore. Foto.](https://api.ndla.no/image-api/raw/DK3dncOM.png?width=1024)

*Utskrift av navn og e-post til alle elever som har registrert e-post* [Begrenset bruk](https://ndla.no/nb/article/opphavsrett) **Bilde:** Google