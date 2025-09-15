---
title: Kommentarer i koden (JavaScript)
feed: show
date: 15-09-2025
---
### Hva er kommentarer?

Kommentarer er tekst i koden som **ikke påvirker hvordan programmet kjører**. De brukes til å forklare koden for deg selv eller andre som leser programmet senere. Kommentarer gjør koden enklere å forstå og vedlikeholde.

### Hvordan skrive kommentarer i JavaScript

I JavaScript finnes det to hovedmåter å skrive kommentarer på:

1. **Enkeltlinje-kommentarer**  
    Bruk `//` for å skrive kommentarer på én linje:
    
    ```javascript
    // Dette er en kommentar på én linje
    const navn = "Karl"; // Kommentar kan også stå etter en kode
    ```
    
2. **Flerelinje-kommentarer**  
    Bruk `/* ... */` når kommentaren går over flere linjer:
    
    ```javascript
    /*
      Dette er en kommentar
      som går over flere linjer.
      Den kan forklare mer komplekse deler av koden.
    */
    const alder = 17;
    ```
    

### Hva bør man kommentere?

- **Forklar hvorfor, ikke hva**: Koden viser ofte _hva_ som skjer, men kommentaren bør forklare _hvorfor_ du gjør det.
    
    ```javascript
    // Beregner rabatt fordi kunden er medlem
    const prisEtterRabatt = pris * 0.9;
    ```
    
- **Komplisert kode**: Hvis en algoritme eller funksjon er vanskelig å forstå, legg til en kommentar som forklarer logikken.
    
- **TODOs og påminnelser**: Kommentarer kan brukes for å markere ting som må gjøres senere.
    
    ```javascript
    // TODO: Sjekk at brukernavn ikke inneholder spesialtegn
    ```
    

### Hva bør unngås

- **Unødvendige kommentarer**: Ikke kommenter åpenbare ting.
    
    ```javascript
    let x = 5; // Setter x til 5 → unødvendig
    ```
    
- **Gamle eller feilaktige kommentarer**: Hvis koden endres, må også kommentaren oppdateres. Ellers kan det forvirre mer enn det hjelper.
    

### Generelle tips for god praksis

1. Skriv kommentarer som er **korte, tydelige og presise**.
    
2. Kommenter **bare det som er nødvendig** – god kode bør ofte være selvforklarende.
    
3. Bruk **standardiserte merker** som `TODO` eller `FIXME` for å markere oppgaver.
    
4. Kommentarer bør være på samme språk som koden diskuteres i (ofte engelsk i profesjonell kode, norsk kan brukes i undervisning).
    

---

Kommentarer er altså et verktøy for å gjøre koden din mer lesbar og forståelig, men de er ikke en erstatning for ryddig, godt strukturert kode. God praksis handler om å bruke kommentarer smart og målrettet.

Her er noen eksempler på **gode og dårlige kommentarer** i JavaScript:

---

### **Dårlige kommentarer**

Kommentarer som er overflødige eller forvirrende:

```javascript
let x = 5; // Setter x til 5

const navn = "Karl"; // Dette er et navn

// Legger til 1 til i tallet
x = x + 1;
```

**Hvorfor dårlig:**

- Kommentarene sier bare det som allerede står i koden.
    
- De gir ingen ekstra informasjon om hvorfor koden finnes eller hva den gjør i sammenheng.
    

---

### **Gode kommentarer**

Kommentarer som forklarer logikk, hensikt eller påminnelser:

```javascript
// Beregner pris etter rabatt for medlemmer
const prisEtterRabatt = pris * 0.9;

/*
  Sjekker om brukernavn er gyldig:
  - Skal være mellom 3 og 15 tegn
  - Ingen spesialtegn
*/
function erGyldigBrukernavn(navn) {
  return navn.length >= 3 && navn.length <= 15 && /^[a-zA-Z0-9]+$/.test(navn);
}

// TODO: Legg til funksjon for å sende velkomst-epost til nye brukere
```

**Hvorfor bra:**

- Kommentarene forklarer _hvorfor_ koden gjør det den gjør.
    
- Flerelinje-kommentaren gir klar dokumentasjon for en funksjon.
    
- `TODO` viser at noe skal implementeres senere.
    

---

### **Generelle tips**

- Skriv kommentarer som **forklarer hensikten**, ikke det som allerede står i koden.
    
- Bruk kommentarer for **komplekse deler av koden eller for oppgaver som gjenstår**.
    
- Hold kommentarene **kortfattede og lettleste**.
    
