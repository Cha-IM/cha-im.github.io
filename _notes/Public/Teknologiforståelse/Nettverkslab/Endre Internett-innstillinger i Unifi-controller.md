---
title: Endre Internett-innstillinger i Unifi-controller
feed: show
date: 24-10-2024
---

1. Åpne Unifi Controller
2. I raden av ikoner til venstre, klikk på tannhjulet nederst (settings)
3. Velg "Internet"
4. Velg din enhet (*Default (WAN 1)*)
5. Ved *Advanced*, klikk på **Manual**
6. Ved *IPv4 Connection*, velg **Static IP**. Det vil da komme opp tre tekstbokser.
	1. **IPv4 Address**, skriv inn adressen under *WAN IP address* i regnearket [IP-adresser i lab.xlsx](https://tronder.sharepoint.com/:x:/s/IMCharlottenlund/Ef98P9EJRO5NnUspzok7g3gBBj5-aM77rAv5XPjbC24-Ww?e=survQx)
	2. **Subnet mask**: 255.255.255.0
	3. **Router**: 172.31.100.1
7. Ved *IPv6 Connections* lar du den stå på *Disabled*
8. Trykk på **Apply Changes**
9. Deretter venter du litt på at innstillingene trer i kraft, før du sjekker om du har nett (gå inn på nettleseren din og prøv å gå inn på en nettside)