---
title: Props – sende data til komponenter
feed: show
date: 15-05-2025
---
Når du lager komponenter i React, vil du ofte sende inn data til dem. Dette gjøres med **props** – en forkortelse for _properties_. Props er som argumenter til funksjoner, men for komponenter.

---

### Hva er props?

Props er data som du sender til en komponent når du bruker den. Du kan bruke props til å gjøre komponentene dine mer fleksible og gjenbrukbare.

Her er et eksempel:

```jsx
// Hilsen.jsx

function Hilsen(props) {
  return <h1>Hei, {props.navn}!</h1>;
}

export default Hilsen;
```

Denne komponenten tar imot en prop som heter `navn`, og viser den i teksten.

---

### Sende inn props

Når du bruker komponenten, sender du inn data som “attributter”, akkurat som i HTML:

```jsx
// App.jsx

import Hilsen from './components/Hilsen';

function App() {
  return (
    <div>
      <Hilsen navn="Aurora" />
      <Hilsen navn="Emil" />
    </div>
  );
}

export default App;
```

Her vises to forskjellige hilsener, fordi vi sender inn ulike verdier som prop `navn`.

---

### Props er readonly

Props kan ikke endres inne i komponenten – de er bare til for å sende data inn. Hvis du trenger å endre data i en komponent, må du bruke **state**, som vi kommer tilbake til senere.

---

### Tips for props og komponentstruktur

Hold komponentene enkle: én oppgave per komponent.

Eksempel med en komponent som viser en oppskrift basert på props:

```jsx
// Oppskrift.jsx

function Oppskrift(props) {
  return (
    <div>
      <h2>{props.tittel}</h2>
      <p>{props.ingredienser}</p>
    </div>
  );
}

export default Oppskrift;
```

Og slik bruker du den:

```jsx
// App.jsx

import Oppskrift from './components/Oppskrift';

function App() {
  return (
    <div>
      <Oppskrift 
        tittel="Pannekaker" 
        ingredienser="Melk, mel, egg" 
      />
      <Oppskrift 
        tittel="Smoothie" 
        ingredienser="Banan, bær, yoghurt" 
      />
    </div>
  );
}
```

