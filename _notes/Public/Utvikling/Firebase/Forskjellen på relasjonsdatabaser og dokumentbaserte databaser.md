---
title: Forskjellen på relasjonsdatabaser og dokumentbaserte databaser
feed: show
date: 04-04-2024
---
![En modell av en sky foran to liggende ringpermer fulle av papir. Foto.](https://api.ndla.no/image-api/raw/iJPaeTL4.jpg?width=1024)
[CC BY-NC](https://creativecommons.org/licenses/by-nc/4.0/deed.no)  **Bilde:** Andrey Popov

Tidligere har du kanskje lært å modellere relasjonsdatabaser og å kode dem i SQL. En viktig forskjell på relasjonsdatabaser (_SQL-baserte databaser_) og dokumentbaserte databaser (_NoSQL-databaser_) er at i dokumentbaserte databaser er det ingen forhåndsbestemte regler for hvordan databasen skal bygges opp. Hele databasen tar utgangspunkt i ei tekstfil (ofte ei .JSON-fil) der vi legger all dataene inn, uten å ha bestemt felt, rader og kolonner på forhånd. Vi skriver rett og slett bare all dataene inn i tekstfila. Dette gjør dokumentbaserte databaser veldig fleksible og enkle å sette opp, men det krever også mer orden fra dem som skal bruke databasen. For at en slik database skal være brukervennlig, krever det dessuten at programmet eller nettsiden vi bruker til å få tilgang til databasen, er satt opp på en måte som gjør det enklere å legge inn riktig data.

Vi kan likevel trekke ut noen likheter mellom relasjonsdatabaser (SQL) og dokumentbaserte databaser (NoSQL). En _tabell_ i SQL tilsvarer ei _samling_ (collection) i NoSQL, og en _rad_ (all dataene tilknyttet et objekt i databasen) i SQL tilsvarer et _dokument_ (document) i NoSQL. Du kan lese mer om oppbyggingen av dokumentbaserte databaser på [MongoDBs side "What is a Document Database"](https://www.mongodb.com/document-databases).

## Trenger vi datamodellering med dokumentbaserte databaser?

![En datamodell med seks firkanter. Noen av firkantene er koblet sammen med andre med linjer. Linjene har streker eller piler på endene. Inne i firkantene er det linjer som representerer tekst. Øverste tekstlinje i hver firkant har et nøkkelikon foran seg. Illustrasjon.](https://api.ndla.no/image-api/raw/x1jYWIh5.svg?width=1024)
*ER-modellering er en vanlig måte å modellere databaser på.*
[CC0](https://creativecommons.org/publicdomain/zero/1.0/deed.no) **Bilde**

Det kan kanskje være enkelt å tro at vi ikke trenger datamodellering i NoSQL-databaser, siden vi ikke trenger å opprette tabeller og felt på samme måte som i SQL, men det kan uansett være en god idé å ha oversikt over hvordan dataene skal organiseres i databasen. Derfor kan det være lurt å sette opp en datamodell også når du skal bruke NoSQL-databaser.

På bildet under ser du oppbyggingen av en Firestore-database med elevdata:  

![Modell av dokumentdatabase. Ei liste med ID-koder peker mot dokumenter med informasjon om forskjellige personer. Illustrasjon.](https://api.ndla.no/image-api/raw/WNSKXIE3.jpg?width=1024)

*Dokumentdatabaser er bygd opp av enkeltstående dokumenter som er gruppert i samlinger.*
**Bilde:** Karl Arne Dalsaune

Som du kan se på bildene, har noen av elevene ulik info. Noen har telefon, andre har e-post, og noen har begge deler. Dette ville ikke ha vært mulig i en SQL-database, der alle feltene må være opprettet på forhånd. Dette viser noe av fleksibiliteten i en NoSQL-database.