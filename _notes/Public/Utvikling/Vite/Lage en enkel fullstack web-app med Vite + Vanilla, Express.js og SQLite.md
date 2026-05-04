---
title: Lage en enkel fullstack web-app med Vite + Vanilla, Express.js og SQLite
feed: show
date: 04-05-2026
---
Vi kan bruke Vite + Vanilla for å lage en fullstack web-app med vanlig HTML og JavaScript pluss litt serverkode i Express/Node.js.

## Innhold
- Sette opp frontend med Vite + Vanilla
- Sette opp backend med Express.js
- Sette opp databaseserveren og API for å kommunisere med databasen
- Koble frontend og backend
- Skrive til databasen
- Oppsummering og veien videre


## Sette opp frontend med Vite + Vanilla
Først: Opprett en mappe der du skal opprette prosjektet ditt, og åpne mappa i VS  Code.

Så åpner du terminalen, og skriver denne koden:

```shell
npm create vite@latest .
```

Gjør deretter valgene som vist på bildet:

![Skjermbilde 2026-05-04 141355.png](/assets/img/vite-vanilla/Skjermbilde2026-05-04-141355.png)

Vite vil nå installere Vanilla-rammeverket og starte en webserver på localhost.


## Sette opp backend med Express.js

Siden terminalen du åpnet fra før er opptatt med å kjøre Vite-webserveren, må du åpne en ny terminal. Trykk på den lille pilen ved plusstegnet øverst på terminalen og velg *Command prompt*.

![](/assets/img/vite-vanilla/Skjermbilde2026-05-04-141448.png)

Så skriver du denne kommandoen i terminalen for å installere express og alt som er nødvendig for å sette opp en SQLite-database:

```shell
npm install express cors better-sqlite3
```

### Sette opp databaseserveren og API for å kommunisere med databasen

![](/assets/img/vite-vanilla/Skjermbilde2026-05-04-143756.png)

Opprett en ny fil i rotmappen som du kaller *server.js*. Legg inn følgende kode:

```js
import express from 'express';
import Database from 'better-sqlite3';
import cors from 'cors';
  
const app = express();
const db = new Database('database.db'); // Lager filen automatisk
  
app.use(cors());
app.use(express.json());
  
// Lag en tabell hvis den ikke finnes
db.exec("CREATE TABLE IF NOT EXISTS meldinger (id INTEGER PRIMARY KEY, tekst TEXT)");
  
// API-endepunkt for å hente data
app.get('/api/data', (req, res) => {
    const rows = db.prepare("SELECT * FROM meldinger").all();
    res.json(rows);
});
  
// API-endepunkt for å lagre data
app.post('/api/data', (req, res) => {
    const { tekst } = req.body;
    const info = db.prepare("INSERT INTO meldinger (tekst) VALUES (?)").run(tekst);
    res.json({ id: info.lastInsertRowid });
});
  
app.listen(3001, () => console.log('Server kjører på http://localhost:3001'));
```

---

**NB:** Denne koden gir deg utgangspunktet for en meldings-app som lagrer meldinger i en tabell i en SQLite-database. Hvis den skal brukes til noe annet, endrer du bare hvilke tabeller og felter som skal opprettes her.

---

## Koble frontend og backend

Nå skal du koble frontenden til backenden ved å lage et skjema for å legge inn meldinger i databasen, pluss at du skal vise fram alle meldingene som er lagt inn.

Åpne */src/main.js* og slett all koden unntatt første linje (den som importerer CSS). Lim inn denne koden:

```js
document.querySelector('#app').innerHTML = `
  <div>
    <h1>Vite + SQLite</h1>
    <input type="text" id="input" placeholder="Skriv noe...">
    <button id="send">Lagre til DB</button>
    <ul id="liste"></ul>
  </div>
`;

const input = document.querySelector('#input');
const knapp = document.querySelector('#send');
const liste = document.querySelector('#liste');

// Hent data fra SQLite via serveren
async function hentData() {
    const respons = await fetch('http://localhost:3001/api/data');
    const data = await respons.json();
    liste.innerHTML = data.map(item => `<li>${item.tekst}</li>`).join('');
}

// Send data til SQLite
knapp.onclick = async () => {
    await fetch('http://localhost:3001/api/data', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ tekst: input.value })
    });
    input.value = '';
    hentData();
};

hentData();
```



Dette oppretter et tekstfelt og en knapp i HTML-koden i *index.html*, henter ut alle meldinger som er lagret i databasen, og sender nye meldinger til databasen når du klikker på knappen.

### Start databaseserveren

For å opprette databasen og gjøre det mulig for *main.js* å kommunisere med databasen må du starte databaseserveren manuelt. Dette gjør du med denne kommandoen i det nye terminalvinduet du åpnet:

```shell
node server.js
```

![](/assets/img/vite-vanilla/Skjermbilde2026-05-04-143925.png)

Du vil da se at databasefilen blir opprettet i rotmappen:

![](/assets/img/vite-vanilla/Skjermbilde2026-05-04-144153.png)

## Skrive til databasen

Åpne web-appen din i nettleseren med adressen som står i vite-terminalen (f.eks. [localhost:5173](http://localhost:5173/))

![](/assets/img/vite-vanilla/Skjermbilde2026-05-04-155007.png)

Du vil da få opp en enkel nettside med en tekstboks og en knapp. Skriv en melding og trykk på knappen.

![](/assets/img/vite-vanilla/Skjermbilde2026-05-04-144102.png)

Meldingen vil da komme opp i en liste under tekstfeltet, sammen med alle andre meldinger som er lagret i databasen.

![](/assets/img/vite-vanilla/Skjermbilde2026-05-04-144433.png)

Hvis du har installert SQLite viewer-extension, kan du se innholdet og strukturen på databasen ved å klikke på *database.db*. (Legg merke til at id fylles ut automatisk med neste ledige tall).

![](/assets/img/vite-vanilla/Skjermbilde2026-05-04-144500.png)

## Oppsummering og veien videre
Du har nå sett hvordan du enkelt kan sette opp en fullstack web-app med database med Vite+Vanilla, Express.js og SQLite. Nå kan du fortsette selv og lage den databasen du trenger. Nye tabeller oppretter du via *server.js* (husk å restarte serveren når du har gjort endringer), og du kan opprette nye tekstfelter i *main.js*.