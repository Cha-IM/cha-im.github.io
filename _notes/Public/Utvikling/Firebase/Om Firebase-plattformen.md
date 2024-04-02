---
title: Om Firebase-plattformen
feed: show
date: 02-04-2024
---
[Firebase (firebase.google.com)](https://firebase.google.com/) er en plattform for å utvikle mobil- og webapplikasjoner som er utviklet av Google. Den opprinnelige ideen bak Firebase var å legge til rette for synkronisering av data mellom web- og mobilapplikasjoner på en enkel måte. Databasen er derfor en viktig del av Firebase. Firebase tilbyr to databasesystemer: Firebase Realtime Database, som er det første produktet som ble lansert av Firebase, og Cloud Firestore, som er en videreføring av Realtime Database med en del oppgraderinger. Begge databasesystemene støttes av Google, men i denne guiden bruker vi Cloud Firestore. Begge databasesystemene er NoSQL-databaser.

I tillegg til database tilbyr også Firebase flere andre funksjoner, som autentisering av brukere, lagring av filer med mer. Firebase kan brukes gratis, men det er begrensninger på hvor mye data som kan lagres, og hvor mye trafikk som går til og fra databasen. For skoleprosjekter holder gratisversjonen fint, men for kommersielle prosjekter vil man sannsynligvis trenge mer. Man betaler da ut fra hvor mye data som er brukt. Om du vil vite mer om kostnadene for Firebase, kan du lese på nettsidene til Firebase: [Firebase pricing (firebase.google.com)](https://firebase.google.com/pricing)

En fordel med Firebase er at du ikke trenger en egen databaseserver for å lagre data, og da trenger du heller ikke bruke noe serversidespråk for å kommunisere med databasen, slik du trenger i for eksempel MySQL eller MongoDB. Firebase støtter mange programmeringsspråk, som JavaScript, Python, Java, C++, C#, Go, Swift og Objective-C og flere. I denne guiden bruker vi JavaScript.