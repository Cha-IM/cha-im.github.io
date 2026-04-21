---
title: Vite-vanilla
feed: show
date: 07-04-2026
---

Vite-Vanilla er et rammeverk som ligner veldig på vanlig "vanilla" JavaScript, HTML og CSS, men du har fordelen at du kan importere tilleggsfunksjoner med NPM.

For å opprette et prosjekt med Vite-Vanilla åpner du en terminal og skriver:

```shell
npm create vite@latest .
```

Denne kommandoen oppretter et Vite-prosjekt i mappen du står i. Når du har kjørt denne kommandoen får du noen spørsmål:

1.  Hvis mappen din ikke er tom (f.eks. om du har klonet et Github-repo) får du spørsmålet: *Current directory is not empty. Please choose how to proceed.* Da velger du: *Ignore files and continue*
2. *Select a framework*. Velg *Vanilla*.
3. *Select a variant*. Velg *JavaScript*.
4. *Install with NPM and start now?* Velg *Yes*

### Lokal webserver
Vite vil starte en lokal webserver på localhost der du kan se endringer du gjør på websiden direkte. Webserveren vil automatisk starte på nytt ved behov, så du kan bare la den kjøre. Om du trenger å starte webserveren på nytt, lukker du den ved å trykke <kbd>Ctrl</kbd> + <kbd>C</kbd>, og starter den på nytt ved å skrive
```shell
npm run dev
```

### Lage et blankt prosjekt
Nå har du satt opp Vanilla-prosjektet ditt. For å starte med et blankt prosjekt følger du disse stegene:
1. Slett *counter.js* i src-mappen.
2. Åpne *main.js* og slett alt innholdet unntatt første linje (`import ./style.css`)
3. (valgfritt) Åpne *style.css* og slett alt innholdet hvis du vil lage din egen CSS.

Du kan nå redigere HTML-koden i *index.html* og skrive JavaScript-kode i *main.js*, som i et vanlig HTML/CSS/JS-prosjekt.

Om du trenger å opprette flere html-dokumenter, kan du opprette dem i rotmappen, ved siden av *index.html*. CSS- og JS-filer oppretter du i */src*-mappen, og bilder og andre mediefiler legger du i */src/assets*-mappen.---