---
title: Installere Windows Server
feed: show
date: 06-11-2025
---

## Steg 1: Hent ISO fil fra Azure
Gå til [Azure](https://azure.com) og logg inn med din Chamedia.no bruker.
Naviger til Education -> Learning Resources -> Software og finn 'Windows Server 2025'.
Last ned denne versjonen av Windows Server.

## Steg 2: Last ned Rufus
Gå til [Rufus](https://rufus.ie/nb/#download) og last ned nyeste versjonen av Rufus.

## Steg 3: Legg til ISO filen til en USB
1. Sett en USB penn i PC'en din.
2. Åpne Rufus.
3. I Rufus velger du USB pennen din som Enhet.
4. Under 'oppstartstype' trykker du på VELG.
5. Finn ISO filen du lastet ned og velg denne.
6. Bildevalg skal stå på Standard Windows installasjon.
7. Under format-valg. Så gir du navn til din USB under Volumnavn. Vi kaller den 'Windows Server 2025'.
8. Trykk på start. Da kommer det noen ekstra valg. Disse 2 skal være på: 'Fjern krav om 4gb+ ram, Secure boot og TPM 2.0' og 'Fjern krav om Microsoft konto'. Trykk så på OK. Får du en feilmelding så trykker du bare på OK igjen.

Rufus vil nå lage en oppstartsbar installasjonsmedium for Windows Server 2025.

## Steg 4: Installere Windows Server 2025
1. Sett USB pennen inn i servermaskinen din.
2. Start datamaskinen og kom deg inn i boot menu. Denne knappen er forskjellig for forskjellige produsenter. Men siden dette er en HP datamaskin så er det ESC eller F9. Fungerer ingen av disse; så prøver du F10, F11 og F12.
3. Når boot menu er oppe, så velger du USB pennen med Windows Server 2025.
4. Følg instruksene videre. Helt til du får velge hvilken versjon du vil installere. Her velger du 'Windows Server 2025 Standard (Desktop Experience)'.
5. Trykk deg så videre til du kommer til Installasjonstype. Der velger du Custom: 'Install Windows only (advanced)'
6. Når du får opp listen med partisjoner, så velger vi å slette alle partisjoner. Du må velge en og en partisjon og trykke på 'Delete'. Den bruker litt tid på å slette hver enkelt partisjon, så når du trykker på Delete så venter du litt til du ser at den er slettet, så sletter du neste helt til du har slettet alle partisjonene. 
7. Til slutt sitter du med en disk igjen på listen som heter: 'Drive 0 Unallocated Space'. Denne velger du og trykker så på 'New'. Så velger du størrelsen på denne nye partisjonen. Vi velger å bruke hele disken.
8. Da ser du at det har kommet en del nye partisjoner på lsiten din. Finn den som har typen: 'Primary' og trykk Next.
9. Følg instruksene videre.
## Gratulerer, du har installert Windows Server 2025!