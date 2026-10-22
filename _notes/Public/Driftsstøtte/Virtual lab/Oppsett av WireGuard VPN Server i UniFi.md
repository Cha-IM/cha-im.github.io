---
title: Oppsett av WireGuard VPN Server i UniFi
feed: show
date: 23-09-2026
---

## Innhold

- [1. Sette opp VPN-server og klientprofiler](#1-sette-opp-vpn-server-og-klientprofiler)
- [2. Klientkonfigurasjon og Ekstern Test](#2-klientkonfigurasjon-og-ekstern-test)
- [Hva som skal dokumenteres i Økt 4](#hva-som-skal-dokumenteres-i-%C3%98kt-4)
- [Refleksjonsoppgaver — Økt 4](#refleksjonsoppgaver--%C3%98kt-4)


VPN kan brukes til å koble til et nettverk fra hvor som helst i verden, slik at det ser ut som du er inne i nettverket, og kan bruke lokale tjenester. I denne øvelse skal vi bruke Wireguard VPN som er innebygd i Unifi-kontrolleren.

En ulempe med vårt system er at vi ikke har tilgang til ruterne lenger opp i fylkesnettet, og vi kan derfor ikke sette opp port forwarding på disse, som kreves for å få tilgang helt inn til våre LAN fra hvor som helst på Internett. Derfor vil dere bare kunne koble til nettverket deres med VPN så lenge dere er koblet til IM-nettet. Dermed blir den eneste forskjellen med å koble til med Wireguard VPN at dere nå kan koble til nettverket deres via trådløsnettet IM-nett hvor som helst på IM-avdelingen.

## 1. Sette opp VPN-server og klientprofiler
- Gå til UniFi Controller: **Settings -> VPN -> VPN Server -> Create New**.
- Velg VPN Protocol: **WireGuard**.
- Klikk på **Add client** Opprett to klientprofiler (`ElevA-Laptop` og `ElevB-Laptop`).
- Last ned `.conf`-profilfilene til laptopene.
- Trykk på **Create** for å opprette VPN-serveren 
-  Åpne begge `.conf`-filene i notisblokk. De ser ut noe som dette:
```plaintext
[Interface]
PrivateKey = [Din unike private nøkkel]
Address = 192.168.2.2/32,fd9b:a618:4666:f283::2/128
DNS = 192.168.2.1,fd9b:a618:4666:f283::1

[Peer]
PublicKey = [Din unike offentlige nøkkel]
AllowedIPs = 0.0.0.0/0,::/0
Endpoint = 172.20.17.155:51820
```
Endre `AllowedIPs` fra `0.0.0.0/0,::/0` til `192.168.X.0/24`

## 2. Klientkonfigurasjon og Ekstern Test
- Installer WireGuard-klientprogramvaren på laptopene ([wireguard.com](https://www.wireguard.com/?utm_source=gemini)).
- Importer `.conf`-filen og aktiver tunnelen.
- **Ekstern test (Simulert hjemmekontor):** Koble fra nettverkskabelen i laptopen og koble til det trådløse nettet IM-nett. Aktiver WireGuard VPN og sjekk at du når både Proxmox UI (`192.168.X.2:8006`) og kan starte en RDP-sesjon mot din virtuelle Windows-klient.


## Hva som skal dokumenteres i Økt 4

1. **UniFi VPN Server Dashboard:** Skjermbilde fra UniFi Controller som viser at WireGuard VPN Server er aktiv og at klientene er opprettet.
2. **Ekstern VPN-tilkobling:** Skjermbilde av WireGuard-klienten på laptopen i tilkoblet tilstand  _samtidig_ som RDP-vinduet mot Windows-klienten er åpent over IM-nett.


## Refleksjonsoppgaver — Økt 4

- **4.1 (VPN vs. Port Forwarding):** Hvorfor er det en uakseptabel sikkerhetsrisiko å åpne RDP-porten (TCP 3389) direkte mot Internett i en bedrift? Hvordan beskytter WireGuard VPN-tunnelen bedriftens interne ressurser mot angripere?
- **4.2 (UDP vs. TCP for VPN):** WireGuard benytter seg av protokollen UDP (port 51820) i stedet for TCP. Hva er forskjellene på TCP og UDP, og hvorfor egner UDP seg spesielt godt for tunneler og VPN-trafikk?