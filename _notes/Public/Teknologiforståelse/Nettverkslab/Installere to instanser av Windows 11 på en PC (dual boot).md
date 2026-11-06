---
title: Installere to instanser av Windows 11 på en PC (dual boot)
feed: show
date: 05-11-2026
---
![](assets/img/dual-boot-win11/IMG_5342.jpeg)## Før du starter

- Lag en oppstartbar USB-minnepenn med Windows 11 ved hjelp av [Rufus](https://rufus.ie/nb/).
- Trekk ut nettverkskabelen på PC-en du skal installere Windows på.

## Installasjon av Windows 11 fra minnepenn - instans 1

Sett inn den oppstartsbare minnepennen og start datamaskinen mens du gjentatte ganger trykker på <key>F11</key>.

![](/assets/img/dual-boot-win11/IMG_5334.jpeg)

Du vil da komme inn i oppstartsmenyen. Velg USB-minnepennen og trykk på Enter.

![](/assets/img/dual-boot-win11/IMG_5335.jpeg)


## Windows 11-installasjon
### Innstillinger for installasjonen

Velg språk og tastaturoppsett.

<div style="display: flex;flex-direction:row;">
<div>
<img src="/assets/img/dual-boot-win11/IMG_5336.jpeg">
</div>
<div>
<img src="/assets/img/dual-boot-win11/IMG_5337.jpeg">
</div>

</div>

Velg **Install Windows 11** og hak av på *I agree everything will be deleted including files, apps and settings*

![](assets/img/dual-boot-win11/IMG_5338.jpeg)

Product key: Trykk på *"I don't have a product key*

![](assets/img/dual-boot-win11/IMG_5339.jpeg)

Velg Windows-versjon: **Windows 11 Pro Education**

![](assets/img/dual-boot-win11/IMG_5340.jpeg)

## Partisjonering
Siden vi skal installere to instanser av Windows må vi lage to partisjoner, som hver tar opp halve disken. Når du skal installere den første instansen, sletter du alle partisjoner på **Disk 0**.

Velg en og en partisjon og trykk på **Delete partition**
![](assets/img/dual-boot-win11/IMG_5342.jpeg)

Når du har slettet alle partisjoner på Disk 0, skal det stå **Disk 0 Unallocated Space**. Det betyr at Disk 0 er tom.

![](assets/img/dual-boot-win11/IMG_5343.jpeg)

Du skal nå lage en partisjon som tar halve disken. Trykk på **Create Partition**, og fyll ut hvor stor partisjonen skal være i feltet der det står **Size in MB**. Her skriver du omtrent halvparten av det som er fylt ut fra før, i dette tilfellet omtrent 238.000 MB. Trykk på **Apply** og vent til de nye partisjonene kommer opp i lista.

![](assets/img/dual-boot-win11/IMG_5345.jpeg)

Windows lager nå tre partisjoner. Velg den største (Disk 0 Partition 3), og trykk **Next**

![](assets/img/dual-boot-win11/IMG_5346.jpeg)