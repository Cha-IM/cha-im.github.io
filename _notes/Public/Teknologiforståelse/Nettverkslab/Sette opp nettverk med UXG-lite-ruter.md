---
title: Sette opp nettverk med UXG-lite-ruter
feed: hide
date: 05-11-2026
---
![[UXG-mini.avif]]
### Resetting av UXG-Lite Gateway

Stikk en binders eller liten pinne inn i hullet ved siden av USB-C-porten (strøm) på baksiden av UXG-Lite. Hold den inne fram til lyset på forsiden slukker. UXG-Lite vil nå restarte. Det kan ta noen minutter før den er på igjen. Når den er ferdig vil lyset på forsiden lyse fast hvitt.

## Oppsett av UXG-Lite

- Koble laptopen din til switchen med kabel og slå av wi-fi.
- Koble switsjen til ruteren på LAN porten. 
- Åpne nettleseren og skriv ´unifi/´ i adressefeltet
	- I mange tilfeller sendes du hit automatisk.
- Du vil få opp en nettside der det står "Gateway Lite Setup".

### Oppsett på statiske nettverk:
- Ruteren vil prøve å koble til nettverket, men får ikke til dette. Den sender deg til siden restart-modem.
- Vi må gå inn på "Other Setup Options"
	- Vi må her fylle inn informasjonen for to av feltene:
		- WAN static IP Adress
		- Local Network Configuration
#### Konfigurering av WAN instillinger
Fra "Other Setup Options" menyen: 
* WAN static IP adress
	* Fyll inn informasjonen fra lærer, husk:
		* MAC Override: Nei
		* VLAN: Nei
	* Trykk på apply changes når du er ferdig med å fylle inn.
	Om alt fungerer som det skal skal du nå få nett og bli videresent til "internet-connected". Trykk Continue

#### Konfigurerer av LAN instillinger
Fra "Other Setup Options" menyen: 
 * Local Network Configuration:
	* Fyll informasjon fra lærer, husk:
		* Endre DHCP Range til
		* Start: 192.168.1.10
		* Slutt: 192.168.1.254
	* Trykk på apply changes når du er ferdig med å fylle inn.

