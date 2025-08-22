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

### Hvordan bruke en komponent?

For å bruke `Hilsen`-komponenten i prosjektet ditt, må du først importere den i en annen komponent, for eksempel i `App.jsx`:

```jsx
import Hilsen from './components/Hilsen';

function App() {
  return (
	<>
		<Hilsen />
    </>
  );
  
}

export default App;
```

Inni `return` må alt vi viser være pakket inn i ett HTML-element. For å slippe å bruke unødvendige `<div>`-er, kan vi bruke tomme tagger: `<>` og `</>`, slik som i eksempelet. Dette kalles et _fragment_.

Legg merke til at komponenter **må ha stor forbokstav**, og at man bruker dem som HTML-tagger uten avslutningstagg, slik: `<Hilsen />`.

---

### Sette sammen flere komponenter

Du kan sette sammen flere forskjellige komponenter i en fil. På denne måten kan komponenter fungere som en slags mal for elementer på en nettside. For eksempel kan vi lage en header-komponent som kan legges øverst på alle nettsider:

```jsx
// Header.jsx

function Header() {
  return (
    <>
      <h1>KOKEBOKA.NO</h1>
      <h2>De beste norske oppskriftene</h2>
    </>
  );
}

export default Header;
```

Og bruke den sammen med andre komponenter, slik:

```jsx
import Header from './components/Header';
import Hilsen from './components/Hilsen';

function App() {
  return (
    <>
      <Header />
      <Hilsen />
    </>
  );
}
```

Da vil du få en nettside som har headeren øverst, og hilsenen (Hei verden!) under.

---

### Hvor skal komponenter lagres?

Lag en egen mappe i `src` som heter `components`, og lagre komponentene der. Eksempel:

```
src/
├── components/
│   ├── Hilsen.jsx
│   └── Header.jsx
├── App.jsx
└── main.jsx
```

