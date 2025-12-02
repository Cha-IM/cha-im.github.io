---
title: Express-app med SQLite
feed: show
date: 02-12-2025
---
Denne guiden bruker `sqlite3`-modulen til å håndtere databasens opprettelse og skjema direkte fra Node.js-koden, slik at du slipper manuell installasjon av SQLite CLI-verktøyet.

### ⚙️ Forutsetninger

- **Node.js** og **npm** er installert.
- Du bruker **VS Code** på Windows 11.
- Du har **ikke** installert det frittstående SQLite CLI-verktøyet.

### Steg 1: Opprett Prosjekt og Installer Express

Lag en mappe til prosjektet, for eksempel **`chatteapp`**. Åpne mappen i VS Code.

1. **Installer `express-generator` globalt** (hvis du ikke har gjort det):

```bash
npm install -g express-generator
```

2. **Opprett Express-prosjektet** i gjeldende mappe (`.`):
```bash
express --no-view .
``` 
   
3. **Installer prosjektavhengigheter:**

```bash
npm install
```

4. **Installer SQLite-modulen:**
   
```bash
npm install sqlite3
```


### Steg 2: Oppsett av Database og Skjema

Vi oppretter en mappe for databaselogikken og en fil som håndterer både tilkobling og tabellstruktur.

1. **Opprett database-mappen:**
```bash
mkdir db
```

2. **Opprett filen `db/db_setup.js`**: Denne filen kobler til, oppretter databasen automatisk hvis den mangler, og definerer tabellene.


#### Innhold i `db/db_setup.js`

```js
const sqlite3 = require('sqlite3').verbose();
const DB_PATH = 'db/chat.db'; 

const db = new sqlite3.Database(DB_PATH, (err) => {
  if (err) {
    console.error("Kunne ikke koble til database:", err.message);
    process.exit(1);
  }
  console.log('✅ Koblet til SQLite-databasen.');
});

// Funksjon for å opprette tabellen
db.serialize(() => {
    db.run(`
        CREATE TABLE IF NOT EXISTS melding (
          id INTEGER PRIMARY KEY AUTOINCREMENT,
          person TEXT NOT NULL,
          melding TEXT NOT NULL,
          tid TEXT NOT NULL
        );
    `, (err) => {
        if (err) {
            console.error("Feil ved oppretting av tabell:", err.message);
        } else {
            console.log("✅ Tabellen 'melding' er klar.");
        }
    });
});

module.exports = db;
```

### Steg 3: Lag Ruter og Registrer i `app.js`

Vi lager ruten for meldinger og registrerer den sentralt.

1. **Lag filen `routes/meldinger.js`**: Denne filen importerer databaseobjektet fra den nye stien (`../db/db_setup`).


#### Innhold i `routes/meldinger.js`


```js
const express = require('express');
const router = express.Router();
const db = require('../db/db_setup'); 

router.get('/', (req, res) => {
  db.all('SELECT * FROM melding ORDER BY id DESC', [], (err, rows) => {
    if (err) return res.status(500).json({ error: "Databasefeil" });
    res.json(rows);
  });
});

router.post('/', (req, res) => {
  // Merk: Tiden kan også beregnes i Node.js-koden for å være sikrere
  const { person, melding, tid } = req.body; 
  const sql = `INSERT INTO melding (person, melding, tid) VALUES (?, ?, ?)`;

  db.run(sql, [person, melding, tid], function (err) {
    if (err) return res.status(500).json({ error: "Kunne ikke lagre melding" });
    // Bruk this.lastID for å returnere ID-en til den nye meldingen (god praksis)
    res.status(201).json({ id: this.lastID }); 
  });
});

module.exports = router;
```

2. **Registrer ruten i `app.js`**: Åpne `app.js` og legg til JSON-parsing og ruten.

#### Endringer i `app.js` (Utdrag)


```js
// Legg inn ruten FØR middleware/error handlers, sammen med 
// `var indexRouter = require('./routes/index');`
const meldingerRouter = require('./routes/meldinger'); 


// Legg inn ruten, under
// `app.use('/', indexRouter);`
app.use('/meldinger', meldingerRouter); 

// Husk at
// `module.exports = app;`
// alltid skal være nederst.
```



<!--
### Steg 4: Kjør Databaseoppsettet

Før du starter webserveren, må du sørge for at oppsettsfilen kjøres minst én gang for å opprette **`chat.db`**-filen og **`melding`**-tabellen.

Gå inn i `db`.mappen i terminalen
```bash
cd db
```

Kjør i terminalen (fra rotmappen):

```bash
node db_setup.js
```

Du skal se meldingene:

✅ Koblet til SQLite-databasen.

✅ Tabellen 'melding' er klar.

Du vil nå se at det er dukket opp en ny fil i `db`-mappen, `chat.db`
-->

### Steg 4: Lag frontend-side
Rediger `public/index.html`:

```html
<!DOCTYPE html>
<html lang="no">
<head>
  <meta charset="UTF-8">
  <title>Chat</title>
</head>
<body>
  <h1>Chat</h1>

  <div id="output"></div>

  <form id="skjema">
    <input id="navn" placeholder="Navn" required>
    <input id="melding" placeholder="Melding" required>
    <button type="submit">Send</button>
  </form>

  <script src="javascripts/chat.js"></script>
</body>
</html>
```

Opprett filen `chat.js` i mappen `public/javascripts/`.
Her bruker vi GET og POST-metodene for å hente og skrive data fra/til databasen.

```js
// Funksjon for å hente meldingene fra databasen og skrive dem ut på nettsiden
async function hent() {
  const res = await fetch('/meldinger');
  const data = await res.json();
  const out = document.getElementById("output");
  out.innerHTML = "";

  data.forEach(m => {
	const el = document.createElement("div");
	el.innerHTML = `[${m.tid}] ${m.person}: ${m.melding}`;
	out.appendChild(el);
  });
}

// Henter HTML-elementer som vi bruker i koden
const skjema = document.getElementById("skjema");
const navnEl = document.getElementById("navn");
const meldingEl = document.getElementById("melding");

// Legger en hendelseslytter på "Send"-knappen 
skjema.addEventListener("submit", async (e) => {
  e.preventDefault();
  // Henter nøyaktig tidspunkt for når funksjonen kjøres
  const tid = new Date().toISOString().replace("T"," ").substring(0,19);

// Bruker POST-metoden på /meldinger-ruten til å sende data til databasen. 
  await fetch('/meldinger', {
	method: 'POST',
	headers: { "Content-Type": "application/json" },
	body: JSON.stringify({
	  person: navnEl.value,
	  melding: meldingEl.value,
	  tid
	})
  });
  // Tømmer alle meldinger som er skrevet ut
  meldingEl.value = "";
  // Kjører hent()-funksjonen for å skrive ut alle meldinger på nytt, inkludert den nyeste.
  hent();
});

//Programmet starter med å skrive ut alle meldinger i databasen
hent();
```

### Steg 5: Start Server og Test

1. **Start serveren:**

```bash
npm start
```

2. **Databasefilen opprettes**: Se at filen `chat.db` opprettes i `db/`-mappen.
3. **Test i nettleser:** Åpne nettleseren på `http://localhost:3000/`. Skriv inn navn og melding.

### Steg 6: Kontroll av databasen i VS Code

I stedet for å bruke SQLite CLI i terminalen, kan du bruke VS Code-utvidelsen for å sjekke databasen. Søk opp SQLite i Extensions-menyen og installer den øverste:

1. Høyreklikk på filen **`db/chat.db`** i utforskeren.
2. Velg **"Open Database"**.
3. Se innholdet og dataen du har lagt inn under "SQLITE EXPLORER" nederst i venstrepanelet.
