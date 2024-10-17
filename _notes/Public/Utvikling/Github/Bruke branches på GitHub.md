---
title: Bruke branches på GitHub
feed: show
date: 09-09-2024
---

Her er en guide for hvordan du kan bruke branches (grener) på GitHub.

### 1. **Hva er en branch?**
   - **En branch er en parallell versjon av prosjektet ditt**:
     - Når du jobber med en branch, kan du gjøre endringer uten å påvirke hovedversjonen (ofte kalt `main` eller `master`).
     - Branches er nyttige når du vil prøve ut nye funksjoner, fikse feil, eller jobbe på forskjellige deler av prosjektet samtidig.
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/b9LTz6joMf8?si=_m-rHd9Beb4zwg3e" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### 2. **Opprette en ny branch**
   - **Fra GitHub-nettstedet**:
     - Gå til repositoriet ditt på GitHub.
     - Klikk på rullgardinmenyen som viser `main` (eller `master`).
     - Skriv inn navnet på den nye branchen, for eksempel `new-feature` eller `styling-updates`.
     - Klikk på "Create branch" for å lage den nye branchen.
   - **Fra VS Code**:
     - Klikk på "Source Control"-ikonet.
     - Klikk på `main` eller `master` nederst i venstre hjørne.
     - Velg "Create new branch" og gi den et navn.
     - Nå vil VS Code automatisk bytte til den nye branchen.

### 3. **Bytte mellom branches**
   - **Fra GitHub-nettstedet**:
     - Gå til repositoriet ditt.
     - Klikk på rullgardinmenyen som viser `main` eller `master`, og velg den branchen du vil jobbe på.
   - **Fra VS Code**:
     - Klikk på `main` eller navnet på den nåværende branchen nederst i venstre hjørne.
     - Velg den branchen du vil bytte til fra listen.

### 4. **Gjøre endringer på en branch**
   - **Når du jobber på en branch, er endringene isolert fra andre branches**:
     - Du kan gjøre endringer i HTML- eller CSS-filer som vanlig.
     - Commit og push endringene til GitHub når du er ferdig.

### 5. **Sammenligne og slå sammen (merge) branches**
   - **Når du er ferdig med å jobbe på en branch, kan du slå den sammen med hovedbranchen**:
     - Gå til repositoriet ditt på GitHub.
     - GitHub vil ofte automatisk foreslå å slå sammen branchen din når du gjør en pull request (PR).
     - Klikk på "Compare & pull request"-knappen.
     - Skriv en kort beskrivelse av hva du har gjort, og klikk på "Create pull request".
     - Hvis det ikke er noen konflikter, klikk på "Merge pull request" for å slå sammen endringene dine med hovedbranchen.
   - **Fra VS Code**:
     - Klikk på `main` eller `master` nederst i venstre hjørne for å bytte tilbake til hovedbranchen.
     - Klikk på "Source Control"-ikonet og velg "Merge Branch".
     - Velg branchen du vil slå sammen med hovedbranchen.

### 6. **Håndtere merge-konflikter**
   - **Noen ganger kan det oppstå konflikter hvis to branches endrer de samme linjene i en fil**:
     - Hvis det skjer, vil GitHub eller VS Code be deg om å løse konflikten.
     - Åpne filen med konflikten, se på endringene, og bestem hvilken versjon som skal beholdes.
     - Når konflikten er løst, commit og push endringene.
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/HosPml1qkrg?si=BArgDq9YKVm1Dc4c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


### 7. **Slette en branch**
   - **Etter at en branch er slått sammen, kan den slettes**:
     - På GitHub, etter å ha slått sammen, vil du ofte få muligheten til å "Delete branch".
     - Dette er nyttig for å holde repositoriet ryddig.
   - **Fra VS Code**:
     - Klikk på `main` eller den nåværende branchen nederst i venstre hjørne.
     - Velg "Delete branch" fra menyen, og velg deretter hvilken branch du vil slette.

### 8. **Når skal du bruke en branch?**
   - **Når du legger til en ny funksjon**: Opprett en branch for å jobbe med en ny funksjon uten å påvirke det som allerede fungerer.
   - **Når du fikser en bug**: Lag en branch for å fikse en feil, slik at du kan jobbe på løsningen uten å påvirke hovedkoden.
   - **Når du eksperimenterer**: Prøv nye ideer på en egen branch for å se hvordan de fungerer uten risiko for å ødelegge noe.

Ved å bruke branches, kan du og gruppen din jobbe på ulike deler av prosjektet samtidig uten å tråkke hverandre på tærne. Det hjelper også med å holde hovedversjonen av koden stabil og fungerende.

## Pull requests
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/LdSwWxVzUpo?si=9Zs5sYInCiCnR_jw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
