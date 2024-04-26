---
title: Installer Ruby og Jekyll
feed: show
date: 22-04-2024
---
Før du installerer Jekyll må du installere Ruby. Det er litt forskjellig på Mac og Windows

## Installer Ruby og Jekyll på Mac
Ruby og Jekyll installeres via Terminal på Mac. For å åpne terminal er den enkleste måten å trykke <kbd>cmd</kbd> + <kbd>space</kbd> for å få opp Spotlight-søk og skrive `terminal` og trykke <kbd>Enter</kbd>. Deretter følger du fremgangsmåten på lenken under. Legg merke til at noen av stegene kan ta litt tid, Det er bare å vente til en kommando er fullført, før du limer inn neste. Pass på å lese det som står mellom alle stegene for å være sikker på at du gjør det riktig.
- [Jekyll on macOS (jekyllrb.com)](https://jekyllrb.com/docs/installation/macos/)

## Installer Ruby og Jekyll på Windows
Til Windows kan du laste ned Ruby som et vanlig program. Det beskrives i lenken under, i avsnittet "Installation via RubyInstaller". Last ned Ruby+DevKit og start installasjonen
- [Jekyll on Windows (jekyllrb.com)](https://jekyllrb.com/docs/installation/windows/)
#### Husk disse tingene:
* På siste steg i installasjonen av Ruby+DevKit er det en avkrysningsboks der det står *Run 'ridk install' to set up MSYS2 and development toolchain*. **Denne skal du krysse på**, slik at det ser ut som på bildet under.
![](https://github.com/Cha-IM/cha-im.github.io/blob/main/assets/img/jekyll/ruby-devkit-install-ridk-install.png?raw=true)
* Når du har klikket på *Finish* kommer det opp et kommandovindu med tre valg. Du skal da skrive **3** (tallet som står ved *MSYS2 and MINGW development toolchain*) og trykke **Enter**. Nå vil disse tjenestene installeres i kommandovinduet. Det vil ta litt tid, bare vent til det er ferdig, og lukk vinduet når du er sikker på at det er ferdig.
![](https://github.com/Cha-IM/cha-im.github.io/blob/main/assets/img/jekyll/ruby-devkit-install-msys2-mingw.png?raw=true)
*  Nå skal du åpne et nytt kommandovindu. Klikk på **Startmenyen** og skriv *CMD* og trykk på **Enter**
* Når kommandovinduet åpner seg, skriver du `gem install jekyll bundler` og trykker på **Enter**. Da vil Jekyll installeres i komandovinduet. Bare vent til det er ferdig.
![](https://github.com/Cha-IM/cha-im.github.io/blob/main/assets/img/jekyll/ruby-devkit-install-jekyll-bundler.png?raw=true)
* Når installasjonen er ferdig kan du skrive `jekyll -v` for å sjekke om det er installert. Denne kommandoen viser deg hvilken verson av Jekyll du har installert.
![](https://github.com/Cha-IM/cha-im.github.io/blob/main/assets/img/jekyll/ruby-devkit-install-ruby-v.png?raw=true)