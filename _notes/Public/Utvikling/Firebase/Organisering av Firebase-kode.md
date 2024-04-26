For å holde Firebase-koden din ryddig kan det lønne seg å dele opp de ulike Firebase-operasjonene i forskjellige js-filer. Her er et forslag til hvordan du kan organisere dette:

## firebaseconfig.js
Her legger du inn Firebase-konfigurasjonen din som du har fått fra Firebase-konsollen. Nederst i koden eksporterer du databasen din, slik at den kan brukes i andre js-filer:
```js
export { db }
```

## populateDatabase.js
Her legger du inn koden for å legge inn data i databasen din. Siden denne koden trenger bare å kjøres en gang, er det lurt å ha det i en egen fil, slik at du slipper at data blir lagret dobbelt hver gang du skal kjøre resten av koden. Etter at du har kjørt koden, og dataen er lagt inn i databasen, kan du enten kommentere ut koden i denne fila, eller du kan fjerne koblingen til denne fila fra nettsiden (html-fila som kjører koden)

Her er et eksempel på en slik kode:
```js
import { db } from "./firebaseConfig.js"
import { setDoc, doc } from "https://www.gstatic.com/firebasejs/10.11.0/firebase-firestore.js"

async function addRoom(roomNo, floor, roomType, noOfBeds, isAvailable){
	await setDoc(
		doc(db, "rooms", roomNo), {
			floor: floor,
			roomType: roomType,
			noOfBeds: noOfBeds,
			isAvailable: isAvailable
		}
	)
}

addRoom("101", 1, "single", 1, true);
addRoom("102", 1, "double", 2, true);
addRoom("201", 2, "suite", 5, false)
```

Dette kan også gjøres mer avansert, der populateDatabase.js inneholder funksjoner som tar inn dataen som tekst eller variabler, og legger dette inn i databasen. Da kan du opprette enda en .js-fil for rådataen, der du for eksempel lager en liste som eksporteres. Evt kan du legge inn rådataen som en .json-fil,