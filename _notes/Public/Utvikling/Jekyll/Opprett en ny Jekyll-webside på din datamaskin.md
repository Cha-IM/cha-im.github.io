---
title: Opprett en ny Jekyll-webside på din datamaskin
feed: show
date: 22-04-2024
---
1. Åpne Visual Studio Code, og åpne en ny, tom mappe.
2. Åpne et terminalvindu ved å klikke på *Terminal* på menyen øverst på skjermen, og så *New terminal*
3. Inne i terminalen skriver du denne koden (bytt ut `minblogg` med navnet på din blogg, uten mellomrom):
```shell
jekyll new minblogg
```
![](https://github.com/Cha-IM/cha-im.github.io/blob/main/assets/img/jekyll/jekyll-vs-code-installed.png?raw=true)
4. Du har nå opprettet en ny blogg, og du kan se at du har fått en ny mappe med bloggnavnet med filer i *Explorer*-vinduet i VS Code. Du må nå åpne mappa i terminalen med denne koden:
```shell
cd minblogg
```
- `cd` står for *change directory*, og betyr at vi går inn i mappen minblogg (hvis du kalte bloggen din noe annet i forrige steg, skriver du det i stedet for minblogg)
5. Til slutt skal du bygge bloggen din og gjøre den tilgjengelig for å åpnes i nettleseren. Dette gjøres ved å starte en lokal webserver (som bare er tilgjengelig for deg og din datamaskin). For å gjøre det skriver du denne koden i terminalen:
```sh
bundle exec jekyll serve
```
6. Nå kan du åpne bloggen din ved å åpne nettleseren og skrive adressen [localhost:4000](http://localhost:4000/)
7. Hvis du ønsker å stoppe webserveren, f.eks. hvis du har gjort endringer som krever at websiden lastes inn på nytt, klikker du inne i terminalen og trykker <kbd>ctrl + c</kbd> (Merk at dette er <kbd>ctrl</kbd>-tasten både på Mac og Windows, ikke <kbd>cmd</kbd> på Mac)

### Noen viktige ting å huske på
* Når vi bruker et rammeverk er de faktiske html-filene som utgjør nettsiden skjult for oss. Disse blir generert når vi bygger nettsiden ved hjelp av koden `bundle exec jekyll serve`, og eksisterer kun så lenge webserveren kjører. Derfor er den eneste måten å vise bloggen å bruke denne koden. Vi kan ikke bruke live preview-tillegget i VS-code for å vise noe av nettsiden.
* Den lokale webserveren vil kjøre helt til vi slår den av (<kbd>ctrl + x</kbd>)