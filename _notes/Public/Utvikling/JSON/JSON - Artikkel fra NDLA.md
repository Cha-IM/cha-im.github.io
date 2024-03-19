---
title: JSON - artikkel fra NDLA
feed: show
date: 19-03-2024
---

[JSON - Utvikling - NDLA](https://ndla.no/subject:5e53694a-c8eb-4871-8558-71523941c28e/topic:7342e935-c243-4277-8d07-d21ffa21b539/resource:607d58ed-da2a-4484-9a78-236fac734e55)

# JSON

Vi ønsker ofte å utveksle data som variabler, lister og objekter mellom programmer og over nett. JSON er en standard for å gjøre om JavaScript-objekter til ren tekst, som lett kan overføres på mange forskjellige måter.

JSON står for JavaScript Object Notation. Med JSON kan vi lagre objekter som skal brukes i JavaScript, som ren tekst. Det at dataene skilles fra koden, gjør det enklere å endre og vedlikeholde data som brukes av en applikasjon eller webside. Dette ligner litt på å bruke Firebase eller andre NoSQL-databaser, men forskjellen er at JSON-data kan lagres lokalt, i samme mappe som websiden.

## Lagre ett objekt som JSON

Data i ei JSON-fil har en spesifikk syntaks som skiller seg litt fra hvordan man lager objekter i JavaScript. Ei JSON-fil kan inneholde ett objekt eller ei liste (array) med objekter. Her er et eksempel på ei JSON-fil med ett objekt:

##### HUND.JSON

```json
1{
2  "navn":"Fido",
3  "kjonn":"M",
4  "rase":"skotsk terrier",
5  "farge":"svart"
6}
```

JSON-data skrives, som du kan se, som par av feltnavn og verdi, med et kolon imellom, slik:

`"feltnavn":"verdi"`

Når vi setter flere felter etter hverandre, bruker vi komma imellom og krøllparenteser rundt for å angi det som et objekt.

Hvis et felt har flere verdier, kan vi sette verdiene i ei liste, slik:

##### HUND.JSON

```json
1{
2  "navn":"Fido",
3  "kjonn":"M",
4  "rase":"skotsk terrier",
5  "farge":"svart",
6  "yndlingsmat":["fiskepudding", "griseøre", "hundemat"]
7}
```


## Lagre flere objekter som JSON

Som nevnt kan ei JSON-fil inneholde ei liste med flere objekter. Det kan vi skrive på denne måten:

##### HUNDER.JSON

```json
1[
2  {
3    "navn":"Fido",
4    "kjonn":"M",
5    "rase":"skotsk terrier",
6    "farge":"svart",
7    "yndlingsmat":["fiskepudding", "griseøre", "hundemat"]
8  },
9  {
10    "navn":"King",
11    "kjonn":"M",
12    "rase":"dvergpuddel",
13    "farge":"brun",
14    "yndlingsmat":["pasta", "loff"]
15  },
16  {
17    "navn":"Bella",
18    "kjonn":"F",
19    "rase":"boxer",
20    "farge":"blond",
21    "yndlingsmat":["biff", "hundemat"]
22  }
23]
```


Noen ganger kan det være nyttig å lagre ett eller flere objekter som verdi til et felt inne i et objekt. Det må vi gjøre hvis vi vil legge til informasjon om eieren av hunden. Da gjør vi slik:

##### HUNDER.JSON (MED EIERE)

```json
1[
2  {
3    "navn":"Fido",
4    "kjonn":"M",
5    "rase":"skotsk terrier",
6    "farge":"svart",
7    "yndlingsmat":["fiskepudding", "griseøre", "hundemat"],
8    "eier":{
9      "navn": "Rebecca Thomasen",
10      "telefon": "12345678"
11    }
12  },
13  {
14    "navn":"King",
15    "kjonn":"M",
16    "rase":"dvergpuddel",
17    "farge":"brun",
18    "yndlingsmat":["pasta", "loff"],
19    "eier":{
20      "navn": "Gabrielle Martin",
21      "telefon": "23456789"
22    }
23  },
24  {
25    "navn":"Bella",
26    "kjonn":"F",
27    "rase":"boxer",
28    "farge":"blond",
29    "yndlingsmat":["biff", "hundemat"],
30    "eier":{
31      "navn": "Jakob Nilsen",
32      "telefon": "2266445"
33    }
34  }
35]
```



## Konvertere JSON-data

Det er mange måter å få JSON-data inn på nettsiden din på. I utgangspunktet er JSON-data bare tekst, så det kan overføres på mange måter. Ofte vil JSON-data leses inn fra en webserver, fra en database eller fra ei tekstfil på datamaskinen din. Det finnes derfor innebygde metoder i JavaScript for å konvertere JSON-data (tekst) til JavaScript-objekter, og motsatt. De mest brukte av disse er `JSON.parse()`, som gjør om JSON-data til JavaScript-objekter, og `JSON.stringify()`, som gjør om JavaScript-objekter til JSON-data. Disse kan du lese om på W3Schools:

- [W3Schools: JSON.parse()](https://www.w3schools.com/js/js_json_parse.asp)
- [W3Schools: JSON.stringify()](https://www.w3schools.com/js/js_json_stringify.asp)

## Importere JSON-data

Hvis du har lagret ei JSON-fil sammen med nettsiden din, eller hvis du har URL-en til ei JSON-fil som ligger på nettet, kan du importere JSON-dataene som en modul i JavaScript, slik:

`import data from` `"_URL_"` `assert` `{` `type: "json" };`

Denne koden både importerer JSON-dataene, og konverterer dem (parse) til JavaScript-data. Du trenger derfor ikke å bruke metoden JSON.parse().

Merk at når du bruker import, må du legge inn `type``="``module``"` i script-taggen på nettsida di, slik:

`<script type="module">`

`import data from` `"_URL_" assert { type: "json" };`

`</script>`

Merk også at `data` ikke skal stå i krøllparenteser.

I tilfellet med _hunder.json_ blir JSON-dataene importert som ei liste med objekter, med variabelnavnet du har satt (`data` i eksempelet over). Dette variabelnavnet kan settes til å være hva du vil, for eksempel `hunder`. For å hente ut navnet til den første hunden, kan du skrive denne koden:

##### SCRIPT TYPE="MODULE"

```js
1import hunder from "./hunder.json" assert { type: "json" };
2
3console.log( hunder[0].navn ) 
```

Kopier kode til utklippstavle

Denne koden vil skrive ut _Fido_ i konsollen.

For å skrive ut informasjon om alle hundene kan du bruke ei løkke:

##### SCRIPT TYPE="MODULE"

```js
1import hunder from "./hunder.json" assert { type: "json" };
2
3for(const hund of hunder){
4  console.log(
5    `${hund.navn} er en ${hund.farge} ${hund.rase} eid av ${hund.eier.navn}.`
6  )
7}
```


Dette vil gi følgende utskrift:

##### CONSOLE

```bash
1Fido er en svart skotsk terrier eid av Rebecca Thomasen.
2King er en brun dvergpuddel eid av Gabrielle Martin.
3Bella er en blond boxer eid av Jakob Nilsen.
```


Hvis du i tillegg vil skrive ut yndlingsmaten til hundene, må du bruke ei løkke inne i løkka for å skrive ut innholdet av lista med yndlingsmat for hver hund. For at utskriften skal bli fin, må vi trikse litt for å få inn komma og _og_ når vi lister opp de forskjellige mattypene. Koden blir slik:

##### SCRIPT TYPE="MODULE"

```js
1import hunder from "./hunder.json" assert { type: "json" };
2
3// Lager variabler som vi skal bruke i løkka
4let utskrift = "";
5let pronomen = "";
6let yndlingsmat = "";
7let i = 0;
8
9// Lager ei løkke for å gå gjennom alle hundene
10for(const hund of hunder){
11
12  if(hund.kjonn == "F"){
13    // Setter pronomen i utskriften til "henne" hvis hunden er hunkjønn
14    pronomen = "hennes";
15  }else{
16    // Setter pronomen i utskriften til "henne" hvis hunden ikke er hunkjønn
17    pronomen = "hans";
18  }
19  
20  // Lager ei løkke for å gå gjennom yndlingsmaten til hver hund
21  for(const mat of hund.yndlingsmat){
22  
23    if(hund.yndlingsmat.length - 2 > i){
24      // Setter inn komma mellom elementene i utskriften  
25      // for alle unntatt de siste to elementene i lista
26      yndlingsmat += `${mat}, `;
27      i++;
28    }
29    else if(hund.yndlingsmat.length - 1 > i){
30      // Setter inn nest siste element uten komma
31      yndlingsmat += `${mat} `;
32      i++;
33    }else{
34      // Setter inn "og" foran siste element
35      yndlingsmat += `og ${mat}`;
36      i++;
37    }
38
39  }
40
41  // Skriver ut til konsollen
42  console.log(`${hund.navn} er en ${hund.farge} ${hund.rase}\
43  eid av ${hund.eier.navn}. \nYndlingsmaten ${pronomen} er ${yndlingsmat}.`)
44  // Tips: \n i console.log gir linjeskift i konsollutskriften
45
46  // Nullstiller teller og utskift av yndlingsmat 
47  // før neste gjennomkjøring av løkka
48  i = 0;
49  yndlingsmat = "";
50  
51}
```



Da blir utskriften slik:

##### CONSOLE

```bash
1Fido er en svart skotsk terrier eid av Rebecca Thomasen. 
2Yndlingsmaten hans er fiskepudding, griseøre og hundemat.
3
4King er en brun dvergpuddel eid av Gabrielle Martin. 
5Yndlingsmaten hans er pasta og loff.
6
7Bella er en blond boxer eid av Jakob Nilsen. 
8Yndlingsmaten hennes er biff og hundemat.
```