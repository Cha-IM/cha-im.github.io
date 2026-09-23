---
title: Installasjon av ProxMox VE
feed: show
date: 23-09-2026
---
## Innhold
- [[#1. Bare-metal installasjon av Proxmox VE|1. Bare-metal installasjon av Proxmox VE]]
- [[#Hva som skal dokumenteres i Økt 1|Hva som skal dokumenteres i Økt 1]]
- [[#Refleksjonsoppgaver — Økt 1|Refleksjonsoppgaver — Økt 1]]


## 1. Bare-metal installasjon av Proxmox VE

- Sett inn Proxmox USB-pennen i den stasjonære PC-en og start opp via Boot-menyen (F12/F11).
- Velg _Install Proxmox VE (Graphical)_.
- Sett Target Disk, Tidssone (_Norway/Oslo_) og velg et sikkert root-passord.
- **Nettverkskonfigurasjon:**
	- Hostname: `pve-gruppeX.lab`
	- IP Address: `192.168.X.2/24`
	- Gateway / DNS: `192.168.X.1`
- Fullfør installasjonen, ta ut USB-pennen og start PC-en på nytt.
3. **Verifisering:** Åpne nettleseren på en laptop og logg inn på Proxmox UI: `[https://192.168.](https://192.168.)X.2:8006`.


## Hva som skal dokumenteres i Økt 1

1. **Fysisk kabling:** Et skarpt bilde av oppsettet med fargekoding eller merking av kablene.
2. **IP-adressetabell:** En strukturert tabell som viser planlagte IP-adresser for WAN, LAN Gateway, Proxmox Vert, UniFi Controller og VM-er.
3. **Installationskvittering:** Skjermbilde fra laptopen som viser pålogget Proxmox VE webgrensesnitt (med synlig URL `[https://192.168.](https://192.168.)X.2:8006` og node-status).

## Refleksjonsoppgaver — Økt 1

- **1.1 (Statisk IP vs. DHCP):** Hvorfor _må_ hypervisoren (Proxmox-verten) konfigureres med en statisk IP-adresse i stedet for å motta dynamisk IP fra DHCP? Hvilke konsekvenser ville det hatt for driften dersom verten byttet IP-adresse etter en omstart?

- **1.2 (Virtualiseringsbro):** Hva er funksjonen til nettverksbroen `vmbr0` i Proxmox, og hvordan fungerer denne sammen med det fysiske nettverkskortet (NIC) i PC-en?