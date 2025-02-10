---
title: Sette opp gjestekonto på en Windows 11-maskin
feed: show
date: 06-02-2025
---
![](/assets/img/nettverkslab/guestlogin.png)
*Bilde generert av Microsoft Copilot*

Hvis vi vil tillate at gjester kan bruke datalaben, eller at elever kan bytte plass på ulike prosjekter, må vi sette opp gjestekontoer, slik at alle kan bruke hvilken som helst datamaskin uten å endre innstillinger eller få tilgang til filene til den som sitter på plassen til vanlig.

Det er to måter å gjøre dette, avhengig av om datamaskinen er meldt inn i et Windows Server-domene (AD) eller ikke. Under er det guider for begge metodene. Velg den metoden som passer for ditt oppsett.

---
### Innhold
1. **Sette opp en gjestekonto uten passord på en vanlig Windows 11-klient (ikke meldt inn i et domene)**
2. **Sette opp en gjestekonto uten passord på en Windows 11-klient meldt inn i et Windows Server domene**

---
![](/assets/img/nettverkslab/guestaccount.png)
*Bilde generert av Microsoft Copilot*

### 1: Sette opp en gjestekonto uten passord på en vanlig Windows 11-klient (ikke meldt inn i et domene)

1. **Åpne Innstillinger**:
    
    - Trykk på **Windows-tasten** og velg **Innstillinger** fra Start-menyen.
2. **Naviger til Kontoer**:
    
    - Velg **Kontoer** fra Innstillinger-menyen.
3. **Familie og andre brukere**:
    
    - Klikk på **Familie og andre brukere** i venstre sidepanel.
4. **Legg til en annen bruker**:
    
    - Under **Andre brukere**, klikk på **Legg til konto**.
5. **Ingen påloggingsinformasjon**:
    
    - Velg **Jeg har ikke denne personens påloggingsinformasjon** når systemet spør etter e-post eller telefonnummer.
6. **Legg til en bruker uten Microsoft-konto**:
    
    - Velg **Legg til en bruker uten en Microsoft-konto** og følg instruksjonene for å sette opp brukernavn. La passordfeltene stå tomme.
7. **Fullfør oppsettet**:
    
    - Etter å ha opprettet kontoen, vil gjestene kunne logge inn med begrenset tilgang. De kan bruke internett og applikasjoner, men vil ikke kunne se dine personlige filer eller endre systeminnstillinger
8. **Logg inn på gjestekontoen**:
    
    - Gå til **Start-menyen**, klikk på brukerkontoikonet øverst til venstre, og velg gjestekontoen. Klikk på **Logg inn** uten å skrive inn et passord.

---
### 2: Sette opp en gjestekonto uten passord på en Windows 11-klient meldt inn i et Windows Server domene

1. **Åpne Active Directory-brukere og datamaskiner**:
    
    - Logg inn på serveren og åpne **Active Directory-brukere og datamaskiner** fra administrasjonsverktøyene.
2. **Opprett en ny bruker**:
    
    - Høyreklikk på den relevante OU (Organizational Unit) og velg **Ny** > **Bruker**.
3. **Fyll ut brukeropplysninger**:
    
    - Fyll ut nødvendig informasjon som fornavn, etternavn og påloggingsnavn. For eksempel, brukernavn "Gjest".
4. **Sett passord**:
    
    - Angi et passord for gjestekontoen. Etter opprettelsen, høyreklikk på brukeren og velg **Egenskaper**. Gå til **Konto**-fanen og merk av for **Brukeren kan ikke endre passord** og **Passord utløper aldri**.
5. **Tillat tomt passord**:
    
    - Åpne **Lokal sikkerhetspolicy** på klientmaskinen ved å trykke **Windows-tasten + R**, skriv `secpol.msc` og trykk **Enter**.
    - Gå til **Lokale retningslinjer** > **Sikkerhetsalternativer**.
    - Finn og deaktiver policyen **Kontoer: Begrens bruk av tomme passord til kun konsollpålogging**.
6. **Fjern passordet**:
    
    - Gå tilbake til **Active Directory-brukere og datamaskiner**, høyreklikk på gjestebrukeren, velg **Tilbakestill passord**, og la passordfeltene stå tomme. Klikk **OK**.
7. **Legg til i gruppen "Gjest"**:
    
    - Høyreklikk på brukeren og velg **Legg til i en gruppe**. Skriv inn **Gjest** og klikk **OK**.
8. **Konfigurer gruppepolicyer**:
    
    - Åpne **Gruppepolicy Management** og opprett en ny GPO (Group Policy Object) for gjestekontoen. Konfigurer policyer for å begrense tilgang til systeminnstillinger og filer.
9. **Tildel GPO til OU**:
    
    - Link den nye GPO-en til den OU hvor gjestekontoen er plassert.
10. **Logg inn på gjestekontoen**:
    
    - På klientmaskinen, gå til **Start-menyen**, klikk på brukerkontoikonet øverst til venstre, og velg gjestekontoen. Klikk på **Logg inn** uten å skrive inn et passord

Håper dette hjelper! Hvis du har flere spørsmål, er det bare å spørre læreren. 😊

### Kilder
[1] [How to Set Up a Guest Account on Windows 11: A Step-by-Step Guide](https://www.solveyourtech.com/how-to-set-up-a-guest-account-on-windows-11-a-step-by-step-guide/)

[2] [How to Create a User Account Without Password in Windows 10 and 11](https://windowsloop.com/create-user-account-without-password/)

[3] [Allow Anonymous Access to Shared Folder or Printer on Windows](https://woshub.com/anonymous-access-shared-folders-printers-windows/)