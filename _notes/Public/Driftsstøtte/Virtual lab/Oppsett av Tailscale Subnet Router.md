---
title: Oppsett av Tailscale Subnet Router
feed: show
date: 22-10-2026
---

*Denne guiden er kun testet på enkeltpunkter. Si fra om noen av kommandoene gir feilmelding*

Tailscale er et mesh VPN nettverk bygd på WireGuard-protokollen. Tailscale lar deg lage et privat, kryptert nettverk mellom enhetene dine, der enhetene er koblet direkte til hverandre (peer-to-peer) via VPN. Fordi enhetene er koblet direkte til hverandre via Tailscale sin koordineringsserver på [tailscale.com](https://tailscale.com/), trenger vi ikke port forwarding gjennom nettverket, slik som vi måtte på Unifi sin Wireguard-løsning. Derfor kan Tailscale brukes i lab-nettverket vårt for å koble til nettverket ditt fra hvor som helst i verden.

Tailscale-klienten installeres direkte på ProxMox-noden din, og må også installeres på alle andre enheter du skal bruke til å koble deg til lab-nettverket ditt eksternt (som laptopen din og mobiltelefon). Alle enheter som har Tailscale-klienten innlogget på samme Tailscale-konto utgjør et lokalt nettverk.

**Opprett en gratis Tailscale-konto:
Gå til [https://tailscale.com](https://tailscale.com/) og opprett en gratis konto.

### Steg 1: Fiks APT-arkivene (Fjern Enterprise-sperren)

Proxmox stopper oppdateringer dersom du mangler betalt lisens (`401 Unauthorized` på `pve-enterprise` og `ceph`). Kilde-filene må slettes og erstatte med No-Subscription-arkivet.

Kjør følgende i **Proxmox Shell**:

```bash
# 1. Slett enterprise-kildene (både .list og .sources format)
rm -f /etc/apt/sources.list.d/pve-enterprise* /etc/apt/sources.list.d/ceph*

# 2. Legg til gratis-arkivet (No-Subscription)
echo "deb http://download.proxmox.com/debian/pve trixie pve-no-subscription" > /etc/apt/sources.list.d/pve-no-subscription.list

# 3. Installer Tailscale
curl -fsSL https://tailscale.com/install.sh | sh
```

### Steg 2: Aktiver IP-videreformidling (IP Forwarding)

For at Proxmox skal kunne rute VPN-pakker fra Tailscale videre ut på det fysiske nettverket, må IP-forwarding aktiveres i Linux-kjernen.


```bash
# 1. Legg til permanente sysctl-regler
echo 'net.ipv4.ip_forward = 1' | tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | tee -a /etc/sysctl.d/99-tailscale.conf

# 2. Aktiver endringene umiddelbart
sysctl -p /etc/sysctl.d/99-tailscale.conf
```

- **Verifisering:** Kjør `cat /proc/sys/net/ipv4/ip_forward` – utskriften skal være `1`.

### Steg 3: Ytelsesoptimalisering (Fjern UDP GRO-advarsel)

For å forhindre hastighetsbegrensninger på nettverksbroen (`vmbr0`), aktiveres UDP Generic Receive Offload:

```bash
ethtool -K vmbr0 rx-udp-gro-forwarding on rx-gro-list off
```

_(Valgfritt: For at denne endringen skal overleve en omstart av Proxmox, kan linjen `post-up ethtool -K vmbr0 rx-udp-gro-forwarding on rx-gro-list off` legges under `iface vmbr0 inet static` i filen `/etc/network/interfaces`)._

  

### Steg 4: Start Tailscale med SNAT og Subnet-ruting

For at Windows-VM-er, UniFi Controller og UXG-Lite skal godta trafikken uten å blokkere den i egne brannmurer, må **SNAT (Source NAT)** aktiveres. Dette gjør at alle VPN-forespørsler ser ut som de kommer direkte fra Proxmox sin IP (`192.168.1.2`).

```bash
tailscale up --advertise-routes=192.168.X.0/24 --snat-subnet-routes=true
```

1. Kopiér innloggingslenken som vises i terminalen.
2. Åpne lenken i nettleseren og logg inn på din Tailscale-konto.


### Steg 5: Godkjenn subnettet i Tailscale Admin Console

1. Gå til **[login.tailscale.com/admin/machines](https://login.tailscale.com/admin/machines)**.
2. Finn Proxmox-noden din (`pve-laerer`) i listen.
3. Klikk på de tre prikkene (`...`) helt til høyre -> **Edit route settings**.
4. Huk av for **`192.168.1.0/24`** under _Subnet routes_ og trykk **Save**.
5. Klikk på de tre prikkene (`...`) på nytt og velg **Disable key expiry** (slik at tilkoblingen ikke utløper etter 180 dager).


### Steg 6: Sjekk klientinnstillinger og test tilkoblingen

1. Installer **Tailscale-appen** på mobil/laptop og logg inn med samme konto.
2. Pass på at innstillingen **Use Tailscale subnets** (eller _Accept routes_) er slått på i appen.
3. Slå på VPN på mobilen over 4G/5G.
4. Test tilkobling til enhetene i labben:  
    - **Proxmox VE:** `https://192.168.X.2:8006`
    - **UniFi OS Controller:** `https://192.168.X.3:11443`
    - **UXG-Lite Gateway:** `https://192.168.X.1`
    - **Windows RDP:** Koble til med `192.168.X.Y` (IP-adressen til Windows-klienten)