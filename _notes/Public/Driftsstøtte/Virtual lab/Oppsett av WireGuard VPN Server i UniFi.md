---
title: Oppsett av WireGuard VPN Server i UniFi
feed: show
date: 23-09-2026
---
*Denne artikkelen er ikke testet*

## Innhold

- [1. Sette opp VPN-server og klientprofiler](#1.%20Sette%20opp%20VPN-server%20og%20klientprofiler)
- [2. Klientkonfigurasjon og Ekstern Test](#2.%20Klientkonfigurasjon%20og%20Ekstern%20Test)
- [Hva som skal dokumenteres i Økt 4](#Hva%20som%20skal%20dokumenteres%20i%20%C3%98kt%204)
- [Refleksjonsoppgaver — Økt 4](#Refleksjonsoppgaver%20%E2%80%94%20%C3%98kt%204)


## 1. Sette opp VPN-server og klientprofiler
- Gå til UniFi Controller: **Settings -> VPN -> VPN Server -> Create New**.
- Velg VPN Protocol: **WireGuard**.
- Client IP Subnet: `10.8.0.0/24` | Server Port: `51820`.
- Under **Client Management**: Opprett to klientprofiler (`ElevA-Laptop` og `ElevB-Laptop`).
- Last ned `.conf`-profilfilene til laptopene.

## 2. Klientkonfigurasjon og Ekstern Test
- Installer WireGuard-klientprogramvaren på laptopene ([wireguard.com](https://www.wireguard.com/?utm_source=gemini)).
- Importer `.conf`-filen og aktiver tunnelen.
- **Ekstern test (Simulert hjemmekontor):** Koble laptopen til et eksternt nettverk (f.eks. mobilt internett / hotspot). Aktiver WireGuard VPN og sjekk at du når både Proxmox UI (`192.168.X.2:8006`) og kan starte en RDP-sesjon mot din virtuelle Windows-klient.


## Hva som skal dokumenteres i Økt 4

1. **UniFi VPN Server Dashboard:** Skjermbilde fra UniFi Controller som viser at WireGuard VPN Server er aktiv og at klientene er opprettet.
2. **Ekstern VPN-tilkobling:** Skjermbilde av WireGuard-klienten på laptopen i tilkoblet tilstand (med synlig Sendt/Mottatt data og VPN IP `10.8.0.x`) _samtidig_ som RDP-vinduet mot Windows-klienten er åpent over eksternt nett.


## Refleksjonsoppgaver — Økt 4

- **4.1 (VPN vs. Port Forwarding):** Hvorfor er det en uakseptabel sikkerhetsrisiko å åpne RDP-porten (TCP 3389) direkte mot Internett i en bedrift? Hvordan beskytter WireGuard VPN-tunnelen bedriftens interne ressurser mot angripere?
- **4.2 (UDP vs. TCP for VPN):** WireGuard benytter seg av protokollen UDP (port 51820) i stedet for TCP. Hva er forskjellene på TCP og UDP, og hvorfor egner UDP seg spesielt godt for tunneler og VPN-trafikk?