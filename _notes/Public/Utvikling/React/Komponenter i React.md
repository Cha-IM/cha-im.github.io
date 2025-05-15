---
title: Komponenter i React
feed: show
date: 15-05-2025
---


En av de viktigste ideene i React er **komponenter**. Komponenter er gjenbrukbare byggeklosser som hver representerer en del av brukergrensesnittet (UI). Du kan tenke på dem som funksjoner som returnerer HTML.

---

### Hva er en komponent?

En komponent er en **JavaScript-funksjon** som returnerer **JSX**. JSX ser ut som HTML, men det er egentlig JavaScript.

Her er et enkelt eksempel:

```jsx
// Hilsen.jsx

function Hilsen() {
  return <h1>Hei, verden!</h1>;
}

export default Hilsen;
```

Denne komponenten returnerer en `<h1>`-overskrift. Den kan brukes hvor som helst i React-prosjektet.

---

### 🔌 Hvordan bruke en komponent?

For å bruke `Hilsen`-komponenten i prosjektet ditt, må du først importere den i en annen komponent, for eksempel i `App.jsx`:

```jsx
import Hilsen from './Hilsen';

function App() {
  return (
	<>
	    <div>
	      <Hilsen />
	    </div>
    </>
  );
  
}

export default App;
```

Når vi bruker komponenter må vi starte og avslutte return-funksjonen med en tom HTML-tagg (`<>` og `</>`), slik som i eksempelet. Legg merke til at komponenter **må ha stor forbokstav**, og at man bruker dem som HTML-tagger uten avslutningstagg, slik: `<Hilsen />`.

---

### Lage flere komponenter

Du kan lage mange forskjellige komponenter. For eksempel:

```jsx
// Oppskrift.jsx

function Oppskrift() {
  return (
    <div>
      <h2>Pannekaker</h2>
      <p>Ingredienser: Melk, mel, egg</p>
    </div>
  );
}

export default Oppskrift;
```

Og bruke den slik:

```jsx
import Oppskrift from './Oppskrift';

function App() {
  return (
    <div>
      <Oppskrift />
    </div>
  );
}
```

---

### Hvor skal komponenter lagres?

Lag en egen mappe i `src` som heter `components`, og lagre komponentene der. Eksempel:

```
src/
├── components/
│   ├── Hilsen.jsx
│   └── Oppskrift.jsx
├── App.jsx
└── main.jsx
```

