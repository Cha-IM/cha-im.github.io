---
title: State – lagre og endre data i komponenter
feed: show
date: 15-05-2025
---

Mens **props** brukes til å sende data _inn_ i en komponent, brukes **state** for å _lagre og endre data_ _inne i_ komponenten. Dette er nyttig når du vil lage interaktive komponenter som for eksempel teller, viser/skjuler noe, eller reagerer på brukerens input.

---

### Hva er state?

State er en "lokal tilstand" i komponenten – altså data som React husker, og som kan endres. Når state endres, vil komponenten **rendres på nytt** (oppdateres automatisk i nettleseren).

For å bruke state trenger du en **React-hook** som heter `useState`. Dette importeres fra React:

```jsx
import { useState } from 'react';
```

---

### Eksempel: Tell hvor mange ganger brukeren har trykket på en knapp

```jsx
// Teller.jsx

import { useState } from 'react';

function Teller() {
  const [antall, setAntall] = useState(0);

  return (
    <div>
      <p>Du har trykket {antall} ganger</p>
      <button onClick={() => setAntall(antall + 1)}>Trykk meg</button>
    </div>
  );
}

export default Teller;
```

---

### Hva skjer her?

```jsx
const [antall, setAntall] = useState(0);
```

- `useState(0)` sier at startverdien er `0`.
- `antall` er den nåværende verdien.
- `setAntall` er en funksjon du bruker for å oppdatere verdien.
- Når `setAntall` blir kalt, oppdaterer React komponenten automatisk.

Knappen har en **event handler**:

```jsx
onClick={() => setAntall(antall + 1)}
```

Dette betyr: Når knappen trykkes, øk `antall` med 1.

---

### Prøv selv!

Lag en fil `Teller.jsx` i `components`-mappa og legg inn koden over. Deretter importer den i `App.jsx`:

```jsx
import Teller from './components/Teller';

function App() {
  return (
    <div>
      <Teller />
    </div>
  );
}
```

---

### Flere eksempler på state

- **Skru av/på tekst**
- **Lagre input fra brukeren**
- **Bytte mellom lys og mørk modus**

Disse krever ofte at man holder på en tilstand som endres når noe skjer – da bruker man `useState`.

