


## Utstyrsliste og IP-plan (Per gruppe)

| **Utstyr / Komponent**      | **Antall** | **Beskrivelse**                                                      |
| --------------------------- | ---------- | -------------------------------------------------------------------- |
| **Stasjonær PC (Lab-vert)** | 1 stk.     | Kraftig PC der Proxmox VE installeres direkte ("bare-metal").        |
| **USB-minnepenn**           | 2 stk.     | - Oppstartbar USB med Proxmox VE<br>- Oppstartbar USB med Windows 11 |
| **UniFi Gateway UXG-Lite**  | 1 stk.     | Fysisk ruter, brannmur og VPN-gateway.                               |
| **Fysisk Svitsj**           | 1 stk.     | Lokal svitsj på pulten.                                              |
| **Elev-laptoper**           | 2 stk.     | Elev A og Elev B sine maskiner.                                      |
| **Patchkabler (RJ-45)**     | 5 stk.     | Nettverkskabler.                                                     |

> **IP-subnetskjema:** Hver gruppe tildeles et unikt IP-område. Erstatt **`X`** med ditt gruppenummer (f.eks. Gruppe 1 = `192.168.10.0/24`, Gruppe 2 = `192.168.20.0/24`).
> 
>   



## Topologioversikt

Plaintext

```
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

## ØKT 1: Fysisk oppkobling, IP-planlegging og installasjon av Proxmox VE

### Praktiske oppgaver

1. **Fysisk kabling:**
    
      
    - Kobl RJ-45 kabel fra skolens nettverksuttak til **WAN-porten** på UXG-Lite.
        
          
        
    - Kobl **LAN-porten** på UXG-Lite til Port 1 på den fysiske svitsjen.
        
          
        
    - Kobl nettverkskortet på den stasjonære PC-en til Port 2 på svitsjen.
        
          
        
    - Kobl Elev A og Elev B sine laptoper til henholdsvis Port 3 og Port 4 på svitsjen.
        

    
      
    



## 
        
          
        
2. 
    

## ØKT 5: Sluttdokumentasjon, topologikart og rapportsammenstilling

### Praktiske oppgaver

1. **Utarbeidelse av helhetlig nettverkskart (Topologi):**
    
      
    - Bruk et profesjonelt verktøy som Draw.io, Cisco Packet Tracer eller Visio.
        
          
        
    - Tegn opp hele infrastrukturen: Skolenett, WAN/LAN-grensesnitt på UXG-Lite, fysisk svitsj, Proxmox-vert, LXC-containere, VM-er og VPN-tunnel.
        
          
        
    - Inkluder alle IP-adresser, portnummer, VLAN/subnett og brukernavn/roller.
        
          
        
2. **Kvalitetssikring og samling av rapporten:**
    
      
    - Sammenstill alle dokumentasjonskrav og refleksjonssvar fra Økt 1–4 i ett felles PDF-dokument.
        
          
        
    - Legg ved en egen **Feilsøkingslogg** (tabell) som beskriver utfordringer gruppen støyter på underveis og hvordan dere løste dem.
        
          
        

### 📷 Hva som skal leveres i Sluttrapporten (Økt 5)

1. **Komplett Nettverkstoppologi:** Vektor/høyoppløselig bilde av det digitale nettverkskartet.
    
      
    
2. **Feilsøkingslogg:** Tabell over oppståtte feil (f.eks. sertifikatadvarsler, brannmurblokkering, manglende IP) med årsak og valgt tiltak.
    
      
    
3. **Alle samlede dokumentasjonsbilder og besvarte refleksjonsoppgaver fra Økt 1 til 4.**
    
      
    

### 🤔 Sluttrefleksjoner og Bærekraftsanalyse — Økt 5

- **5.1 (Bærekraft og Grønn IT):** Sammenlign dette virtualiserte oppsettet (1 kraftig fysisk PC som kjører Proxmox + 3 virtuell enheter) med å kjøpe 3 separate fysiske servere. Vurder forskjellene i energiforbruk, e-avfall (hardware livssyklus) og romoppvarming/kjøling i et datasenter.
    
      
    
- **5.2 (Sikkerhet og Risikoanalyse):** Tenk deg at denne lab-infrastrukturen var produksjonsnettverket til en liten bedrift med 20 ansatte. Identifiser minst to "Single Point of Failure" (SPOF) i designet og foreslå tiltak for å øke tilgjengeligheten (f.eks. redundans, backup-strategi, UPS).