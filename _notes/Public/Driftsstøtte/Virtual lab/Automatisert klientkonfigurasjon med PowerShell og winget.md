---
title: Automatisert klientkonfigurasjon med PowerShell og winget
feed: show
date: 02-11-2026
---


## Oppgave
### Automatisering, skripting, klientadministrasjon i Windows 11

Som IT-tekniker i en bedrift vil du sjeldent bruke tid på å klikke deg gjennom manuelle installasjonsprogrammer eller opprette brukere manuelt på nye maskiner. Standardisering og automatisering sparer tid, sikrer lik oppsett og reduserer sjansen for feil.

I denne oppgaven skal du lage et PowerShell-skript som automatisk klargjør en Windows 11-klient for en nyansatt utvikler. Skriptet skal opprette en ny lokal brukerkonto og installere nødvendig programvare automatisk via **Windows Package Manager (`winget`)**.


## Krav til skriptet (`klargjoering.ps1`)

Skriptet ditt skal kjøres som **Administrator** i PowerShell på din Windows 11-VM og utføre følgende tre hoveddeler:


### Del 1: Opprette ny lokal brukerkonto

1. Sjekke om brukeren `utvikler1` finnes fra før.
2. Opprette brukeren `utvikler1` med et sikkert engangspassord dersom den ikke eksisterer.
3. Legge brukeren inn i den lokale `Users`-gruppen.

### Del 2: Automatisk programvareinstallasjon (`winget`)

Skriptet skal installere følgende verktøy uten at brukeren må klikke på "Neste/Next" i installasjonsveiviserne (lydløs/silent installasjon):


- **Utviklerverktøy:** Visual Studio Code (`Microsoft.VisualStudioCode`)
- **Nettverksverktøy:** Wireshark (`WiresharkFoundation.Wireshark`)
- **Nettleser:** Google Chrome (`Google.Chrome`) eller Mozilla Firefox (`Mozilla.Firefox`)
- **Nytteverktøy:** 7-Zip (`7zip.7zip`)

> **Tips til winget-flagg:**
> For å kjøre installasjonene helt automatisk uten dialogbokser eller lisensspørsmål, bruker du flaggene:
> 
> `--silent --accept-source-agreements --accept-package-agreements`

### Del 3: Brukergrensesnitt og tilbakemelding

1. Skriptet skal skrive ut ryddige meldinger i konsollen underveis (f.eks. ved bruk av `Write-Host` med farger) som viser status på hvert steg.
2. Skriptet skal avslutte med en oppsummering som bekrefter at klargjøringen er ferdig.

##  Ekstrautfordringer (For deg som blir fort ferdig)

Velg én eller flere av følgende utvidelser for å heve skriptet ditt:

- **Loggføring:** La skriptet skrive alle handlinger og tidsstempler til en tekstfil (f.eks. `C:\Logs\klargjoering.log`).
- **Sjekk av Administrator-rettigheter:** Legg til en sjekk i starten av skriptet som stopper kjøringen med en feilmelding dersom skriptet _ikke_ kjøres som Administrator.
- **Dynamiske parametere:** Gjør det mulig å sende inn brukernavnet som et argument når skriptet kjøres (f.eks. `.\klargjoering.ps1 -Brukernavn "ola.nordmann"`).


##  Nyttige kommandoreferanser

```powershell
# Sjekke om brukerkonto finnes, lagre true eller false i en variabel
$EksisterendeBruker = Get-LocalUser -Name "utvikler1" -ErrorAction SilentlyContinue

# Opprette ny lokal bruker
$Password = ConvertTo-SecureString "Sommer2026!" -AsPlainText -Force
New-LocalUser -Name "utvikler1" -Password $Password -FullName "Ny Utvikler" -Description "Klargjort via skript"

# Søke etter pakke med winget
winget search "visual studio code"

# Installere pakke silent med winget
winget install --id Microsoft.VisualStudioCode --silent --accept-source-agreements --accept-package-agreements
```

