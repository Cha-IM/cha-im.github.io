---
title: Installasjon av Unifi Controller i Proxmox VE
feed: show
date: 23-09-2026
---

## Innhold

- [1. Opprette LXC-container for UniFi Controller](#1-opprette-lxc-container-for-unifi-controller)
- [2. Førstegangsoppsett og Adoption](#2-f%C3%B8rstegangsoppsett-og-adoption)
- [Hva som skal dokumenteres i Økt 2](#hva-som-skal-dokumenteres-i-%C3%98kt-2)
- [Refleksjonsoppgaver — Økt 2](#refleksjonsoppgaver--%C3%98kt-2)



## 0. Oppsett av UXG-Lite
- Koble laptopen din til switchen med kabel og slå av wi-fi.
- Åpne nettleseren og skriv ´unifi/´ i adressefeltet
- Du vil få opp en nettside der det står "Gateway Lite Setup". Klikk på "Start secure browser setup"
- Du vil få en advarsel om at "Tilkoblingen er ikke privat". Klikk på "Avansert" "Fortsett til unifi (usikker)".
- Klikk på "Other configuration options" nederst på siden.
- Klikk på "Local IP and DHCP"
- Fyll inn:
	- "IP Address": `192.168.X.1`
	- "Netmask": `24`
	- Huk av "DHCP server"
	- "DHCP Range": `192.168.X.1` - `192.168.X.254`
- Klikk på "Apply changes"
- Klikk på "Confirm and apply"
- Vent ett minutt
- Siden vil lastes på nytt innen ett minutt, klikk da på "Fortsett til 192.168.X.1 (usikker)"
- Setupen vil starte på nytt, men du skal ikke gjøre noe mer her. Du skal nå koble deg til Proxmox-noden.


## 1. Opprette LXC-container for UniFi Controller

- Logg deg på Proxmox-noden ved å skrive `192.168.X.2` i adressefeltet i nettleseren.
- Logg deg inn med brukernavn `root` og passordet du satte i Proxmox-installasjonen.
- Under "Datacenter" i vinduet til venstre finner du Proxmox-noden med det navnet du satte i installasjonen. Klikk på den for å finne info om systemet ditt.
- Klikk på "**Shell**" opp til høyre på skjermen.
- Kjør hjelpeskriptet for UniFi Network Application:
	```bash
	bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/ct/unifi-os-server.sh)"
	```
- Velg **No** på spørsmål om å sende Diagnostics.
- Velg **Advanced Install** 
- CONTAINER TYPE: Velg **Privileged** (Trykk på Enter.)
- ROOT PASSWORD: Sett samme passord som du bruker for å logge deg på Proxmox-noden
- SET CONTAINER ID: 100
- HOSTNAME: unifi-controller
- DISK SIZE: 20
- CPU CORES: 2
- RAM SIZE: 2048
- NETWORK BRIDGE: vmbr0
- IPV4 CONFIGURATION: static
- STATIC IPv4 ADDRESS: 192.168.X.3/24 (X er gruppenummeret ditt)
- GATEWAY IP: 192.168.X.1 (Adressen til UXG-Lite)
- IPv6 CONFIGURATION: none
- MTU SIZE: La det stå blankt og trykk enter
- DNS SEARCH DOMAIN: La det stå blankt og trykk enter
- DNS SERVER: 1.1.1.1
- MAC ADDRESS: La det stå blankt og trykk enter
- VLAN TAG: La det stå blankt og trykk enter
- CONTAINER TAGS: bak det som står fra før, skriv inn `;unifi`
- SSH KEY SOURCE: none
- SSH ACCESS: Yes
- FUSE SUPPORT: No
- TUN/TAP SUPPORT: Yes
- NESTING SUPPORT: Yes
- GPU PASSTHROUGH: No
- KEYCTL SUPPORT: Yes
- APT CACHER PROXY: No
- HTTP/HTTPS PROXY: No
- CONTAINER TIMEZONE: Europe/Oslo
- CONTAINER PROTECTION: Yes
- DEVICE NODE CREATION: No
- MOUNT FILESYSTEMS: La det stå blankt og trykk enter
- POST-INSTALL HOOK (HOST): La det stå blankt og trykk enter
- VERBOSE MODE: No
- Du får nå en oppsummering av valgene dine. Velg **Yes.** Det er mulig at skjermen blir kuttet av på bunnen og du ikke ser noen valg på skjermen. **Trykk da på pil til venstre én gang og trykk <key>Enter</key> for å bekrefte valgene dine**.
- Til slutt får du spørsmålet "Save these advanced settings as defaults for Unifi-OS-Server?" Velg "Yes"
- Skriptet vil nå installere Unifi-controlleren. Dette kan ta litt tid, da den må laste ned installasjonsfiler for en Linux-installasjon, og installasjonsfiler for Unifi OS Server.

## 2. Førstegangsoppsett og Adoption
- Skriv `unifi/` i nettleseren.
- Gi UXG-Lite et navn: *unifi-gruppe-X*
- Under **UI Account**, klikk på **Other Configuration Options**
- Klikk på **Manually Connect to UniFi Network**
- Under **Inform URL**, skriv inn `http://192.168.X.3:8080/inform`
- Klikk på "Got it"

- Åpne nettleseren mot kontrolleren: `https://192.168.X.3:11443`.
- Gi Unifi-serveren din et navn: unifi-server-gruppe-X
- Under **Create a UI Account**, klikk på **Proceed Without a UI Account**
- Klikk på **Continue Anyway**
- **Set Console Password**: Velg et passord for å logge på Unifi Controller. Passordet må være minst 12 tegn langt, og ha både store og små bokastver, tall og spesialtegn. Det kan være samme passord som du bruker for å logge på Proxmox-noden, hvis det oppfyller alle de kravene.
- Huk av på **I understand and agree to Terms of Service and Privacy Policy**
- Klikk på **Finish**
- **Setup Complete!** Klikk på **Go To Dashboard**.
- Klikk på **Unifi devices** (bildet av en sirkel inne i en sirkel i feltet til venstre)
- Ved **Gateway Lite** og **US 8 60 W** (switchen) står det **Click to Adopt** under **Status**, klikk der på begge to.
- Det starter en adopsjonsprosess i Unifi-controlleren. Når den er ferdig, hvis det står **Update available**, klikk der også.
- Lyset foran på UXG-Lite vil lyse blått når den er adoptert.
- Hvis du oppdaterer UXG-Lite vil den restarte. Det vil da stå **Console offline** på skjermen. Vent til UXG-Lite har startet igjen, så vil serveren komme tilbake. Oppdater siden i nettleseren når UXG-Lite har fast blått lys foran.




## Hva som skal dokumenteres i Økt 2

1. **LXC Container-status:** Skjermbilde fra Proxmox som viser LXC ID 100 `unifi-controller` i aktiv drift (inkludert CPU/RAM-graf).
2. **Device Adoption:** Skjermbilde fra UniFi Network-oversikten der UXG-Lite har status **Online / Getting Ready**.
3. **Nettverkskonfigurasjon:** Skjermbilde fra UniFi Controller som viser oppsettet for LAN-nettverket (DHCP IP Range og Subnet Mask).

##  Refleksjonsoppgaver — Økt 2

- **2.1 (LXC vs. Fysisk/Virtuell Maskin):** Hva er de viktigste forskjellene på en LXC-container og en full virtuell maskin (VM) i Proxmox når det gjelder ressurshåndtering (RAM/CPU) og isolasjon? Hvorfor egner UniFi Controller seg godt som LXC?
- **2.2 (Prosess for Adoption):** Hva skjer teknisk under "adoption"-prosessen mellom UXG-Lite og UniFi Controller? Hvordan vet gatewayen hvilken kontroller den skal rapportere til?
