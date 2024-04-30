---
title: Endre CSS-koden til bloggen din
feed: show
date: 29-04-2024
---
CSS-koden i Jekyll er ofte skjult, slik at man ikke skal kunne endre på temaet uten at man vet hva man holder på med. Nå skal vi finne CSS-filene og legge dem inn i bloggen vår slik at vi kan endre dem.

Åpne en terminal i VS Code og skriv koden

```sh
bundle info --path minima
```

Du vil nå få opp filbanen til *minima*-temaet i Jekyll. Finn denne mappen i filutforskeren på datamaskinen din (hold inn <kbd>ctrl</kbd>/<kbd>cmd</kbd> og klikk på filbanen eller kopier filbanen og lim det inn i et utforsker-vindu). Du vil da få opp alle filene som hører til temaet. Vi skal kopiere CSS-filene inn i bloggen vår.

Dra mappen *_sass* inn i VS Code, slik at den blir kopiert inn i mappen til bloggen din.
I denne mappen ligger det en .scss-fil, og en mappe som inneholder tre .scss-filer, 
![](https://github.com/Cha-IM/cha-im.github.io/blob/main/assets/img/jekyll/jekyll-sass-files.png?raw=true)

