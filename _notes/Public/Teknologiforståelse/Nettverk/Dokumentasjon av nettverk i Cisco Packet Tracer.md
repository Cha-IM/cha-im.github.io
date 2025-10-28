---
title: Dokumentasjon av nettverk i Cisco Packet Tracer
feed: show
date: 28-10-2025
---
Vi skal nå se videre på nettverkspoppsett i Cisco Packet Tracer, og hvordan vi dokumenterer nettverksoppsett. Se artikkelen [[Innføring i lokale nettverk med Cisco Packet Tracer]] hvis du ikke allerede har lastet ned Cisco Packet Tracer.

Det vi skal jobbe med i dag er kurset [Exploring Networking with Cisco Packet Tracer](https://www.netacad.com/courses/exploring-networking-cisco-packet-tracer?courseLang=en-US) på Cisco Networking Academy. Start kurset ved å klikke på den grønne knappen "**Get Started With Self-Paced**".

![Skjermbilde fra Cisco Networking Academy](/assets/img/packettracer/exploring.png)

## Dokumentasjon
Mens du jobber med kurset skal du også dokumentere nettverkene du setter opp i Cisco Packet Tracer.

Lag en mappe i [dokumentasjons-repoet ditt på Github](https://classroom.github.com/a/UVPhVCn7) som du kaller `modul-04-nettverkslab/`. I denne mappen lager du en fil som du kaller `packet-tracer-dokumentasjon.md` Lag også en undermappe som du kaller `assets/`. Hvis du har clonet repoet ditt til VS Code, kan du opprette mappene og filene direkte i *Explorer*-vinduet i VS Code. Hvis ikke kan du gjøre det direkte i github.com i nettleseren ved å klikke på **+**-tegnet ved siden av den grønne **Code**-knappen.

![Skjermbilde av Github-repo på github.com](/assets/img/packettracer/github-new-file.png)
### Tips: Lag en ny mappe direkte i nettleseren

For å lage en ny mappe avslutter du mappenavnet med *skråstrek*, slik: `modul-04-nettverkslab/`. Da kommer det opp et nytt tekstfelt for å lage en ny fil i den nye mappa. Du må lage en ny fil, så det enkleste er å bare lage en `readme.md`-fil i den nye mappa.

![](/assets/img/packettracer/github-new-folder.gif)


## Dokumentasjon av kontornettverk i Cisco Packet Tracer

Når du jobber med å sette opp et kontornettverk i Cisco Packet Tracer, skal du dokumentere hvordan du har satt det opp.  Dokumentasjonen skal vise at du forstår hvordan nettverket fungerer, og gjøre det mulig for andre å forstå og gjenskape oppsettet ditt.


### Hva dokumentasjonen skal inneholde

#### 1. Tittel og introduksjon

Start dokumentasjonen med en kort beskrivelse av hva du har laget.  
Eksempel:

```markdown
# Kontornettverk – Cisco Packet Tracer

Dette dokumentet beskriver hvordan jeg har satt opp et kontornettverk i Cisco Packet Tracer. Nettverket består av to avdelinger koblet sammen med en router, med DHCP, DNS og webserver.
```

#### 2. Nettverksoversikt

Beskriv hva slags utstyr du har brukt:

- Rutere, switcher, PC-er, servere osv.
- Hvilke nettverk/avdelinger som finnes (for eksempel IT, Admin, Gjest).
- IP-adresser og subnett.

Du kan vise dette som en punktliste eller en tabell:

```markdown
| Enhet | Rolle | IP-adresse | Kommentar |
|--------|--------|-------------|------------|
| Router0 | Kobler sammen to nettverk | 192.168.1.1 / 192.168.2.1 | Gateway |
| Switch0 | Kobler PC-er i IT-avdelingen | - | - |
| PC0 | Bruker i IT-avdelingen | 192.168.1.10 | Får IP fra DHCP |
```

Denne markdown-koden vil se slik ut når den vises i nettleseren:

| Enhet | Rolle | IP-adresse | Kommentar |
|--------|--------|-------------|------------|
| Router0 | Kobler sammen to nettverk | 192.168.1.1 / 192.168.2.1 | Gateway |
| Switch0 | Kobler PC-er i IT-avdelingen | - | - |
| PC0 | Bruker i IT-avdelingen | 192.168.1.10 | Får IP fra DHCP |


#### 3. Nettverksdiagram

Legg inn et bilde (skjermdump) fra Packet Tracer som viser nettverket ditt.

1. Ta skjermbilde av hele oppsettet i Packet Tracer.
2. Lagre bildet i `Assets`-mappen.
3. Sett det inn i Markdown-filen slik:

```markdown
![Nettverksdiagram](Assets/nettverk.png)
```


#### 4. Konfigurasjon

Vis hvordan du har konfigurert viktige deler av nettverket.  
Dette kan være:

- Routerkonfigurasjon (IP-adresser, routing, DHCP)
- Serverinnstillinger (DNS, Web, DHCP)
- IP-oppsett på PC-er

Eksempel:

```markdown
### Routerkonfigurasjon
```

```plaintext
Router> enable
Router# configure terminal
Router(config)# interface gig0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config)# ip dhcp pool IT
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 192.168.1.2
```


#### 5. Testing

Vis at nettverket fungerer:

- Ping mellom enheter
- Tilkobling til webserver
- IP tildelt via DHCP

Eksempel:

```markdown
### Test av forbindelser
- PC0 kan pinge PC1 ✅
- PC0 får IP automatisk fra DHCP ✅
- PC1 får opp nettsiden fra WebServer ✅
```

Legg gjerne inn skjermbilder av terminalvinduer:

```markdown
![Ping-test](Assets/pingtest.png)
```


#### 6. Oppsummering / refleksjon

Avslutt med en kort tekst om hva du lærte eller hva som fungerte/ikke fungerte.

```markdown
### Oppsummering
Jeg lærte hvordan routere og DHCP fungerer sammen. Jeg hadde først problemer med DNS-serveren, men løste det ved å sjekke gateway-innstillingen.
```



### Levering

1. Lagre dokumentasjonen som `nettverksdokumentasjon.md`
2. Legg inn eventuelle bilder i `Assets/`
3. Last opp alt til dokumentasjons-repoet ditt på GitHub.
4. Sjekk at Markdown-filen vises riktig på GitHub.


###  Tips

- Bruk korte forklaringer og mange bilder.
- Husk at dokumentasjonen skal være **lett å forstå** også for andre.
- Bruk Markdown-formatering for å gjøre dokumentet oversiktlig:
    - `#` for overskrifter
    - `**fet tekst**` for viktige begreper
    - Kodeblokker (` `` `) for terminalkommandoer
