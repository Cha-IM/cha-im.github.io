---
title: Mininet
feed: show
date: 19-03-2024
tags:
---

Mininet er et verktøy for å simulere nettverk, som kan brukes til testing og opplæring nettverk. I denne guiden skal du lære hvordan du setter opp en virtuell maskin som kjører Mininet i Ubuntu Linux.

## 1. Laste ned Mininet Image
Mininet kan lastes ned som en ferdig image-fil som kan åpnes i virtualiseringsprogramvare som VirtualBox. En image-fil er en fil som inneholder en virtuell harddisk, med alle filer som trengs for å kjøre en virtuell maskin, med operativsystem, drivere osv. Siste versjon av Mininet kan lastes ned fra [Mininets Github](https://github.com/mininet/mininet/releases), eller direkte her: [Mininet 2.3.0 Ubuntu 20.04.1 VM Image](https://github.com/mininet/mininet/releases/download/2.3.0/mininet-2.3.0-210211-ubuntu-20.04.1-legacy-server-amd64-ovf.zip)

## 2. Laste ned VirtualBox
VirtualBox er et program som kan brukes til å opprette, administrere og kjøre virtuelle maskiner. 

En virtuell maskin er en stimulert datamaskin som kjører virtuelt på en fysisk datamaskin. Den fungerer akkurat som en fysisk datamaskin, men alle komponentene er simulert (virtualisert). Ved hjelp av virtuelle datamaskiner kan du kjøre flere operativsystemer på samme datamaskin, sette opp simulerte (virtuelle) nettverk, og teste og prøve ut ting uten å være bekymret for at din datamaskin eller operativsystem blir skadet, siden en virtuell datamaskin er helt separert fra din fysiske datamaskin. 

Last ned VirtualBox fra [virtualbox.org](https://www.virtualbox.org/wiki/Downloads) (klikk lenken for operativsystemet på din datamaskin, f.eks. Windows eller MacOS), og installer programmet.

## 3. Laste inn Mininet image i VirtualBox
Når VirtualBox er installert og Mininet imaget du lastet ned i punkt 1 er ferdig nedlastet. Kan du laste imaget inn i VirtualBox. Alt du trenger å gjøre er å pakke ut zip-filen med Minniet imaget, og åpne filen som slutter på .ovf. Dette vil åpne VirtualBox og et vindu som viser deg info om imaget. Klikk på Finish for å legge den virtuelle maskinen inn i VirtualBox.

Før du åpner den virtuelle maskinen må du endre på skjerminnstillingene i VirtualBox slik at det er mulig å endre størrelsen på den virtuelle maskinen, da skjermen er som standard veldig liten. For å få muligheten til å gjøre vinduet større og skaleres, gå inn i VM-ens innstillinger (klikk på Minninet-VM, og det gule tannhjulet der det står **Settings**), velg **User Interface** -> **Visual state: Scaled**.

## 4. Start den virtuelle maskinen _Mininet-VM_
Klikk inne i vinduet til den virtuelle maskinen. Musepekeren vil nå forsvinne, og den virtuelle maskinen vil "fange" tastaturet og musa. For å få tilbake kontroll over vertsmaskinen (din fysiske datamaskin) må du trykke på **Ctrl-knappen til høyre** (Windows) eller **Cmd-knappen til venstre** (Mac). Dette kalles _host button_ i VirtualBox.

Logg inn med brukernavn _mininet_ og passord _mininet_ (merk at det vil ikke vises noen tegn når du skriver inn passordet. Dette er av sikkerhetsgrunner. Trykk enter når du har skrevet passordet)

## Endre keyboard layout i den virtuelle maskinen
Som standard er den virtuelle maskinen satt opp med amerikansk keyboard layout. For å endre dette må du skrive kommandoen:

`sudo dpkg-reconfigure keyboard-configuration`

_Merk at før du har endret keyboard layout må du trykke på pluss-tasten (+/?)  for å skrive bindestrek (-)._

Da kommer det opp en meny der du kan velge mellom forskjellige typer tastatur. Gjør følgende valg (trykk enter mellom hvert valg)
1. Keyboard model: `Generic 105-key PC (intl.)`
2. Country of origin for the keyboard: `Norwegian` 
3. Keyboard layout: `Norwegian (Win keys)` (hvis du har Windows-PC) eller `Norwegian (Macintosh)` om du har Mac.
4. Key to function as Alt Gr: `Right Alt (AltGr)` 
5. Compose key: `No compose key`

## Installere grafisk brukergrensesnitt på den virtuelle maskinen
For å ha muligheten til å flere vinduer på skjermen samtidig må vi bruke et grafisk brukergrensesnitt. Det kan vi installere med denne kommandoen:

`sudo apt-get update && sudo apt-get install xinit lxde virtualbox-guest-x11`

Du vil få spørsmål om du vil fortsette. Bare trykk på Enter.

Når installasjonen er ferdig kan du starte det grafiske brukergrensesnittet ved å skrive `startx`.

Hvis oppløsningen i den virtuelle maskinen er veldig høy (alt på skjermen er veldig lite), kan du starte dette ved å åpne ("start"-)menyen nederst til venstre på skjermen og velge **Preferences**, og **Monitor settings** og velge en lavere oppløsning (resolution), f.eks. 1024x768. Klikk på **Apply**.


# Bruke Mininet
For å starte Mininet, klikk på ("start"-)menyen nederst til venstre, velg **System Tools** og **Xterm**. Du vil da åpne et terminal-vindu der du kan skrive kommandoer.

For å starte Mininet kan du skrive

`sudo mn`

Minnet vil da starte opp et simulert nettverk med en en svitsj (s1), to vertsmaskiner (h1 og h2) og en kontroller (c0).

Du kan se at du nå er inne i Mininet ved at det står `mininet>` foran der du skriver inn tekst.

Nå kan du utforske nettverket som er satt opp. Prøv disse kommandoene:

### `nodes`

Viser alle nodene (komponentene) i nettverket.

### `net`

Viser alle koblingene i nettverket (hvilke enheter som er koblet sammen via hvilke porter).

### `dump`

Viser info om alle nodene i nettverket, inkludert koblinger og IP-adressene til enhetene.



## Åpne separate terminaler for vertsmaskinene

Hvis du åpner vertsmaskinene i hver sin terminal, kan du behandle dem som separate datamaskiner. Dette gjør du med denne kommandoen:

`xterm h1 h2`

Det vil da dukke opp to ny terminalvinduer. Øverst i hvert terminalvindu vil det stå hvilken node de representerer; **"Node: h1"** og **"Node: h2"**.

Kjør kommandoen

`ifconfig -a`

For å se info om nettverkstilkoblingen til hver av nodene.

For å sjekke om nodene har kontakt med hverandre kan du kjøre `ping`-kommandoen fra den ene noden til den andre. Da må du ha IP-adressen til noden som du fikk da du kjørte `ifconfig`

For eksempel, hvis Node: h2 har IP-adressen 10.0.0.2, kjører du denne koden på Node: h1

`ping -c 1 10.0.0.2`

Hvis nodene har kobling til hverandre får du noe som dette som tilbakemelding:

```shell
PING 10.0.0.2 (10.0.0.2) 56(84) bytes of data.
64 bytes from 10.0.0.2: icmp_seq=1 ttl=64 time=0.837 ms

--- 10.0.0.2 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.837/0.837/0.837/0.000 ms
```

Den viktige infoen her er "1 packets transmitted, 1 received, 0% packet loss". Dette betyr at 1 pakke ble sendt og 1 pakke ble mottatt, med ingen tap. Det betyr at nodene har tilkobling til hverandre.


## Sette opp et Mininet-nettverk med Internettkobling og webserver

Sett opp Mininet med NAT for å få Internettilkobling

`sudo mn --nat`

`xterm h1 h2`

Sette opp webserver på node h1:

`python -m SimpleHTTPServer 80 &`

Åpne nettleser og skriv IP-adressen til h1 i adressefeltet