---
title: Slett et element fra en array
feed: show
date: 21-05-2024
---

Det er to hovedmetoder for å slette et element fra en liste, avhengig av om du vil slette indexen til elementet eller ikke, *array.splice()* eller *delete*.

## array.splice()

Hvis vi har denne listen:
```js
const array = ["1", "2", "3", "4", "5"];
```
og vil fjerne elementet med index 3, skriver vi
```js
array.splice(3, 1);
```

Elementet med index 3 (det fjerde elementet i lista) vil nå fjernes helt, og elementene etter vil få nye indexer. Dette blir den nye listen
```js
["1", "2", "3", "5"]
```

## delete
Hvis vi vil fjerne elementet i listen med index 3, men beholde samme index på elementene som kommer etter det fjernede elementet må vi bruke *delete*, slik
```js
const array = ["1", "2", "3", "4", "5"];

delete array[3]
```

Elementet vil da bli satt som undefined i listen, og de resterende elementene beholder sin index. Listen ser da slik ut:
```js
["1", "2", "3", undefined, "5"]
```