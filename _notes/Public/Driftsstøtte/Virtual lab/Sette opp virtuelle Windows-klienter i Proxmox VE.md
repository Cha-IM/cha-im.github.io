---
title: Sette opp virtuelle Windows-klienter i Proxmox VE
feed: show
date: 23-09-2026
---
## Innhold

- [1. Opprette Virtuelle Maskiner (VM 101 og VM 102):](#1-opprette-virtuelle-maskiner-vm-101-og-vm-102)
- [2. Installasjon av Windows](#2-installasjon-av-windows)
	- [2a. Alternativ 1: Send USB-pennen direkte inn i VM-en (USB Passthrough)](#2a-alternativ-1-send-usb-pennen-direkte-inn-i-vm-en-usb-passthrough)
	- [2b. Alternativ 2: Last opp ISO-filen til Proxmox](#2b-alternativ-2-last-opp-iso-filen-til-proxmox)
- [3. Etter installasjon](#3-etter-installasjon)
- [Hva som skal dokumenteres i Økt 3](#hva-som-skal-dokumenteres-i-%C3%98kt-3)
- [Refleksjonsoppgaver — Økt 3](#refleksjonsoppgaver--%C3%98kt-3)



## 1. Opprette Virtuelle Maskiner (VM 101 og VM 102):
 
- Klikk **Create VM** i Proxmox UI.
- **VM 101 (`Win11-Klient-A`):** CPU: 2 Cores | RAM: 4096 MB | Disk: 50 GB | Network Bridge: `vmbr0` | TPM 2.0 & EFI aktivert.
- **VM 102 (`Win11-Klient-B`):** Samme spesifikasjoner, dedikert til Elev B.
- Start installasjonen og opprett lokale brukerkontoer (`ElevA` og `ElevB`).


## 2. Installasjon av Windows 
### 2a. Alternativ 1: Send USB-pennen direkte inn i VM-en (USB Passthrough)

Du kan koble USB-pennen fysisk inn i den stasjonære Proxmox-PC-en og sende den direkte videre til den virtuelle maskinen. Dette gjør at du kan bruke oppstartsmediet du lagde med Rufus, som omgår kravet om Microsoft-konto, og gjør Windowsinstallasjonen bedre tilpasset virtualisering i lab.

**1. Sett inn USB-pennen i Proxmox-PC-en:**

Sett oppstartsdisken inn i en ledig USB-port på den stasjonære Proxmox-PC-en.

_Verifisering:_ Proxmox registrerer nye USB-enheter automatisk i bakgrunnen i løpet av noen sekunder.

**2. Legg til USB-enheten i VM-en:**

1. I Proxmox web-grensesnittet, klikk på maskinen din (`101 Win11-Klient-A`) i venstremenyen.
2. Velg **Hardware** i undermenyen.
3. Klikk på **Add**-knappen øverst og velg **USB Device**.
4. Velg **Use USB Vendor/Device ID**.
5. Åpne rullegardinmenyen og velg USB-pennen din fra listen (f.eks. SanDisk, Kingston eller Generic Flash Disk).
6. Klikk **Add**.

_Verifisering:_ Du skal nå se en ny linje under Hardware som heter `USB Device (usb0)`.

**3. Endre boot-rekkefølge:**
1. Klikk på **Options** i menyen under din VM.
2. Dobbelklikk på **Boot Order**.
3. Hak av for den nye USB-enheten og trekk den øverst i listen (eller over harddisken).
4. Klikk **OK**.

_Verifisering:_ USB-enheten står nå oppført som et av de første oppstartsvalgene.

**4. Start VM-en og installer:**

Start VM-en og åpne **Console**. Trykk en tast når du ser skjermbildet for oppstart.

_Verifisering:_ Windows 11-installasjonsveiviseren starter opp på skjermen direkte fra USB-pennen.

*Etter at Windows-kjernen er installert fra USB-pennen vil den virtuelle maskinen restarte. Du vil da få en feilmelding om at maskinen prøver å starte installasjon fra USB-en, men at det er allerede en installasjon som er i gang. Fjern USB-pennen og klikk på **Ja** under feilmeldingen.*


### 2b. Alternativ 2: Last opp ISO-filen til Proxmox

1. Åpne Proxmox i nettleseren (`[https://192.168.](https://192.168.)X.2:8006`).
2. I venstremenyen, klikk på lagringsområdet **`local`** under Proxmox-noden din.
3. Velg **ISO Images** i menyen og klikk på **Upload**.
4. Velg Windows 11 ISO-filen fra USB-pennen/laptopen og trykk **Upload**. Vent til opplastingen er fullført (100%).


**1. Opprett ny virtuell maskin (VM):** 
Klikk på den blå knappen **Create VM** øverst til høyre i Proxmox-grensesnittet.

- **VM ID:** `101` (eller `102` for elev B).
- **Name:** `Win11-Klient-A`.
- Klikk **Next**.
**2. Velg operativsystem (OS):** ISO-fil og OS-type.
- **Storage:** Velg `local`.
- **ISO Image:** Velg Windows 11 ISO-filen du nylig lastet opp.
- **Type:** `Microsoft Windows`.
- **Version:** `11/2022/2025`.
- Klikk **Next**.

**3. Systeminnstillinger (Kritisk for Windows 11):** Krav om UEFI og TPM 2.0.

For at Windows 11 skal godkjenne maskinvaren, må disse valgene settes slik:

- **Graphic card:** Default.
- **Machine:** `q35` _(Viktig for nyere Windows)_.
- **BIOS:** `OVMF (UEFI)` _(Obligatorisk for Win 11)_.
- **EFI Storage:** Velg `local-lvm` eller `local-zfs`.
- **Add TPM:** Hak av her _(Obligatorisk)_.  
    - **TPM Storage:** Velg `local-lvm` / `local-zfs`.
    - **Version:** `v2.0`.
- Klikk **Next**.
**4.Konfigurer disk, CPU, minne og nettverk:**Resursfordeling.
- **Disks:**  
    - **Bus/Device:** Velg **`SATA`** _(Anbefalt for enkelhet – da slipper du å laste inn ekstra VirtIO-drivere under installasjonen)_.
    - **Disk size:** `50 GB`.
- **CPU:**  
    - **Cores:** `2` (eller `4` dersom PC-en har god kapasitet).
    - **Type:** `host` _(Gir best ytelse)_.
- **Memory:** `4096 MB` (4 GB RAM).
- **Network:**  
    - **Bridge:** `vmbr0`.
    - **Model:** `Intel E1000` _(Fungerer direkte i Windows uten ekstra drivere)_.
- Klikk **Next** og deretter **Finish**.

**5.Start VM og kjør Windows-installasjonen:** Boot fra virtuell CD.

1. Klikk på den nye VM-en (`101 Win11-Klient-A`) i venstremenyen og velg **Console**.
2. Klikk på **Start Now** øverst.
3. **VIKTIG:** Klikk raskt inne i konsollvinduet og trykk en valgfri tast på tastaturet når du ser teksten _"Press any key to boot from CD or DVD..."_.
4. Windows 11-installasjonsveiviseren starter nå opp. Følg stegene på skjermen for å installere Windows på disken.
 
**Tips: Omgå krav om Microsoft-konto (Opprett lokal brukerkonto)**
Under oppsettet av Windows 11 krever Microsoft ofte tilkobling til en Microsoft-konto. Slik oppretter du heller en ren lokal brukerkonto (`ElevA`).

Først må du koble fra den virtuelle nettverkskabelen et øyeblikk slik at Windows tror maskinen mangler nett.

1. Gå til Proxmox-grensesnittet i nettleseren på laptopen din.
2. Klikk på VM-en din (`101 Win11-Klient-A`) -> velg **Hardware** i undermenyen.
3. Dobbelklikk på **Network Device (net0)**.
4. Hak av for **Disconnect** (eller fjern haken for _Link down_ avhengig av Proxmox-versjon).
5. Klikk **OK**. _(Nettverket til VM-en er nå koblet fra)._
6. Gå tilbake til konsollen i Windows 11.
7. Trykk **`Shift + F10`**, skriv `OOBE\BYPASSNRO` og trykk **Enter**.
8. Maskinen starter på nytt, og du må gå gjennom noen av de samme spørsmålene du har vært gjennom allerede på nytt. Bare fortsett, det er normalt.
9. Når du kommer til opprettelse av brukerkonto, vil knappen **"Jeg har ikke internett"** dukke opp fordi nettverket er koblet fra.
10. Når du har laget brukerkontoen og kommet inn på skrivebordet, går du bare tilbake til Proxmox -> Hardware -> Network Device og fjerner haken for **Disconnect** igjen.



## 3. Etter installasjon

Når du er inne på skrivebordet i Windows:

1. Gå til **Start -> Innstillinger -> System -> Remote Desktop (Fjernskrivebord)**.
2. Slå funksjonen **PÅ**.
3. Åpne `cmd` og skriv `ipconfig` for å finne IP-adressen som UXG-Lite har tildelt maskinen.
4. Du kan nå koble deg til maskinen direkte fra laptopen din via **Tilkobling til fjernskrivebord (mstsc.exe)**.
5. **Nettverkskonfigurasjon og feilsøking i Windows:**
    - Åpne Ledetekst (`cmd`) på begge klientene og kjør `ipconfig /all`. Verifiser at de mottar IP-adresser fra UXG-Lite sin DHCP-tjeneste.
    - Test nettverksforbindelse mellom Klient A og Klient B med `ping [IP-adresse]`.
    - Dersom ping feiler: Konfigurer Windows Firewall til å tillate ICMPv4-Inbound echo request.


## Hva som skal dokumenteres i Økt 3

1. **Proxmox VM Oversikt:** Skjermbilde av Proxmox ressursoversikt som viser at både VM 101 og VM 102 kjører samtidig.
2. **IP-konfigurasjon:** Skjermbilde av `ipconfig /all` fra begge Windows-klientene side om side.
3. **Vellykket Ping-test:** Skjermbilde fra `cmd` som viser 0% pakketap ved ping mellom `Win11-Klient-A` og `Win11-Klient-B`.
4. **RDP I Drift:** Skjermbilde fra Elev A sin laptop som viser at han/hun har en aktiv RDP-sesjon vindu-i-vindu mot sin virtuell Windows 11-maskin.

## Refleksjonsoppgaver — Økt 3

- **3.1 (Brannmur og sikkerhet):** Hvorfor blokkerer Windows Firewall ICMP (ping) som standard på "Public/Private" nettverksprofiler? Hvilke sikkerhetsrisikoer er knyttet til at enheter svarer på ping i et bedriftsnettverk?
- **3.2 (Ressursallokering / Overcommit):** Dersom den stasjonære PC-en har 16 GB RAM totalt, og dere tildeler 4 GB til Elev A sin VM, 4 GB til Elev B sin VM, 2 GB til UniFi LXC og Proxmox bruker 2 GB selv — hva skjer dersom dere i tillegg starter opp to nye tunge server-VM-er? Forklar konseptet RAM Overcommit og Swapping.
