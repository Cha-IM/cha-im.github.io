

## Forberedelser

- Last ned programmet Rufus her: [Rufus - Lag en oppstartbar USB-stasjon på den enkle måten](https://rufus.ie/nb/).
- Last ned Proxmox VE her: [Proxmox VE 9.2 Installer](https://enterprise.proxmox.com/iso/proxmox-ve_9.2-1.iso).
- Last ned Windows 11 her: [Download Windows 11](https://www.microsoft.com/en-us/software-download/windows11).
	- Gå til **Download Windows 11 Disk Image (ISO) for x64 devices**, velg **Windows 11 multi-edition ISO for x64 devices** i nedtrekksmenyen, og klikk **Confirm.**
	- Under **Select the product language**, velg **Norwegian** eller **English**, og klikk **Confirm**.
	- Klikk på **64-bit download**. ISO-filen vil nå begynne å laste ned.

### Lag Proxmox USB-installasjonsmedium med Rufus
- Åpne Rufus
- Sett inn en USB-penn i PC-en din
	- Rufus vil automatisk kjenne igjen USB-pennen
- Klikk på **VELG** ved siden av **Oppstartstype**, og velg ISO-filen du vil lage oppstartbar (*proxmox-ve_9.2-1.iso*)
- Klikk på **START**
	- Når den grønne Progressbaren er ferdig og det står **KLAR**, kan du ta ut minnepennen. 
- Gjenta samme prosess for den andre minnepennen, med det andre

## Lag et Proxmox-tilpasset Windows USB-installasjonsmedium med Rufus
- Åpne Rufus
- Sett inn en USB-penn i PC-en din
	- Rufus vil automatisk kjenne igjen USB-pennen
- Klikk på **VELG** ved siden av **Oppstartstype**, og velg ISO-filen du vil lage oppstartbar (*Win11_25H2_Norwegian_x64_v2*)
- Gjør valgene likt som på bildet:
![[Rufus-win-1.png]]
- Trykk på START. Du vil da få opp et vindu med tittelen **Windows brukeropplevelse**. Gjør samme valgene som på bildet for å få en enklere Windows-installasjon:
![[Rufus-win-2.png]]- Klikk **OK** og vent til prosessen er ferdig.