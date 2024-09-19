---
title: CSS-velgere
feed: show
date: 19-09-2024
---
Det finnes tre hovedtyper CSS-velgere: _type_, _class_ og _id_. Eksempelet over er en typevelger. Typevelgere velger elementer basert på HTML-taggen. Under ser du eksempler på CSS-regler med typevelgere.

```css
body{
  font-family: Arial, Helvetica, sans-serif;
  background-color: black;
}

header{
  background-color: black;
  color: white;
  font-family: Arial black;
  font-size: 40px;
  text-align: center;
  height: 90vh;
}

main{
  width: 75%;
  margin: auto;
  background-color: white;
}
```


`body`, `header` og `main` angir CSS-regler for elementer i HTML-dokumentet med taggene `<body>`, `<header>` og `<main>`.

## Typevelgere, id-velgere og class-velgere gir større variasjon

![Nettsidedesign på en datamaskin i vinklet perspektiv. Ulike gjenstander rundt datamaskinen, blant annet et fotoapparat, ei klokke, en snakkeboble, ei lyspære, en blyant. Grafisk illustrasjon.](https://api.ndla.no/image-api/raw/artboard_4-utsnitt.png?width=1024)
Bilde: Sentavio / [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.no)

Om vi bare skulle bruke typevelgere, ville det begrense veldig hva vi kunne gjøre med utseendet på nettsiden, for alle elementer av samme type vil bli helt like. Men av og til vil vi at elementer av samme type skal se forskjellige ut og plasseres ulikt på nettsiden. Da trenger vi å kunne skille ut enkelte elementer på andre måter enn bare ved navnet på HTML-taggen. Det kan vi gjøre med _class_- og _id_-velgere.

_Class_ og _id_ er attributter til HTML-tagger og angis derfor inne i en HTML-tag, for eksempel slik:

`<p id=”ingress”>` eller `<img class=”miniatyrbilde” src=”bilde.jpg”>`

## Class og id

Forskjellen på class og id er at samme class kan brukes på flere elementer på samme nettside, men en id kan bare brukes en gang. Id brukes derfor på elementer som bare skal opptre en gang på nettsiden, som for eksempel hovedmeny, banner eller bunntekst, mens class brukes på elementer som gjentas, som bilder, knapper, lenker eller lister.

**Class-velgere** angis i CSS med et punktum foran navnet på klassen, slik:
```css
.miniatyrbilde{
  width: 50px;
  height: 50px;
}
```


**Id-velgere** angis i CSS med firkant-tegn foran navnet på klassen, slik:
```css
#ingress{
  font-size: 20px;
  font-style: italic;
}
```

## Interne lenker med id

![Skisse for web-design. Foto.](https://api.ndla.no/image-api/raw/3223200963_a10a35b583_o.jpg?width=1024)
Bilde: Aleksandar Urošević / [CC BY](https://creativecommons.org/licenses/by/4.0/deed.no)

Et annet bruksområde for id-attributtet er interne lenker i et dokument. Med interne lenker kan du lenke til spesifikke deler på nettsiden. Dette brukes mye i moderne web-design, der det er vanlig at hele nettstedet er spredt utover ett langt HTML-dokument. Interne lenker bruker id-en til et element til å få nettleseren til å automatisk skrolle til det elementet. Dette kan sammenlignes med innholdsfortegnelsen i et Word- eller PDF-dokument.

### Eksempel
```html
<a href=”#about”>Om oss</a>
```

Denne lenken vil gjøre at nettleseren automatisk skroller til elementet med `id=”about”`, for eksempel `<div id=”about”>`.


*Denne teksten er opprinnelig publisert på [ndla.no]([CSS-velgere - Konseptutvikling og programmering - NDLA](https://ndla.no/subject:1:1352b19e-e706-4480-a728-c6b0a57ba8ae/topic:1:f7b88f8c-5f2f-4ea8-bdcf-1bd4811c37b3/topic:1:df9278b0-7252-4a62-a39c-3107d7f319f1/resource:2e32dd04-efdd-4d73-ad07-10285e7b0c79))*