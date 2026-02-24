

```shell
express --no-view .
npm install express-session bcrypt better-sqlite3
```

db.js
```js
const Database = require("better-sqlite3");

// Initialize SQLite database

const db = new Database('bil.db');

module.exports = db;
```

routes/biler.js
```js
const express = require('express');

const router = express.Router();

const db = require('../db');

  

router.get('/', function(req, res) {

    const cars = db.prepare('SELECT * FROM bil').all();

    res.json(cars);

});

  

module.exports = router;
```

routes/personer.js
```js
const express = require('express');

const router = express.Router();

const db = require('../db');

  

router.get('/', function(req, res) {

    const users = db.prepare('SELECT * FROM person').all();

    res.json(users);

});

  

module.exports = router;
```


```shell
sqlite3
> .open bil.db
```

```sql
create table person(
id INT PRIMARY KEY,
fornavn TEXT,
etternavn TEXT,
epost TEXT,
tlf TEXT);

create table bil(
id INT PRIMARY KEY,
regnr TEXT,
bilmerke TEXT,
modell TEXT,
aarsmodell INT,
farge TEXT);

INSERT INTO person VALUES (1, 'Karl Arne', 'Dalsaune', 'karda@trondelagfylke.no', '45030745'); 

ALTER TABLE bil ADD COLUMN personID INT;

insert into bil values (1, 'EK69810', 'Tesla', 'Model X', 2017, 'Mørk grå', 1); 

alter table person add column passord TEXT; 

update person set passord = '123' where id=1;

```


middleware/auth.js
```js
const express = require('express');

const session = require('express-session');

  

function kreverInnlogging(req, res, next) {

    if (!req.session || !req.session.bruker) {

        return res.status(401).json({ message: "Du må være innlogget for å få tilgang" });

    }

       next(); // Gå videre til neste handler

}

module.exports = kreverInnlogging;
```



Rekkefølge

1. login.html
2. routes/login.js
	1. router.post()
3. public/javascripts/loginHandler.js
4. app.js -> app.use(session())
5. auth.js