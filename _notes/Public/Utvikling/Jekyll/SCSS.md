---
title: SCSS
feed: show
date: 29-04-2024
---
SCSS er en utvidelse av CSS som har noen flere funksjoner enn vanlig CSS. SCSS er stort sett leselig for deg om du kan vanlig CSS, men det er noen forskjeller.
## 1. Variabler
SCSS støtter variabler, slik at det er mulig å forhåndsbestemme en del egenskaper i CSS-koden din. F.eks kan du sette en fast fargepalett som defineres med navn i stedet for fargekoder. Verdier som størrelse på elementer og tekst er også nyttig å lagre som variabler.

Her er et eksempel på hvordan variabler gjør koden enklere. Se på denne CSS-koden:
```css
.header {
    background-color: #ff6347;
    color: white;
}

.footer {
    background-color: #ff6347;
    color: white;
}
```

Hvis vi skal endre bakgrunnsfargen, må vi endre den både i .header og .footer. I SCSS kan vi bruke variabler for å gjøre dette enklere:
```scss
$theme-color: #ff6347;
$text-color: white;

.header {
    background-color: $theme-color;
    color: $text-color;
}

.footer {
    background-color: $theme-color;
    color: $text-color;
}
```

Her har vi definert bakgrunnsfarge og skriftfarge som variabler. Om vi skal endre fargetema senere, trenger vi bare å endre verdien til variabelen, i stedet for å finne alle steder der vi har definert fargene.
## 2. Nøsting 
SCSS støtter nøstede CSS-regler, som vil si at vi kan ha regler inne i regler. Dette kan gjøre koden lettere å forstå.

Se på denne CSS-koden:
```CSS
.navbar {
    background-color: #333;
}

.navbar ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}

.navbar li {
    float: left;
}

.navbar li a {
    display: block;
    color: white;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
}
```

Denne koden kan skrives slik i SCSS:
```scss
.navbar {
    background-color: #333;

    ul {
        list-style-type: none;
        margin: 0;
        padding: 0;
    }

    li {
        float: left;

        a {
            display: block;
            color: white;
            text-align: center;
            padding: 14px 16px;
            text-decoration: none;
        }
    }
}
```

SCSS gjør det lettere å forstå hvilke stiler som gjelder for hvilke elementer, siden de er gruppert sammen, på samme måte som de er i HTML
## 3. Mixins
Mixins i SCSS tilsvarer funksjoner. En mixin er en forhåndslagret kodesnutt som kan gjenbrukes i SCSS-regler.

Her er et eksempel på en CSS-kode som kan forenkles ved hjelp av Mixins:
```css
.button1 {
    background-color: blue;
    border-radius: 5px;
    color: white;
    padding: 10px;
}

.button2 {
    background-color: green;
    border-radius: 5px;
    color: white;
    padding: 10px;
}
```

I SCSS kan vi skrive denne koden slik:
```scss
@mixin button-styles($bg-color) {
    background-color: $bg-color;
    border-radius: 5px;
    color: white;
    padding: 10px;
}

.button1 {
    @include button-styles(blue);
}

.button2 {
    @include button-styles(green);
}
```

## Den viktigste forskjellen
Den viktigste forskjellen mellom CSS og SCSS er hvordan koden blir lest i nettleseren. Nettleseren kan lese CSS, men ikke SCSS. SCSS må derfor gjøres om til CSS før det kan leses av nettleseren, og derfor brukes SCSS bare i web-rammeverk som Jekyll, React, Next.js med flere. Når du bruker et rammeverk skjer oversettelsen fra SCSS til CSS automatisk, så du trenger ikke tenke på det. På samme måte som rammeverket gjør om .md-filer eller .jsx-filer til html, blir .scss-filer gjort om til .css-filer.