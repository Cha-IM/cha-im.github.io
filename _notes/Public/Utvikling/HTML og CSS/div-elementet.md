---
title: <div>-elementet
feed: show
date: 19-09-2024
---
`<div>` er et element som brukes mye i forbindelse med id- og klassevelgere. `<div>`-taggen gjør i utgangspunktet ingenting med innholdet, men brukes for å gruppere innhold eller til å hekte class eller id på innholdet, slik at man enkelt kan legge CSS-kode eller annen kode til elementet. Du kan legge et hvilket som helst innhold i et `<div>`-element. På grunn av dette er `<div>` en av de mest brukte HTML-taggene, og den brukes ofte i stedet for andre tagger som er mer spesifikke, som for eksempel `<ul>`, `<p>` eller `<table>`.

### Eksempel

```html
<div class=”miniatyrbilde”>
  <img src=”bilde.png”>
  <div class=”bildetekst”>Et bilde</div>
</div>
```

I eksemplet brukes den første `<div>`-en til å gruppere et bilde og en bildetekst, og den andre `<div>`-en brukes til å formatere bildeteksten med class-velger i CSS.

### `<span>`
En annen tag som ligner på `<div>`, er `<span>`. Forskjellen er at `<span>` er såkalt _inline_, som betyr at den kan brukes til å markere enkeltord eller deler av ei linje uten at tekstflyten blir påvirket. `<div>` vil automatisk lage linjeskift før og etter elementet.


*Denne teksten er opprinnelig publisert på [ndla.no]([CSS-velgere - Konseptutvikling og programmering - NDLA](https://ndla.no/subject:1:1352b19e-e706-4480-a728-c6b0a57ba8ae/topic:1:f7b88f8c-5f2f-4ea8-bdcf-1bd4811c37b3/topic:1:df9278b0-7252-4a62-a39c-3107d7f319f1/resource:2e32dd04-efdd-4d73-ad07-10285e7b0c79))*