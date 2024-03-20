---
title: Sette opp nettverk med Unifi-ruter
feed: show
date: 19-03-2024
tags:
---
## 1. Komponenter og kabling
Du trenger:
* 1 klient-PC eller server-PC
* 1 Unifi ruter (hvit)
* 1 Switch
* 3 ethernet-kabler

Slik kobler du sammen komponentene:
1. Sett en kabel fra **WAN-porten på ruteren** til din port **i veggen** (den som er koblet opp i svitsjeskapet)
2. Sett en kabel fra **LAN-porten på ruteren** til **svitsjen** (hvilken som helst port)
3. Sett en kabel fra **svitsjen** (hvilken som helst port) til **PC-en din**.

## 2. Resett ruter
Nå må du resette ruteren for å sette den opp på nytt med denne innstillinger.

1. Sett strøm på svitsjen. Den vil nå starte opp og lyset rundt logoene på toppen vil begynne å blinke. 
2. **Vent ca 1 minutt** til lyset på toppen lyser fast.
2. Stikk en binders inn i det lille hullet på forsiden av ruteren. Hold bindersen der i ca 10 sekunder, **til lyset oppå svitsjen** slås av.
3. Svitsjen vil nå starte på nytt og begynne å blinke. Vent ca ett minutt til lyset blir fast igjen. Hvis alt er som det skal, skal lyset være hvitt.

## 3. Gå inn i ruterens innstillinger
Åpne en nettleser på datamaskinen din. I adressefeltet skriver du **192.168.1.1** (hvis det ikke fungerer, prøver du 192.168.0.1, eller 10.0.0.1).

Du vil nå få opp et skjema der du skal fylle inn innformasjon om nettverket ditt.

## 4. IP-adresser
Fyll ut skjemaet med info fra [IM CHA Oversikt over labmaskiner og IP-adresser 2023-2024 - Google Regneark](https://docs.google.com/spreadsheets/d/1CZ7tFNzi1N6dENOXU-uCyjHjf3NYJQOspECbOoXKM5k/edit#gid=1414378157) slik:

### WAN Settings:
1. Connection type: **Static IP**
2. IP address: **Ruter-IP WAN** (din unike adresse)
3. Subnet mask: **255.255.255.0**
4. Router: **Gateway WAN**: (172.31.100.1)
5. Preferred DNS: **8.8.8.8**
6. Alternate DNS: **8.8.4.4**
7. Use VLAN ID: Nei  

### LAN settings
1. IP address: **192.168.1.1**
2. Subnet mask: **255.255.255.0**
3. DHCP Server: **ON**
4. DHCP Range: **192.168.1.6**-**192.168.1.254**

Trykk så på **Apply changes** og vent et par minutter.

## 5. Har du nett?
Nå må du sjekke om du har nett. Åpne en ny fane i nettleseren og prøv å åpne en nettside, f.eks. [trondelagfylke.no](https://www.trondelagfylke.no/)

Hvis nettsiden åpner seg har du nett, hurra!

### Har du ikke nett?
1. Høyreklikk på start-menyen, og klikk på **Network connnections**
2. Klikk på **Change Adapter options**
3. Høyreklikk på **Ethernet**, velg **Properties**
4. I listen under _The connection uses the following items_, klikker du på **Internet protocol version 4 (TCP/IPv4)** og på **Properties**.
5. Klikk på **Use the following IP address**, og fyll ut:
	* IP address: **192.168.1.10**
	* Subnet mask: **255.255.255.0**
	* Default gateway: **192.168.1.1**
6. Use the following DNS server address:
	* Preferred DNS server: **8.8.8.8**
	* Alternate DNS server: **8.8.4.4**

Klikk på **OK**, og **Close**

Du vil nå (mest sannsynlig) ha kontakt med internett.

#### Har du fortsatt ikke nett?
- Sjekk om kabelen fra ruteren til veggen virker
- Sjekk at du er koblet inn i riktig punkt i veggen (at punktet er koblet opp i patch-skapet)



## 6. Last ned Java
Last ned siste versjon av Java: [Download Java for Windows](https://www.java.com/download/ie_manual.jsp)

Åpne installasjonsfilen og installer på vanlig måte.

## 7. Last ned Unifi Controller
Vi kan ikke bruke nyeste versjon av Unifi Controller, men vi bruker version 7.0.23: [UniFi Network Application for Windows](https://dl.ui.com/unifi/7.0.23/UniFi-installer.exe)

Åpne installasjonsfilen og installer på vanlig måte.

## 8. Sett opp Unifi Controller
1. Åpne Unifi Controller fra skrivebordet
2. Det tar litt tid for kontrolleren å koble seg til ruteren, så vent litt.
3. Du kan få spørsmål om du vil tillate Unifi å sende og motta trafikk gjennom brannmuren. Trykk på **Allow**
4. Klikk på **Launch a web browser to access Unifi controller**
5. Nettleseren vil nå åpnes, og du skal nå konfigurere ruteren.
6. **Name your controller**: Gi kontrolleren din et navn, f.eks. _dittNavncontroller_. **Skriv ned dette i dokumentasjonen din.**
7. Huk av _By selecting this you are agreeing to end user license agreement and the terms of service_
8. Trykk **Next** (helt nederst i høyre hjørne)
9. Kontrolleren spør nå om brukernavn og passord. Vi skal ikke gjøre det, velg istedenfor **Switch to advanced setup**.
10. **Advanced remote and local access**: Klikk de to bryterne _Enable remote access_ og _Use your Ubiquiti account for local access_ **av**.
11. Fyll inn skjemaet: 
	* _Local administrator username_: admin. **Skriv ned dette i dokumentasjonen din.**
	* _Local administrator password_: et enkelt passord som du husker - **Skriv ned passordet i dokumentasjonen din** (ikke bruk et passord du bruker andre steder)
	* _Confirm password_: Skriv passordet en gang til
12. Klikk på _Next_
13. **Unifi Network Setup** Klikk bryteren _Enable auto backup_ **av**.
14. **Devices setup**: Huk av boksen ved __USG-3P__. Dette er ruteren din, som skal meldes inn i nettverket.
15. **WiFi Setup**: (Vi skal egentlig ikke bruke WiFi, men vi må sette det opp likevel)
	* _WiFi Name_: F.eks. dittNavnWiFi. **Skriv ned dette i dokumentasjonen din.**
	* _WiFi Password_: Et enkelt passord med minst 8 tegn. **Skriv ned passordet i dokumentasjonen din**
16. **Review Configuration**: Her får du en oppsummering av innstillingene dine, og skal velge land og tidssone
	* _Country or Territory_: Norway (tips: trykk på O, så er Norge rett over Oman)
	* _Timezone_: (UTC+1) Europe/Oslo
17. Trykk på **Finish**