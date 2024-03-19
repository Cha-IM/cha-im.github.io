---
title: Gruppearbeid i Github
feed: show
date: 19-03-2024
tags:
---

Når flere jobber sammen i et repo i Github er det flere ting man må tenke på.

## 1. Github synkroniserer ikke automatisk
For at ditt arbeid skal vises for de andre på gruppa må du *pushe* endringene dine til Github. Husk å **lagre** filene dine før du pusher, slik at alle endringene blir med.

Når du har pushet må de andre på gruppa *pulle* siste versjon av repoet for å få oppdatert filene de jobber i.

### Synkroniseringskonflikter.
Det kan skje noen uheldige ting når vi gjør dette her er noen vanlige problemer.
1. Du har filer åpne som du ikke har lagret når du puller siste versjon fra Github.
	- Du vil da få en konflikt mellom filene du har åpne og siste versjon av filene du nettopp har lastet ned. Derfor må du huske å **lagre filene dine og pushe endringer FØR du puller**.
2. **Merge conflict**
	- Du får en feilmelding i Github desktop hvis du prøver å pushe en endring der du har endret noe **i samme linje** som noen andre har endret noe. Det er derfor lurt å være enig om hvilke deler av filen dere 