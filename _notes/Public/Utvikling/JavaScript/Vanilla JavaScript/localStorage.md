---
title: localStorage
feed: show
date: 23-09-2025
---

## Hva er `localStorage`?

Når vi lager nettsider, kan det noen ganger være nyttig å lagre informasjon slik at den ikke forsvinner når vi laster siden på nytt.  
For eksempel:

- Huske brukernavn til en elev som har logget inn.
    
- Huske hvilken bakgrunnsfarge brukeren har valgt.
    

Til dette kan vi bruke **`localStorage`**, som er en del av nettleseren.

---

## Viktige egenskaper

- `localStorage` lagrer data **lokalt i nettleseren**.
    
- Dataen blir liggende der selv om du lukker nettleseren eller skrur av PC-en.
    
- Den lagrer **alltid som tekst (string)**.
    

---

## Hvordan bruke `localStorage`

### 1. Lagre data

```js
localStorage.setItem("navn", "Ola");
```

Her lagres teksten `"Ola"` med nøkkelen `"navn"`.  
Tenk på det som en merkelapp og en verdi:

- **nøkkel (key):** "navn"
    
- **verdi (value):** "Ola"
    

---

### 2. Hente data

```js
const lagretNavn = localStorage.getItem("navn");
console.log(lagretNavn); // Skriver "Ola"
```

---

### 3. Slette data

```js
localStorage.removeItem("navn");
```

Dette sletter bare den nøkkelen du velger.

Hvis du vil slette **alt** som er lagret i `localStorage`:

```js
localStorage.clear();
```

---

## Viktig å huske

- Alt lagres som tekst, selv om du skriver inn et tall:
    

```js
localStorage.setItem("alder", 16);
const alder = localStorage.getItem("alder");
console.log(alder); // Skriver "16" (som tekst, ikke tall)
```

- Senere skal vi lære å lagre mer kompliserte ting som lister og objekter, men da trenger vi **JSON**. Enn så lenge kan dere lagre enkle ting som navn, tall (som tekst), eller små innstillinger.
    
---