---
title: Oppsett av Creality Print
feed: show
date: 25-11-2025
---
![](/assets/img/3dprint/crealitylogo.png)

## Last ned Creality Print
1. Gå til [Creality Print](https://www.creality.com/download).
2. Last ned Creality Print og installer.

## Første oppsett av Creality Print
1. Det kommer nå opp en guide om å legge til printer preset i Creality Print.
2. ![](/assets/img/3dprint/crealityprint1.png)
3. Trykk skip på denne.
4. Finn og trykk på denne menyen øverst til venstre i Creality Print:
![](/assets/img/3dprint/crealityprint2.png)
<br>
5. Velg 'Select/Remove printers(system presets)':
![](/assets/img/3dprint/crealityprint3.png)
<br>
6. Under 'Flagship Series', finn 3D printeren vi skal bruke som heter 'Creality K1 Max' og huk av printeren:
![](/assets/img/3dprint/crealityprint4.png)
<br>
7. Da har vi lagt til rett printer i Creality Print. Da må vi passe på at vi bruker samme type plate som ligger i printeren. Akkurat nå er det en 'Textured PEI Plate' som står i printeren. Så velg dette under 'Bed Type':
![](/assets/img/3dprint/crealityprint5.png)
<br>

## Hvordan Slice en modell
1. Importer modellen din (.STL filen) inn i Creality Print. Enten ved å dra den rett inn i programmet eller ved å trykke på File -> Import -> Import 3MF/STL/STEP/SVG/OBJ/AMF... eller bruk hurtigtasten 'CTRL + I':
![](/assets/img/3dprint/crealityprint6.png)
<br>
2. Plasser modellen din, vanligvis midt på platen. 
3. For å bevege deg rundt i programmet, så bruker du høyre klikk for å snu på kameraet og mellommus for flytte på kameraet.
4. Det som er viktig å huske er at 3D-printeren smelter plast og bygger oppover. Det vil si at man må passe på om det er noen deler av modellen flyter i luften, så vil ikke dette printe. Og printen vil ikke fungere. *Det er dessverre ikke slik tyngdekraften fungerer.* Så hvis dere har en modell som ser slik ut med masse elementer som henger i lufta, så må vi se på noe som heter 'Supports':
![](/assets/img/3dprint/crealityprint7.png)
<br>
5. For å lage supports så finnes det 2 måter. Den ene måten lager vi 'Globalt', dette gjelder da alle modellene som er i printen deres. (Det går an å 3D printe flere modeller samtidig, men det skal jeg vise dere litt lenger ned). Også har vi en måte som gjelder kun for modellen som er valgt. Dette er den beste måten å gjøre det på, spesielt hvis det er flere modeller i printen, hvor en eller flere ikke trenger supports.
6. Trykk på modellen din for å velge den. Så trykker du på 'Objects'
![](/assets/img/3dprint/crealityprint8.png)
<br>
7. Huk av 'Enable support' og velg en Type. Da kan velge mellom Normal og Tree. Du kan også velge mellom auto og manual. Auto; så lager Creality Print supports for deg. Velger du manual så må du male på modellen hvor du vil ha support. Velg Tree eller Normal auto så kan Creality Print gjøre dette for deg:
![](/assets/img/3dprint/crealityprint9.png)
<br>
8. Det er fordeler og ulemper med både Normal og Tree. Normal er mer robust, men bruker ofte mer filament, tar lengre tid (ikke alltid) og er ofte vanskligere å ta av. Mens Tree er printer ofte kjappere, bruker mindre filament, men er ikke like robust som Normal. Under her så kan du se hvordan de ser ut:<br>
### Normal:
![](/assets/img/3dprint/crealityprint10.png)
<br>
### Tree:
![](/assets/img/3dprint/crealityprint11.png)
<br>
9. Når du er klar for å eksportere modellen, så må dere først trykke på 'Slice Print'
![](/assets/img/3dprint/crealityprint12.png)
<br>
10. Da får du informasjon om hvor lang tid det tar, hvor mye filament den bruker og du kan se hvordan den printer lag for lag: 
![](/assets/img/3dprint/crealityprint13.png)
<br>
11. Da har Creality Print klargjort en 'gcode' fil, som blir brukt i printeren slik at den vet hva den skal gjøre til en hver tid. Da må vi eksportere filen ved trykke på pilen ved siden av 'Send Print' og velg 'Export G-code':
![](/assets/img/3dprint/crealityprint14.png)
<br>
12. Legg denne på en minnepenn for å få den inn i 3D printeren.

### Du har laget en printeklar fil!