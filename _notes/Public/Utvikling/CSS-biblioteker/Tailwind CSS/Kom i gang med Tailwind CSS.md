---
title: Kom i gang med Tailwind CSS
feed: show
date: 10-09-2024
---

Her er en enkel steg-for-steg guide for å komme i gang med Tailwind CSS, inkludert hvordan du legger det til på en statisk nettside og bruker det til å style HTML-elementer.

## Steg 1: Opprett en enkel HTML-side
Start med en enkel HTML-fil som du kan bruke til å legge til Tailwind CSS og style elementer.

```html
<!DOCTYPE html>
<html lang="no">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Min Tailwind Nettside</title>
  <!-- Tailwind CSS -->
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body>
  <div class="container mx-auto">
    <h1 class="text-3xl font-bold text-center mt-10">Velkommen til Tailwind CSS!</h1>
    <p class="text-lg text-center mt-4">Dette er en enkel nettside stylet med Tailwind CSS.</p>
  </div>
</body>
</html>
```

### Forklaring:
- **`<link>`-taggen** legger til Tailwind CSS fra et CDN (Content Delivery Network), slik at du kan begynne å bruke det uten å installere noe lokalt.
- I dette eksempelet har vi lagt til noen grunnleggende Tailwind-klasser for å style teksten i `<h1>` og `<p>`-elementene.

## Steg 2: Legg til Tailwind CSS via CDN
Vi bruker et CDN (som er en server som gjør Tailwind tilgjengelig på nett) for å enkelt inkludere Tailwind i prosjektet.

1. **Legg til denne linjen i `<head>`-delen av HTML-filen**:
   ```html
   <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
   ```
   Dette gjør at du får tilgang til alle Tailwind CSS-klasser på nettsiden din uten å måtte laste ned noe.

## Steg 3: Bruk Tailwind CSS til å style nettsiden
Tailwind CSS er basert på utility-first-klasser, som betyr at du kan bruke små, enkle CSS-klasser direkte på HTML-elementene dine for å style dem.

### Eksempler på styling:

1. **Endre tekststørrelse og farge**:
   - `text-3xl`: Setter skriftstørrelsen til "extra large".
   - `text-center`: Sentraliserer teksten.
   - `text-lg`: Setter skriftstørrelsen til "large".
   - `font-bold`: Gjør teksten fet.
   - `text-blue-500`: Setter tekstfargen til en blå nyanse.

2. **Legg til margin og padding**:
   - `mt-10`: Gir et "margin-top" på 10 enheter.
   - `px-4`: Gir horisontal padding på 4 enheter (padding left + right).
   - `py-2`: Gir vertikal padding på 2 enheter (padding top + bottom).

### Eksempel på hvordan du kan bruke disse klassene:

```html
<h1 class="text-3xl font-bold text-blue-500 text-center mt-5">Tailwind CSS er kult!</h1>
<p class="text-lg text-gray-700 text-center mt-2">Nå kan du enkelt style elementer med Tailwind.</p>
```

## Steg 4: Legg til flere HTML-elementer og style dem
Tailwind gjør det enkelt å style flere elementer raskt. Her er et eksempel der vi legger til en knapp med Tailwind-styling:

```html
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mt-5 mx-auto block">
  Klikk meg
</button>
```

### Forklaring:
- **`bg-blue-500`**: Setter bakgrunnsfargen til blå.
- **`hover:bg-blue-700`**: Endrer bakgrunnsfargen til en mørkere blå når du holder musepekeren over knappen.
- **`text-white`**: Gjør teksten hvit.
- **`font-bold`**: Gjør teksten fet.
- **`py-2 px-4`**: Gir vertikal padding på 2 enheter og horisontal padding på 4 enheter.
- **`rounded`**: Gjør knappens hjørner avrundet.
- **`mx-auto block`**: Sentraliserer knappen på skjermen.

## Steg 5: Lagre og test nettsiden
Når du har gjort endringer i HTML-filen din, lagrer du filen og åpner den i en nettleser for å se resultatet. Du vil nå se at Tailwind CSS-stylingen har blitt anvendt på nettsiden din.

## Eksempel på en komplett nettside:

```html
<!DOCTYPE html>
<html lang="no">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Min Tailwind Nettside</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-100">
  <div class="container mx-auto p-10">
    <h1 class="text-4xl font-bold text-center text-blue-500">Velkommen til Tailwind CSS!</h1>
    <p class="text-lg text-center mt-5 text-gray-700">Nå kan du style nettsiden din raskt og enkelt med Tailwind CSS.</p>

    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mt-10 mx-auto block">
      Klikk meg
    </button>
  </div>
</body>
</html>
```

Med disse enkle stegene kan du begynne å bruke Tailwind CSS til å style statiske nettsider!