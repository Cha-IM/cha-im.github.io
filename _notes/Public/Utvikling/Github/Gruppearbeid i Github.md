---
title: Gruppearbeid i Github
feed: show
date: 19-03-2024
tags:
---

Når flere jobber sammen i et repo i Github er det flere ting man må tenke på.

## Github synkroniserer ikke automatisk
For at ditt arbeid skal vises for de andre på gruppa må du *pushe* endringene dine til Github. Husk å **lagre** filene dine før du pusher, slik at alle endringene blir med.

Når du har pushet må de andre på gruppa *pulle* siste versjon av repoet for å få oppdatert filene de jobber i.

### Synkroniseringskonflikter.

Når du arbeider med Git og GitHub i et prosjekt, kan det oppstå situasjoner der flere personer gjør endringer i de samme filene, og når du prøver å slå sammen disse endringene, kan det oppstå en merge-konflikt. En merge-konflikt oppstår når Git ikke automatisk kan slå sammen filene, fordi det er forskjellige endringer på de samme linjene eller nær hverandre. Her er en steg-for-steg guide for hvordan du kan løse en merge-konflikt i GitHub via VS Code:

### 1. Oppdag konflikten
Når du prøver å slå sammen en branch (for eksempel via `git pull`, `git merge`, eller `git rebase`), og det oppstår en konflikt, vil Git stoppe operasjonen og vise en melding om at det er konflikter som må løses før du kan fortsette.

### 2. Se konflikten i VS Code
- Åpne prosjektet ditt i VS Code.
- I "Source Control"-panelet (venstre side med ikonet som ser ut som en gren), vil du se at det står at det er "Merge Conflicts".
- Filene med konflikter vil være markert, og du kan klikke på hver fil for å se hvor konfliktene er.

### 3. Forstå konfliktmarkeringene
Når du åpner en fil med en konflikt i VS Code, vil du se at konfliktområdene er markert slik:

```plaintext
<<<<<<< HEAD
Her er det som finnes i din lokale branch.
=======
Her er det som finnes i branchen du prøver å slå sammen med.
>>>>>>> branch-name
```

- **`<<<<<<< HEAD`**: Dette representerer endringene i din lokale branch (den du jobber på).
- **`=======`**: Dette er separatoren som skiller de to konfliktområdene.
- **`>>>>>>> branch-name`**: Dette representerer endringene fra branchen du prøver å slå sammen med.

### 4. Velge hvordan konflikten skal løses
VS Code gir deg flere alternativer for hvordan du kan løse konflikten:

- **Accept Current Change**: Beholder din lokale versjon (`HEAD`).
- **Accept Incoming Change**: Beholder den andre versjonen (branchen du prøver å slå sammen med).
- **Accept Both Changes**: Beholder begge endringene, én etter den andre.
- **Compare Changes**: Viser en detaljert sammenligning mellom de to versjonene, slik at du kan bestemme manuelt hvilke endringer som skal beholdes.

### 5. Løs konflikten
- Velg det alternativet som passer best for situasjonen.
- Hvis ingen av de automatiske løsningene er riktig, kan du manuelt redigere filen for å kombinere endringene på en måte som gir mening.

### 6. Fjern konfliktmarkeringer
Når du har bestemt hvilke endringer som skal beholdes, fjern manuelt konfliktmarkeringene (`<<<<<<<`, `=======`, `>>>>>>>`) hvis de ikke forsvinner automatisk når du velger en løsning i VS Code.

### 7. Lagre filen
Etter å ha løst konflikten og redigert filen, lagre den.

### 8. Fullfør merge-prosessen
Når alle konflikter er løst og filene er lagret:
- Gå tilbake til "Source Control"-panelet i VS Code.
- Skriv inn en commit-melding som beskriver hva du gjorde (for eksempel "Løste merge-konflikt i `filnavn`").
- Klikk på "✔ Commit"-knappen for å bekrefte endringene.

### 9. Push endringene til GitHub
- Etter å ha committed endringene, klikk på de tre prikkene (...) i Source Control-panelet og velg "Push" for å sende endringene dine til GitHub.

### 10. Bekreft at konflikten er løst
Når du har pushet endringene til GitHub, kan du sjekke i GitHub-repositoriet ditt for å sikre at konflikten er løst, og at den oppdaterte koden er lastet opp riktig.

---

Ved å følge disse trinnene, kan du effektivt løse merge-konflikter i GitHub via VS Code, slik at prosjektet ditt kan fortsette uten problemer.