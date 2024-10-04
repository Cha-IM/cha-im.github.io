---
title: JavaScript Cheat Sheet
feed: show
date: 04-10-2024
---

---

**Hva er JavaScript?**  
JavaScript er et programmeringsspråk som gjør nettsider interaktive. Det brukes til alt fra å håndtere knappeklikk til å bygge komplekse webapplikasjoner.

---

### **1. Variabler**  
Variabler lagrer informasjon som kan brukes i koden.  
Eksempel:
```javascript
const navn = "Anna";
let alder = 18;
```
- `const`: brukes for verdier som ikke skal endres.
- `let`: brukes for verdier som kan endres senere.

---

### **2. Datatyper**  
Vanlige datatyper i JavaScript:
- **String**: tekst (f.eks. `"Hei"`)
- **Number**: tall (f.eks. `42`)
- **Boolean**: sant/usant (f.eks. `true`, `false`)

Eksempel:
```javascript
let tekst = "Hei, verden!";
let tall = 10;
let erLærer = true;
```

---

### **3. Funksjoner**  
Funksjoner utfører handlinger. To måter å definere funksjoner på:

**Funksjonsdeklarasjon**  
```javascript
function siHei() {
  console.log("Hei!");
}
siHei(); // Kaller på funksjonen
```

**Pilfunksjon** (arrow function)  
```javascript
const siHei = () => {
  console.log("Hei!");
}
siHei();
```

---

### **4. Betingelser (if-else)**  
Brukes for å ta avgjørelser basert på vilkår.  
Eksempel:
```javascript
let poeng = 85;
if (poeng >= 50) {
  console.log("Bestått!");
} else {
  console.log("Ikke bestått.");
}
```

---

### **5. Løkker**  

#### **For-løkke**  
Går gjennom en kodeblokk et bestemt antall ganger.  
Eksempel:
```javascript
for (let i = 0; i < 5; i++) {
  console.log("Tallet er: " + i);
}
```

#### **While-løkke**  
Utfører kode så lenge en betingelse er sann.  
Eksempel:
```javascript
let i = 0;
while (i < 5) {
  console.log("Tallet er: " + i);
  i++;
}
```

---

### **6. Lister (Arrays)**  
En liste (array) lagrer flere verdier sammen i én variabel.  
Eksempel:
```javascript
const frukt = ["eple", "banan", "appelsin"];
console.log(frukt[0]); // Skriver ut "eple"
```

#### **Legge til, fjerne og endre elementer i en liste**

**Legge til element**  
```javascript
frukt.push("druer"); // Legger til "druer" på slutten av listen
```

**Fjerne element med `pop()`**  
```javascript
frukt.pop(); // Fjerner det siste elementet i listen
```

**Fjerne element med `splice()`**  
Med `splice()` kan du fjerne et element fra en bestemt posisjon:
```javascript
frukt.splice(1, 1); // Fjerner 1 element fra indeks 1 (banan blir fjernet)
```
**Merk:** Når du fjerner et element med `splice()`, endres indeksen til de etterfølgende elementene. For eksempel, etter å ha fjernet "banan" fra listen, vil "appelsin" nå ha indeks 1 i stedet for 2.

**Endre element**  
Du kan endre et spesifikt element i listen ved å bruke dets indeks:
```javascript
frukt[1] = "pære"; // Endrer det andre elementet (banan) til "pære"
```

Du kan også bruke `splice()` for å endre et element:
```javascript
frukt.splice(1, 1, "pære"); // Erstatter elementet på indeks 1 med "pære"
```

#### **`for...of`-løkke**  
Går gjennom hvert element i en liste.  
```javascript
for (const element of frukt) {
  console.log(element); // Skriver ut "eple", "pære", "appelsin" etter fjerning
}
```

#### **`forEach`-metoden**  
`forEach` er en innebygd metode som utfører en gitt funksjon for hvert element i en liste. Den er spesielt nyttig for å iterere gjennom lister.

Eksempel:
```javascript
const frukt = ["eple", "banan", "appelsin"];

frukt.forEach((element) => {
  console.log(element);
});
```
I dette eksempelet vil funksjonen bli kjørt for hvert element i listen, og `element` refererer til hvert enkelt element i `frukt`.

---

### **7. Objekter**  
Objekter lagrer data i egenskaper (properties).  
Eksempel:
```javascript
const elev = {
  navn: "Jonas",
  alder: 17,
  erElev: true
};
console.log(elev.navn); // Skriver ut "Jonas"
```

**`for...in`-løkke**  
Går gjennom alle egenskaper i et objekt.  
```javascript
for (const egenskap in elev) {
  console.log(egenskap + ": " + elev[egenskap]);
}
```

---

### **8. Klasser og Metoder**  
Klasser brukes til å lage objekter med spesifikke egenskaper og metoder.  
Eksempel:
```javascript
class Bil {
  constructor(merke, modell) {
    this.merke = merke;
    this.modell = modell;
  }
  kjør() {
    console.log(`${this.merke} ${this.modell} kjører.`);
  }
}

const bil1 = new Bil("Toyota", "Corolla");
bil1.kjør(); // Skriver ut "Toyota Corolla kjører."
```

---

### **9. Subklasser (Arv)**  
Subklasser lar en klasse arve egenskapene og metodene til en annen klasse.  
Eksempel:
```javascript
class ElBil extends Bil {
  lad() {
    console.log(`${this.merke} ${this.modell} lader.`);
  }
}

const tesla = new ElBil("Tesla", "Model S");
tesla.kjør(); // Arvet metode
tesla.lad();  // Ny metode
```

---

### **10. DOM-manipulasjon**  
JavaScript kan manipulere HTML-innhold med Document Object Model (DOM). Det gir mulighet til å endre eller fjerne elementer dynamisk.

#### **Velge og endre elementer**
Eksempler:
```javascript
document.getElementById("overskrift").innerHTML = "Velkommen!";
document.querySelector(".tekst").innerHTML = "Hei, alle sammen!";
```
- `getElementById`: velger element etter ID.
- `querySelector`: velger første element som matcher CSS-selektoren.
- `querySelectorAll`: velger alle elementer som matcher CSS-selektoren og returnerer en liste.
  
Eksempel på `querySelectorAll`:
```javascript
const elementer = document.querySelectorAll(".klasser");
elementer.forEach(element => {
  element.style.color = "red"; // Endrer fargen til alle elementene med klassen "klasser" til rød
});
```

#### **Opprette og fjerne elementer**  

**`createElement`**  
Du kan lage nye HTML-elementer og legge dem til på siden:
```javascript
const nyttElement = document.createElement("div");
nyttElement.innerHTML = "Dette er en ny div!";
nyttElement.className = "ny-klasse";
nyttElement.id = "nyId";
nyttElement.style.color = "blue";

document.body.appendChild(nyttElement); // Legger til elementet i body
```

**`removeElement`**  
Fjern et element fra siden:
```javascript
const element = document.getElementById("nyId");
element.remove(); // Fjerner elementet med ID 'nyId'
```

---

### **11. Event Listeners**  
Event Listeners brukes for å reagere på ulike hendelser i brukergrensesnittet, som klikk på knapper eller tastetrykk. Ved å legge til en Event Listener kan du spesifisere hvilken funksjon som skal kjøres når en bestemt hendelse inntreffer.

Eksempel:
```javascript
document.querySelector("#knapp").addEventListener("click", () => {
  alert("Du klikket på knappen!");
});
```


**Legge til en Event Listener med en egen funksjon**  
Du kan definere en funksjon og deretter bruke `addEventListener` for å binde den til en hendelse. Dette gjør koden mer organisert og lett å vedlikeholde.

```javascript
function visMelding() {
  alert("Du klikket på knappen!");
}

document.querySelector("#knapp").addEventListener("click", visMelding);
```

I dette eksemplet vil når knappen med ID "knapp" klikkes, funksjonen `visMelding` bli kalt, og en alert-boks vil vises.

---

**Legge til Event Listener for tastaturinput (Enter-tasten)**  
Du kan også lytte til tastaturhendelser ved å bruke `addEventListener` på dokumentet. I dette tilfellet kan vi sjekke om brukeren har trykket på Enter-tasten.

```javascript
document.addEventListener("keypress", (event) => {
  if (event.key === "Enter") {
    console.log("Enter-tasten ble trykket!");
  }
});
```

Her legger vi til en Event Listener for `keypress`-hendelsen på hele dokumentet. Når en tast trykkes ned, sjekker vi om den trykkede tasten er "Enter", og hvis den er det, skriver vi ut en melding i konsollen.

---

**Bruke `onclick`-metoden**  
En annen måte å håndtere klikk på er ved å bruke `onclick`-metoden direkte på et DOM-element. Dette er en enklere tilnærming, men mindre fleksibel enn `addEventListener`.

```javascript
const knapp = document.querySelector("#knapp");
knapp.onclick = () => {
  alert("Knappen ble klikket!");
};
```

I dette eksemplet setter vi `onclick`-egenskapen på knappen, som vil utføre den angitte funksjonen når knappen klikkes. Dette er nyttig for enkle interaksjoner, men husk at det bare lar deg legge til én funksjon per hendelse.

---

### **12. Kommentarer**  
Kommentarer er notater i koden som ikke påvirker kjøringen av programmet. De brukes til å forklare kode og gjøre den lettere å forstå.

- **Enkel linjekommentar**: Bruker `//` for kommentarer som går over én linje.  
  Eksempel:
  ```javascript
  // Dette er en kommentar
  const tall = 5; // Tallvariabel
  ```

- **Flere linjer**: Bruker `/* ... */` for kommentarer som strekker seg over flere linjer.  
  Eksempel:
  ```javascript
  /*
  Dette er en kommentar
  som strekker seg over flere linjer
  */
  const navn = "Ola";
  ```

---
