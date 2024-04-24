For å holde Firebase-koden din ryddig kan det lønne seg å dele opp de ulike Firebase-operasjonene i forskjellige js-filer. Her er et forslag til hvordan du kan organisere dette:

## firebaseconfig.js
Her legger du inn Firebase-konfigurasjonen din som du har fått fra Firebase-konsollen. Nederst i koden eksporterer du databasen din, slik at den kan brukes i andre js-filer:
```js
export { db }
```

## populateDatabase.js
Her legger du inn koden for å legge inn data i databasen din. Siden denne koden trenger bare å kjøres en gang, er det lurt å ha det i en egen fil, slik at du slipper at data blir lagret dobbelt hver gang du skal kjøre resten av k