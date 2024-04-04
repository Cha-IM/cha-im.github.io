---
title: Oppsett av Firebase og Cloud Firestore
feed: show
date: 02-04-2024
---
**Firebase er et produkt fra Google som gjør det enkelt å koble en database til en nettside eller app, slik at man kan lagre info og innstillinger over lengre tid. I denne guiden vil du lære et basisoppsett av Firebase-databasen Cloud Firestore. Det skal du bruke videre i denne modulen.**

## Kom i gang med Firebase
For å bruke Firebase må du ha en Google-konto. Gå til [firebase.google.com](https://firebase.google.com/) og logg på med brukernavn og passord ved å trykke på "Logg på" øverst i høyre hjørne, hvis du ikke allerede er innlogget. Når du har logget inn, trykker du på "Get started" eller "Go to console" for å komme i gang med Firebase.

### Opprett et nytt prosjekt
![Firebase-konsollen, med overskriften "Welcome to Firebase!". Skjermbilde.](https://api.ndla.no/image-api/raw/0mJUNA6M.png?width=1024)
	*Opprett et prosjekt i Firebase*
	**Bilde:** Google

Du skal nå opprette et nytt prosjekt. Trykk på "Create a project", og følg instruksjonene. Det er tre steg:

1. Gi prosjektet ditt et navn. I dette første prosjektet skal vi lage en app for å registrere elever, så du kan gjerne kalle prosjektet ditt _Elevliste_.
    
    I dette steget må du huske å huke av på "I accept the Firebase Terms" og "I confirm that I will use Firebase exclusively for purposes relating to my trade, business, craft or profession".
    
2. Angi om prosjektet ditt skal bruke Google Analytics. Det er ikke nødvendig i dette prosjektet, så du kan slå dette av ved å trykke på bryteren ved "Enable Google Analytics for this project", slik at den blir grå. Trykk deretter på "Create project".
    
    Google Analytics brukes til å analysere bruk og besøk til nettsiden eller appen din.
    
3. Du vil få beskjeden "Your new project is ready". Du har nå opprettet prosjektet ditt. Trykk på "Continue" for å gå til prosjektsiden.
    

### Legg til en webapp
![Prosjektoversikten Elevliste i Firebase. Skjermbilde.](https://api.ndla.no/image-api/raw/MqFeVHhV.png?width=1024)
	*Dette er konsollen for Firebase-prosjektet ditt.*
	**Bilde:** Google

Du skal nå legge til en app i prosjektet ditt. Siden vi skal lage en webside, eller webapp, trykker du på symbolet \</> over teksten "Add an app to get started". Først må du gi appen din et navn. Gi appen din navnet _Elevliste-web_. Dette navnet brukes bare internt i Firebase-konsollen for å skille forskjellige apper fra hverandre, så det er ikke viktig at navnet er unikt og spennende. Trykk på "Register app".

Du får nå opp koden som du skal bruke for å koble Firebase til nettsiden din. Denne koden kalles SDK (Software Development Kit), og den inneholder all informasjon nettsiden ditt trenger for å kunne kommunisere med Firebase. Trykk på "Use a \<script> tag" for å få opp riktig kode (vi skal ikke bruke npm i denne guiden). Kopier ut koden fra Firebase ved å trykke på de to overlappende firkantene nederst til høyre i kodefeltet. NB: Ikke trykk deg videre ennå.

![SDK-koden til prosjektet. Skjermbilde.](https://api.ndla.no/image-api/raw/udsEGAZY.png?width=1024)
	*Dette er SDK-koden til Firebase-prosjektet, som du kan lime inn i ei HTML-fil. Ditt prosjekt vil ha forskjellige koder og adresser.*
	**Bilde:** Google

Nå skal du sette denne koden inn i en JavaScript-fil som du kan bruke til å hente inn Firebase-konfigurasjonen din på alle nettsider som skal bruke denne databasen:
1. Åpne en kodeeditor, for eksempel Visual Studio Code, og opprett ei ny mappe som du kaller _Elevliste_ (i VS Code: "Open folder" og så "Ny mappe"). 
2. I denne mappa oppretter du ei ny fil som du kaller _firebase.js_. 
3. Lim du inn koden du fikk fra Firebase, men ta bort `<script>`-taggene på første og siste linje. 
	Husk at denne koden er unik for deg, så deler av koden din vil være ulik skjermbildet over.
4. Lagre fila, men la den være åpen, da vi skal legge inn mer kode i den i neste steg.

Nå kan du gå tilbake til Firebase og trykke på "Continue to console".

Hvis du trenger å finne igjen denne koden (SDK) senere, finner du den igjen i "Project settings".
### Legg til en Firestore-database
![Firebase-konsollen. Man kan legge til et produkt i appen. Det ene er "Authenticiation", det andre er "Cloud Firestore". Skjermbilde.](https://api.ndla.no/image-api/raw/mnRahZmf.png?width=1024)
	*Når du har opprettet en app i Firebase, kan du legge til funksjonaliteten du trenger.*
	**Bilde:** Google

Du skal nå legge til Cloud Firestore i prosjektet ditt. Trykk på "Cloud Firestore", og trykk deretter på "Create database". Du må nå gjøre to valg:

1. Hvor skal databasen din lagres? Her velger du "eur3" (europe-west). Da vil databasen din bli lagret i Vest-Europa, noe som er en fordel, både fordi det er fysisk nært Norge, og fordi landene i Vest-Europa følger EUs personverndirektiv GDPR, som er det samme direktivet som vi følger i Norge.
    
2. Hvem skal ha lese- og skriverettigheter til databasen din? For enkelthets skyld velger vi "Start in test mode", som gir både lese- og skrivetilgang til alle som har tilgang på koden til databasen din, for eksempel via nettsiden din. Dette kan du endre senere, og du må endre det innen 30 dager.
    

Nå har du opprettet databasen din.

![Databasen, delt inn i to felt. Det venstre feltet har overskriften "Elevliste", og i det til høyre står det "Your database is ready to go. Just add data". Skjermbilde.](https://api.ndla.no/image-api/raw/Ymx6MngY.png?width=1024)
	*Slik ser databasen ut før du har lagt inn noe data.*
	**Bilde:** Google

Du kan legge inn data i databasen direkte om du ønsker det. Firestore er en dokumentbasert database, eller NoSQL-database. Denne typen database er mye mindre streng på hva slags data som kan lagres i databasen. Man lager ikke tabeller, felt og datatyper på forhånd, som i SQL, men man legger data inn direkte som objekter (dokumenter). Metadata legges inn på hvert dokument individuelt, slik at hvert dokument kan ha forskjellig data og metadata. Man er derfor mer avhengig av hvordan appen som kommuniserer med databasen, er bygd opp for å få en oversiktlig database.
## Legg inn databasen i scriptet ditt
Nå som du har opprettet databasen, må du legge inn databasen i scriptet du lagde tidligere. Åpne Visual Studio Code igjen. I koden du kopierte inn tidligere, skal du nå legge til noen linjer.

Du skal legge til to kodelinjer:

1. Under `//` `TODO: Add SDKs for Firebase products that you want to use` (linje 3), legger du inn denne koden (kopier linja under og lim den inn i HTML-dokumentet ditt):
```javascript
import { getFirestore } from "https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore.js"
//NB: Pass på at versjonsnummeret i URL-en (9.6.1) er det samme som versjonsnummeret fra koden du kopierte da du satte opp webappen din (f.eks. 10.0.1).
```

2. Nederst i scriptet legger du inn denne koden (kopier linja under og lim den inn i HTML-dokumentet ditt)
```javascript
const db = getFirestore();

export { db };
```

### Kontroller koden din
Sjekk at koden din er lik som koden under, men med dine unike verdier under `firebaseConfig`.

#### firebase.js
```javascript
// Import the functions you need from the SDKs you need
import { initializeApp } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-app.js";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries
import { getFirestore } from "https://www.gstatic.com/firebasejs/9.6.3/firebase-firestore.js"

// Your web app's Firebase configuration
// NB! HER KOMMER DINE UNIKE KODER
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

const db = getFirestore();

export { db };
```

For å bruke databasen din, og hente og legge inn data, oppretter du et nytt script og importerer databasen din slik i starten av koden:

```javascript
import { db } from "./firebase.js"
// "./firebase.js" angir at firebase.js ligger i samme mappe som denne scriptfilen.
```
