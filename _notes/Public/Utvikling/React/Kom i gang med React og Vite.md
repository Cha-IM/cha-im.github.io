---
title: Kom i gang med React og Vite
feed: show
date: 15-05-2025
---


Denne guiden lærer deg å komme i gang med å lage en React-app med Vite.

* **React** er et web-rammeverk for å lage moderne web-apper ved å sette sammen ferdiglagde komponenter.
* **Vite** er et utviklingsverktøy som blant annet kan kjøre en lokal webserver med live oppdatering.

## Installere node.js
For å bruke React må du først installere **Node.js**. Dette er et program som lar deg kjøre JavaScript-programmer utenfor nettleseren. Dette gjør JavaScript mye mer fleksibelt, og man kan bruke Node.js til å lage servere (backend) og skrive til filer og databaser. Du finner Node.js her: [Node.js — Run JavaScript Everywhere](https://nodejs.org/en). Last ned nyeste versjon og installer det. Merk at installasjonen kan ta litt tid, og det kan åpnes kommandolinjevinduer under installasjonen som legger inn tilleggsfunksjonalitet.

Innebygd i node.js er **NPM**, Node Package Manager, som lar deg installere tilleggspakker og kjøre script i node-prosjektene dine. NPM kjøres direkte i terminalen (kommandovinduet), f.eks. via VS Code.

![Infografikk om node.js](/assets/img/react/npm-infographic.png)


---

## Lage et React-prosjekt med Vite og npm

Vi skal nå opprette et nytt React-prosjekt. 
1. Åpne VS Code og åpne en mappe der prosjektet ditt skal lagres. Du trenger ikke lage en ny mappe for prosjektet, for det gjøres automatisk når du oppretter prosjektet med NPM. 
2. Åpne terminalen i VS Code ved å klikke på *Terminal* i menylinjen øverst, og velg *New terminal*. Terminalvinduet vil da komme opp nederst i VS Code-vinduet. Hvis du ikke ser *Terminal* på menylinjen får du det opp ved å klikke de tre prikkene til høyre på menylinja (ved søkefeltet).

---
### Opprett et nytt prosjekt

I terminalen, skriv:

```bash
npm create vite@latest
```

Du får da opp noen valg i terminalen. Bruk piltastene og enter-tasten for å velge:

- **Project name**: for eksempel `matoppskrifter`
- **Framework**: `React`
- **Variant**: `JavaScript`

Når du har gjort disse valgene blir prosjektet opprettet, og du vil se at en mappe med prosjektnavnet du valgte har blitt opprettet i *Explorer*-vinduet i VS Code. Inne i denne mappen er det mange filer, men du skal bare redigere noen få av dem. Vi skal gå gjennom hvilke filer du skal jobbe med videre i guiden.

### Får du feilmelding i terminalen?
Det kan være noen problemer med rettigheter eller policy i terminalen når du bruker NPM. Hvis du får feilmelding (rød skrift) når du skriver inn `npm` i terminalen, kan du prøve å endre shell i terminalen. Til høyre øverst i terminalen ser du en knapp med et plusstegn (+). Ved siden av dette står det hvilket shell du bruker (f.eks. Powershell). Klikk på den lille pilen (v) ved pluss-knappen for å velge et annet shell. Velg **Command Prompt**. Skriv deretter inn kommandoen på nytt.

![](/assets/img/react/select-shell.png)

#### Virker det fortsatt ikke?
Om det fortsatt ikke virker kan du prøve å installere **PNPM** i stedet for NPM. I terminalen, skriv:

```shell
winget install pnpm.pnpm -e
```

Etter at installasjonen er ferdig, oppretter du prosjektet slik:

```shell
pnpm create vite@latest
```
I resten av guiden kommer vi til å bruke NPM. Om du måtte installere PNPM skriver du bare `pnpm` i stedet for `npm` i alle kommandoene videre. Resten av kommandoen vil være det samme om du bruker NPM eller PNPM.

---

### Gå inn i prosjektet og installer avhengigheter
Når vi jobber i terminalen må vi passe på at vi alltid står i mappen vi skal jobbe i. Hver linje i terminalen starter med adressen til mappen der du står. Slik kan du se at du er på riktig plass. Siden det ble opprettet en ny mappe må du gå inn i denne mappa. Skriv i terminalen:

```bash
cd matoppskrifter
```

Nå må du installere avhengigheter. Det vil si å installere tilleggsfunksjonalitet som trengs for å kjøre prosjektet ditt. Dette er definert i *package.json*-filen i prosjektet ditt. Heldigvis er denne prosessen automatisert i NPM, så du trenger bare å skrive denne kommandoen, så gjøres alle installasjoner automatisk:

```shell
npm install
```


---

### Start utviklingsserveren
Nå kan du starte en webserver så du kan se websiden du har opprettet med React. Foreløpig er det bare en mal, men det er nyttig å åpne den, så du kan se at installasjonen har vært vellykket. Skriv dette i terminalen for å starte en utviklingswebserver.

```bash
npm run dev
```

Da startes en lokal webserver på adressen [http://localhost:5173](http://localhost:5173/). Denne kjøres via Vite, som gjør at endringer du gjør i koden din vil vises umiddelbart på nettsiden.

![](/assets/img/react/vite-react-template.png)

---

### Filstruktur og kode

Hvis du ser i prosjektmappen din ser du en rekke mapper og filer. Her ser du en oversikt over de viktigste filene:

```pgsql
matoppskrifter/
├── node_modules/         ← Alle installerte npm-pakker (automatisk generert)
├── public/
│   └── vite.svg          ← Standard ikon (kan slettes eller byttes)
├── src/
│   ├── assets/           ← Bilder, ikoner, osv.
│   ├── App.jsx           ← Hovedkomponenten for appen
│   ├── App.css           ← Stil for App.jsx
│   ├── main.jsx          ← Startpunktet som kobler React til HTML
│   └── index.css         ← Global CSS
├── .gitignore            ← Hvilke filer Git skal ignorere
├── index.html            ← Hoved-HTML-filen (roten til appen)
├── package.json          ← Info om prosjektet + hvilke npm-pakker som brukes
├── package-lock.json     ← Låser versjonene til avhengighetene
└── vite.config.js        ← Konfigurasjon for Vite

```

Når du skal jobbe med React-prosjektet ditt vil du stort sett redigere og opprette filer i *src*-mappen. Hvis du åpner filen *App.jsx* ser du koden til malen som du åpnet i nettleseren. Prøv å redigere HTML-koden i denne filen, så vil endringene oppdateres øyeblikkelig i nettleseren hver gang du lagrer filen.

#### .JSX-filer

I React bruker vi ikke HTML og JS-filer, men vi bruker i stedet filtypen JSX, som står for JavaScript XML. I JSX kan du skrive JavaScript- og HTML-kode i samme fil, slik at kodingen blir mer sømløs, med både innhold og logikk i samme fil.

Her er et eksempel på en .jsx-fil:

```jsx
//Hei.jsx

function Hei() {

	const navn = "Aurora";
	
	return(
		<h1>Hei {navn}</h1>
	);
	
}

export default Hei;
```
