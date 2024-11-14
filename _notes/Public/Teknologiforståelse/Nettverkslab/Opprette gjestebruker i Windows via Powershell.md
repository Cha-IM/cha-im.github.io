---
title: Opprette gjestebruker i Windows via Powershell
feed: show
date: 14-11-2024
---
![[/assets/img/PowerShellScripting.jpg]]
1. <img src="/assets/img/rightclickstartmenu.png" style="float:right;height:10em">Åpne kommandolinjen ved å **høyreklikke** på **Start** og velg **Ledetekst (Administrator)** eller **Powershell (Administrator)**. _Hva de heter kommer an på din versjon av Windows_ 
2. Skriv in følgende kommando: `net user Gjest /add /active:yes`
3. Når kontoen er laget, vil du få spørsmål om å legge til et passord. Det skal vi **ikke** gjøre. Trykk på **Enter** for å hoppe over det.
4. Deretter må vi slette gjestekontoen fra brukergruppen og legge den til en egen gruppe for gjestebrukere. Skriv in følgende kommandoer:

- `net localgroup users TWC /delete`
- `net localgroup guests TWC /add`

Nå har du opprettet en gjestebruker.