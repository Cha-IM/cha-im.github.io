---
title: Installasjon av Unifi Controller i Proxmox VE
feed: show
date: 23-09-2026
---
*Denne artikkelen er ikke testet*

## Innhold

- [1. Opprette LXC-container for UniFi Controller](#1-opprette-lxc-container-for-unifi-controller)
- [2. Førstegangsoppsett og Adoption](#2-f%C3%B8rstegangsoppsett-og-adoption)
- [Hva som skal dokumenteres i Økt 2](#hva-som-skal-dokumenteres-i-%C3%98kt-2)
- [Refleksjonsoppgaver — Økt 2](#refleksjonsoppgaver--%C3%98kt-2)



## 1. Opprette LXC-container for UniFi Controller
- Åpne **Shell** på Proxmox-noden i web-grensesnittet.
- Kjør hjelpeskriptet for UniFi Network Application:
	```bash
	bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/ct/unifi.sh)"
	```
- Velg **Advanced Settings** og oppgi parametere:
	- CT ID: `100` | Hostname: `unifi-controller`
	- RAM: `2048 MB` | Disk: `8 GB`
	- IP: Statisk IP `192.168.X.3/24` | Gateway: `192.168.X.1`

## 2. Førstegangsoppsett og Adoption
- Åpne nettleseren mot kontrolleren: `[https://192.168.](https://192.168.)X.3:8443`.
- Opprett lokal admin-bruker (`admin_lab`) og gi nettverket navnet `Lab-GruppeX`.
- Gå til **Devices**, finn UXG-Lite (står som _Pending Adoption_) og klikk **Adopt Device**.
- Kontroller under **Settings -> Networks** at LAN-subnettet matcher gruppens IP-plan.


## Hva som skal dokumenteres i Økt 2

1. **LXC Container-status:** Skjermbilde fra Proxmox som viser LXC ID 100 `unifi-controller` i aktiv drift (inkludert CPU/RAM-graf).
2. **Device Adoption:** Skjermbilde fra UniFi Network-oversikten der UXG-Lite har status **Online / Getting Ready**.
3. **Nettverkskonfigurasjon:** Skjermbilde fra UniFi Controller som viser oppsettet for LAN-nettverket (DHCP IP Range og Subnet Mask).

##  Refleksjonsoppgaver — Økt 2

- **2.1 (LXC vs. Fysisk/Virtuell Maskin):** Hva er de viktigste forskjellene på en LXC-container og en full virtuell maskin (VM) i Proxmox når det gjelder ressurshåndtering (RAM/CPU) og isolasjon? Hvorfor egner UniFi Controller seg godt som LXC?
- **2.2 (Prosess for Adoption):** Hva skjer teknisk under "adoption"-prosessen mellom UXG-Lite og UniFi Controller? Hvordan vet gatewayen hvilken kontroller den skal rapportere til?
