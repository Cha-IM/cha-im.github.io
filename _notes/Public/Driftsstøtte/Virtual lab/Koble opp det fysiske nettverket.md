---
title: Koble opp det fysiske nettverket
date: 23-09-2026
feed: show
---
## Innhold

- [1. Utstyrsliste og IP-plan (Per gruppe)](#1-utstyrsliste-og-ip-plan-per-gruppe)
- [2. Topologioversikt](#2-topologioversikt)
- [3. Fysisk kabling](#3-fysisk-kabling)



## 1. Utstyrsliste og IP-plan (Per gruppe)

| **Utstyr / Komponent**      | **Antall** | **Beskrivelse**                                                      |
| --------------------------- | ---------- | -------------------------------------------------------------------- |
| **Stasjonær PC (Lab-vert)** | 1 stk.     | Kraftig PC der Proxmox VE installeres direkte ("bare-metal").        |
| **USB-minnepenn**           | 2 stk.     | - Oppstartbar USB med Proxmox VE<br>- Oppstartbar USB med Windows 11 |
| **UniFi Gateway UXG-Lite**  | 1 stk.     | Fysisk ruter, brannmur og VPN-gateway.                               |
| **Fysisk Svitsj**           | 1 stk.     | Lokal svitsj på pulten.                                              |
| **Elev-laptoper**           | 2 stk.     | Elev A og Elev B sine maskiner.                                      |
| **Patchkabler (RJ-45)**     | 5 stk.     | Nettverkskabler.                                                     |

> **IP-subnetskjema:** Hver gruppe tildeles et unikt IP-område. Erstatt **`X`** med ditt gruppenummer (f.eks. Gruppe 1 = `192.168.10.0/24`, Gruppe 2 = `192.168.20.0/24`).


## 2. Topologioversikt


```plaintext
                      [ Skolenett / Internett ]
                                  │
                                  ▼ (WAN)
                      ┌──────────────────────┐
                      │ UniFi Gateway (UXG)  │ (LAN Gateway: 192.168.X.1)
                      └───────────┬──────────┘ (VPN Pool: 10.8.0.0/24)
                                  │ (LAN)
                                  ▼
                      ┌──────────────────────┐
                      │   Fysisk Svitsj      │
                      └─┬─────────┬────────┬─┘
                        │         │        │
          ┌─────────────┘         │        └─────────────┐
          ▼                       ▼                      ▼
       Elev A Laptop        Elev B Laptop        Proxmox VE Vert
       (DHCP fra UXG)       (DHCP fra UXG)       (Statisk: 192.168.X.2)
                                                         │
                                                         ├─► LXC 100: UniFi Controller (192.168.X.3)
                                                         ├─► VM 101: Win11-Klient-A (DHCP)
                                                         └─► VM 102: Win11-Klient-B (DHCP)
```

## 3. Fysisk kabling
- Koble RJ-45 kabel fra skolens nettverksuttak til **WAN-porten** på UXG-Lite.
- Koble **LAN-porten** på UXG-Lite til Port 1 på den fysiske svitsjen.
- Koble nettverkskortet på den stasjonære PC-en til Port 2 på svitsjen.
- Koble Elev A og Elev B sine laptoper til henholdsvis Port 3 og Port 4 på svitsjen.



