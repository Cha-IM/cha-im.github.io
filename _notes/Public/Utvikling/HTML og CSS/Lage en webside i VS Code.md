---
title: Lage en webside i VS Code
feed: show
date: 19-09-2024
---

### 1. **Installer VS Code**
Last ned og installer VS Code fra [Visual Studio Code sin nettside](https://code.visualstudio.com/).

### 2. **Opprett en mappe for prosjektet**
Opprett en ny mappe på datamaskinen som vil inneholde prosjektfilene dine. Gi den et beskrivende navn, som for eksempel `MinWebside`.

### 3. **Åpne mappen i VS Code**
1. Åpne VS Code.
2. Gå til **File** > **Open Folder** (Fil > Åpne mappe).
3. Finn mappen du nettopp opprettet (for eksempel `MinWebside`) og klikk **Select Folder**.

### 4. **Opprett HTML- og CSS-filer**

#### Opprett en HTML-fil:
1. I filutforskeren på venstre side i VS Code, høyreklikk på mappen og velg **New File**.
2. Navngi filen `index.html`.
3. Skriv `!` i filen og trykk **Enter** for å automatisk generere grunnstrukturen for en HTML-side.
4. Legg deretter manuelt til en link til CSS-filen i `<head>`-seksjonen:
```html
<link rel="stylesheet" href="style.css">
```

Dette vil sørge for at HTML-filen er koblet til CSS-filen.

#### Opprett en CSS-fil:
1. Høyreklikk på mappen igjen og velg **New File**.
2. Navngi filen `style.css`.
3. Legg til grunnleggende CSS-stiler:
```css
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
}

h1 {
    color: #333;
    text-align: center;
    padding: 20px;
}
```

### 5. **Bruke GitHub via Source Control-menyen**
For å integrere prosjektet ditt med GitHub via Source Control-menyen i VS Code:

1. **Klon GitHub Classroom-repositoriet**:
   - Åpne GitHub Classroom-lenken som læreren din har delt, og følg trinnene for å opprette ditt eget repositorium.
   - Kopier GitHub-repositoriets URL.

2. **Klon repositoriet i VS Code**:
   - Åpne VS Code.
   - Klikk på **Source Control**-ikonet (ser ut som en gren med en node) på venstre side.
   - Klikk på **Clone Repository** og lim inn GitHub-repositoriets URL.
   - Velg hvor du vil lagre prosjektet på din lokale maskin.

3. **Jobb med prosjektet**:
   - Når du har klonet repositoriet, kan du legge til HTML- og CSS-filene i prosjektmappen.

4. **Commit og push endringer til GitHub**:
   - Etter å ha gjort endringer i filene, gå til **Source Control**-panelet.
   - Skriv en kort beskrivelse av endringene dine i feltet.
   - Klikk på **Commit**-knappen (✓).
   - Klikk deretter på **Push** for å laste opp endringene til GitHub.

### 6. **Se nettsiden din**
For å se nettsiden lokalt mens du jobber med den, kan du bruke **Live Preview**-utvidelsen i VS Code:
1. Installer **Live Preview** fra **Extensions**-panelet.
2. Høyreklikk på `index.html` og velg **Show preview**.

Nå er du klar til å bygge websideprosjektet ditt og jobbe med GitHub Classroom via VS Code!