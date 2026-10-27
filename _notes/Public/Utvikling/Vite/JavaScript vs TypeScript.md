

TypeScript er en variant av JavaScript der man har inkludert datatyper. Dette gjør at utviklingsmiljø som VS Code lettere kan oppdage om det kommer til å oppstå feil i koden din som kommer av at variabler har feil type.

Her skal jeg forklare hovedforskjellen på TypeScript og JavaScript.

## Variabler
Når vi deklarerer variabler i JavaScript bryr vi oss ikke om hvilken datatype som skal lagres i variablene. I JS blir datatypen satt først når vi gir variabelen en verdi, og datatypen kan også endre seg om vi endrer verdien til en annen datatype.

F.eks. er dette godkjent i JS:

```js
let verdi = 3

verdi = "Hei"

verdi = true
```

Dette vil ikke fungere i TypeScript. Der måtte det vært tre forskjellige variabler:

```ts
let tall: number = 3

let tekst: string = "Hei"

let erSann: boolean = true
```

Hvis vi hadde prøvd å endre verdien av `tall` til f.eks. `"hei"`, ville koden fått en rød strek under seg i VS Code.

## Henting av 