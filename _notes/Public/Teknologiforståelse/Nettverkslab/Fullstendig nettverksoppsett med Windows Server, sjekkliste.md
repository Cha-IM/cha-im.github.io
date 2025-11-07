---
title: Fullstendig nettverksoppsett med Windows Server, sjekkliste
feed: show
date: 05-11-2025
---

## Nødvendig utstyr
- 2 PC-er med skjerm, tastatur og mus (en klient og en server)
- Unifi router
- Unifi switch
- Minnepenn

## Programvare/filer
- Rufus (programvare for å lage oppstartsmedium)
- ISO-fil med Windows Server 2025
- ISO-fil med Windows 11
- ISO-fil med Ubuntu Server 24.04

## Fremgangsmåte

### 1. Installer Windows Server
1. Gjør minnepinnen til oppstartsmedium for Windows Server 2025 vha Rufus
2. Sjekk at virtualisering er aktivert i BIOS på server-PC-en ([])
3. Installer Windows Server på den ene PC-en
	- Lag to partisjoner; 
		- En partisjon (C:) på 100-150 GB for operativsystemet og evt tjenester
		- En partisjon (D:) for resten av den tilgjengelige plassen for å lagre VM-er og data
4. Når Windows server er installert:
	- Endre maskinnavn til noe enkelt, f.eks. `Labserver`
	- Still klokka på serveren (Tidssone UTC+0100)

### 2. Basisoppsett av Unifi-ruter
1. Koble Windows Server-PC-en til Unifi-ruterens LAN-port og koble ruterens WAN-port til nettverkspunktet i veggen
2. Resett Unifi-ruteren
3. Koble til ruteren ved å skrive default gateway-adressen inn i nettleser på Windows serveren.
4. Kjør basisoppsett på Unifi-ruteren så du får nett
	- Om labnettverket er satt opp med DHCP, trenger du ikke statisk IP-adresse på WAN-siden, men du kan velge DHCP (snakk med lærer/nettverksadmin om du er usikker).
5. På Windows Server; sett statisk IP-adresse `192.168.1.10` på serverens nettverkskort. (Snarvei til Network Connections: Trykk <kbd>Win</kbd> + <kbd>R</kbd> på tastaturet og skriv inn `ncpa.cpl`, trykk <kbd>Enter</kbd>)


> **Neste punkt kan gjøres på to måter, 3a ELLER 3b**


### 3a. Installasjon av Unifi Controller på en virtuell Ubuntu Server
1. Installer Hyper-V-tjenesten på Windows Server 2025 (husk å sette opp virtuell switch koblet til fysisk nettverkskort)
2. Opprett en virtuell maskin i Hyper-V med Ubuntu Server 24.04 
3. Installer Unifi Controller i den virtuelle Ubuntu Serveren
4. Koble til Unifi-controller via nettleser: 
   `https://<ip-adresse til Ubuntu server>:8443`
5. Konfigurer Unifi-kontroller

### 3b. Installasjon av Unifi Controller på klientmaskin eller Windows Server
1. Installer Unifi Controller på en Windows-maskin i nettverket eller på Windows Serveren. Koble maskinen du skal installere på til ruteren med kabel.
2. Start Unifi-controlleren, og velg **Launch a web browser to access Unifi controller** (eller lignende)
3. Konfigurer Unifi-kontroller

>Pass på at du ikke installerer Unifi-kontroller flere steder samtidig. Du vil da miste kontakten med Unifi-nettverksutstyret ditt, og du må starte på nytt. 

>Det anbefales å bruke løsningen med en virtuell Ubuntu-server, da denne løsningen er mer stabil over tid, og du vil da ha tilgang til kontrollerprogramvaren via en fast url som kan nås fra alle enheter i nettverket.

### 4. Koble sammen resten av nettverket
- Koble WAN-porten på Unifi-ruteren til veggen (dette har du sikkert gjort allerede)
- Koble LAN-porten på Unifi-ruteren til svitsjen (hvilken som helst port)
- Koble klient-PC til svitsjen
- Koble Server-PC til svitsjen

### 5. Sette opp klientmaskin
1. Lag installasjonsmedium for Windows 11 (Rufus og minnepinne)
2. Installer Windows 11 på klientmaskinen
	- Lag tre like store partisjoner:
		- En for Windows (NTFS)
		- En for data (filer/dokumenter) (ExFAT)
		- En som er tom (unallocated data - kan brukes til å installere Linux senere)
3. Sjekk om du har nett på klientmaskinen

### 6. Sette opp AD, DNS og DHCP

> Dette kan gjøres på to måter: 
> 1. Alle servertjenester installeres på Windows serveren du har installert, eller 
> 2. Sett opp virtuelle servere, med AD og DNS på en server, og DHCP på en annen server. Dette er regnet som beste praksis i produksjonsmiljøer, da det er mer stabilt å kjøre tjenester separat fra hverandre. Ulempen er at du trenger lisensnøkler for hver enkelt av Windows Server VM-instansene (med mindre du har tilgang til Windows server Datacenter Edition).

### 7. Sette opp andre tjenester
> Alle tjenester som skal være tilgjengelig i nettverket kan nå installeres på VM-er på serveren. Her er et eksempel på oppsett med Hyper-V.


|**VM-navn**|**Rolle(r)**|**Operativsystem**|**Beskrivelse**|
|---|---|---|---|
|**DC01**|Active Directory, DNS|Windows Server|Domenekontroller, håndterer autentisering og navneoppslag.|
|**DHCP01**|DHCP-server|Windows Server|Tildeler IP-adresser til klienter i nettverket.|
|**FS01**|Filserver|Windows Server|Hjemmemapper og delte mapper via AD og GPO.|
|**WSUS01**|Windows Server Update Services|Windows Server|Lokal oppdateringsserver for Windows-klienter og servere.|
|**MGMT01**|Administrasjonsverktøy|Windows Server / Klient|Brukes til RSAT, PowerShell, GPMC, og fjernadministrasjon.|
|**WEB01**|Webserver|Ubuntu Server|Kjører Apache eller Nginx for nettsider og testing av webtjenester.|
|**DOCKER01**|Docker-host|Ubuntu Server|Kjører containere for web, database, overvåkning, etc.|
|**UNIFI01**|UniFi Network Controller|Ubuntu Server|Administrerer nettverksutstyr (AP-er, switcher, gateway) via UniFi.|
|**CL01**|Klient-PC|Windows 10/11|Bruker-PC for testing av pålogging, GPO, hjemmemapper, nettverksstasjoner.|
|_(Valgfritt)_ **MON01**|Overvåkning (Grafana, Prometheus)|Ubuntu Server|For logging og overvåkning av systemer og nettverk.|

#### Tips for oppsett
- Bruk **intern virtuell switch** i Hyper-V for å simulere et lukket nettverk.
- Gi VM-er **statisk IP** eller DHCP-reservasjon for enkel administrasjon.
- Bruk **snapshots** før større endringer.
- Installer **SSH** på Linux-VM-er for fjernstyring.
- Bruk **evalueringsversjoner** av Windows Server for testing.

### 8. Sett opp Azure Arc

>**Azure Arc** er Microsofts løsning for å **administrere lokale og hybride miljøer** som om de var en del av Azure – og det passer perfekt inn i et oppsett som har **lokale VM-er i Hyper-V** som kjører tjenester som AD, DHCP, filserver osv.

1. Opprett Azure studentkonto og logg inn
2. Installer Azure Connected Agent på hver VM