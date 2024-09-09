---
title: Sette opp Github-bruker og bruke Github med VS Code og Github Classroom
date: 09-08-2024
feed: show
---

## 1. Opprette en GitHub-konto
1. **Gå til GitHubs nettsted:**
   - Åpne nettleseren din og gå til [https://github.com](https://github.com).

2. **Klikk på "Sign up" (Registrer deg):**
   - Du finner denne knappen øverst til høyre på siden.

3. **Fyll ut registreringsskjemaet:**
   - Skriv inn e-postadressen din, opprett et brukernavn, og et sterkt passord.
   - Følg instruksjonene for å verifisere at du ikke er en robot.

4. **Velg plan:**
   - GitHub tilbyr både gratis og betalte planer. Velg den planen som passer best for dine behov (den gratis planen er ofte tilstrekkelig for personlig bruk).

5. **Bekreft e-posten din:**
   - GitHub vil sende en bekreftelses-e-post til adressen du oppga. Åpne e-posten og følg instruksjonene for å bekrefte kontoen din.

## 2. Installere Git på Windows
1. **Last ned Git:**
   - Gå til [https://git-scm.com](https://git-scm.com) og klikk på "Download for Windows".

2. **Installer Git:**
   - Åpne den nedlastede filen for å starte installasjonsprosessen.
   - Under installasjonen kan du velge standardinnstillinger, eller tilpasse installasjonen etter behov. Det anbefales å beholde standardinnstillingene, med unntak av:
     - Når du kommer til valget for "Adjusting your PATH environment", velg "Git from the command line and also from 3rd-party software".

3. **Fullfør installasjonen:**
   - Følg resten av instruksjonene for å fullføre installasjonen.
   - Når installasjonen er ferdig, kan du åpne Git Bash (installeres sammen med Git) for å sjekke at Git er installert korrekt ved å skrive `git --version` og trykke Enter.

## 3. Installere Visual Studio Code (VS Code)
1. **Last ned VS Code:**
   - Gå til [https://code.visualstudio.com](https://code.visualstudio.com) og klikk på "Download for Windows".

2. **Installer VS Code:**
   - Åpne den nedlastede filen og følg installasjonsinstruksjonene.
   - Under installasjonen kan du velge om du vil legge til VS Code i systemets PATH, noe som gjør det lettere å åpne VS Code fra kommandolinjen.

3. **Åpne VS Code:**
   - Etter installasjonen kan du åpne VS Code fra Start-menyen eller skrivebordet.

## 4. Konfigurere Git i VS Code
1. **Åpne Terminalen i VS Code:**
   - Åpne VS Code, og klikk på "Terminal" > "New Terminal" i menyen.

2. **Konfigurer Git med dine GitHub-detaljer:**
   - Skriv inn følgende kommandoer i terminalen for å konfigurere brukernavn og e-postadresse:
     ```bash
     git config --global user.name "Ditt Brukernavn"
     git config --global user.email "din-epost@eksempel.com"
     ```

3. **Installer GitHub-utvidelsen i VS Code:**
   - Klikk på "Extensions"-ikonet på venstre side i VS Code.
   - Søk etter "GitHub" og installer den offisielle GitHub-utvidelsen. Dette vil gi deg ekstra funksjonalitet for å jobbe med GitHub-repositorier direkte i VS Code.

## 5. Bruke GitHub i VS Code via Version Control-menyen
1. **Koble VS Code til GitHub:**
   - I VS Code, klikk på "View" > "Command Palette" (eller trykk `Ctrl + Shift + P`).
   - Skriv inn `GitHub: Sign in` og følg instruksjonene for å logge inn på din GitHub-konto. Dette gjør at du kan arbeide direkte med GitHub-repositorier i VS Code.

2. **Klone en oppgave fra GitHub Classroom:**
   - Gå til GitHub Classroom-nettsiden hvor læreren har delt oppgaven.
   - Finn oppgaven og klikk på "Accept" for å generere ditt personlige repository.
   - Når repositoriet er opprettet, vil du se en knapp med teksten "Go to repository". Klikk på den, og kopier URL-en fra repositoriet (under "Code" > "HTTPS").

3. **Klone repositoriet i VS Code:**
   - Åpne VS Code. Klikk på "Source Control"-ikonet på venstre side (ser ut som en gren med tre punkter).
   - Klikk på "Clone Repository" øverst i menyen.
   - Lim inn URL-en du kopierte fra GitHub Classroom, og trykk Enter.
   - Velg en mappe på datamaskinen hvor du vil lagre prosjektet, og VS Code vil automatisk klone repositoriet til denne mappen.

4. **Arbeide med oppgaven:**
   - Etter kloningen vil prosjektmappen åpnes automatisk i VS Code.
   - Du kan nå begynne å lage, redigere og lagre filer som en del av oppgaven.

5. **Commit endringer:**
   - Når du har gjort endringer, vil du se et nummer ved siden av "Source Control"-ikonet som indikerer antall endrede filer.
   - Klikk på "Source Control"-ikonet, skriv en beskrivende commit-melding i tekstfeltet øverst (for eksempel "Ferdig med oppgave 1"), og klikk deretter på "✔ Commit"-knappen for å lagre endringene lokalt.

6. **Push endringene til GitHub:**
   - Etter å ha committed endringene lokalt, klikker du på de tre prikkene (...) øverst i Source Control-menyen.
   - Velg "Push" fra rullegardinmenyen for å sende endringene dine til GitHub.
   - Nå vil læreren din kunne se endringene du har gjort i oppgaven din på GitHub.

7. **Trekke inn oppdateringer (Pull):**
   - Hvis læreren eller medelever gjør endringer i repositoriet, kan du hente disse ved å klikke på "Pull"-knappen (tre prikker > "Pull") for å oppdatere prosjektet ditt med de nyeste endringene.

## 6. Ytterligere tips
- **Bruk branching**: Før du gjør større endringer, kan det være lurt å lage en ny gren (branch) for å holde hovedgrenen (main) ren.
- **Merge og pull requests**: Hvis du jobber i team, kan du bruke pull requests for å foreslå endringer som andre kan gjennomgå før de blir merget inn i hovedgrenen.
