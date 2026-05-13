---
title: Fra kravspesifikasjon til backlog
feed: show
date: 12-05-2026
---
Når dere har lagd en kravspesifikasjon er det fortsatt en del å gjøre før dere kan starte på selve prosjektet. Kravspesifikasjonen sier noe om hvordan det endelige produktet skal fungere, men den sier ikke noe om hvordan dere skal lage det. For å finne ut av det må dere lage en *produktbacklog*. Dette er en liste over alle de konkrete oppgavene dere må gjøre for å realisere produktet.

Som et eksempel skal vi se for oss at vi skal lage en web-app der brukerne kan lage ulike topp 5-lister ned f.eks. sine favorittsanger, favorittfilmer, tv-serier, band eller lignende. Vi kan da se for oss følgende kravspesifikasjon:

#### Funksjonelle krav
| **ID**  | **Krav**                  | **Beskrivelse**                                                                                                       |
| ------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **FK1** | **Brukerregistrering**    | Brukere må kunne opprette en profil med e-post, brukernavn og passord.                                                |
| **FK2** | **Opprettelse av lister** | Brukere skal kunne lage en liste ved å velge en kategori, gi listen en tittel og legge inn 5 elementer (rangert 1–5). |
| **FK3** | **Søkefunksjon**          | Det skal være mulig å søke etter lister basert på kategori, tittel eller brukernavn.                                  |
| **FK4** | **Redigering**            | Brukere må kunne endre eller slette egne lister i etterkant.                                                          |
| **FK5** | **Sosial interaksjon**    | Brukere skal kunne "like" andres lister og legge inn kommentarer.                                                     |
| **FK6** | **Bildefunksjonalitet**   | Mulighet for å laste opp eller hente inn et miniatyrbilde for hvert element i listen.                                 |
| **FK7** | **Kategorisering**        | Systemet skal ha forhåndsdefinerte kategorier (Musikk, Film, spill, etc.), men også tillate "Annet".                  |

#### Ikke-funksjonelle krav
| **ID**   | **Kategori**             | **Krav**                                                                                         |
| -------- | ------------------------ | ------------------------------------------------------------------------------------------------ |
| **IFK1** | **Responstid**           | Sider skal laste på under 2 sekunder ved normal bruk.                                            |
| **IFK2** | **Responsivt design**    | Webappen skal fungere optimalt på både desktop, nettbrett og mobil (Mobile First).               |
| **IFK3** | **Sikkerhet**            | Alle passord skal hashes i databasen, og brukersesjoner skal sikres med HTTPS.                   |
| **IFK4** | **Universell utforming** | Appen skal følge WCAG 2.1-standarden for tilgjengelighet (kontrast, skjermleservennlighet).      |
| **IFK5** | **Brukervennlighet**     | Det skal ikke kreves mer enn 3 klikk for å starte prosessen med å lage en ny liste fra forsiden. |
## Minimum Viable Product (MVP)
Det er vanlig å tenke at man skal starte med å lage en versjon av det endelige produktet som fungerer som en fullstendig app, men som har med kun de absolutt nødvendige funksjonene. Målet er å lage en smal, men fungerende versjon av skuttproduktet som kan tas i bruk med en gang. Etter dette fortsetter man å videreutvikle produktet til man fullfører alle funksjonene man har planlagt i kravspesifikasjonen.

Målet med en MVP er at man kan bruke denne til å faktisk finne ut om folk vil bruke den ferdige appen - man sjekker om ideen var god, uten at man har brukt mye tid på å perfeksjonere en fullstendig app.

I eksempelet med topp 5-appen kan vi lage en MVP ved å starte med kun FK1, FK2 og FK4 og lage en fullstendig app som dekker disse tre kravene. Legg merke til at MVP skal være brukbart, så man må fortsatt ha en ferdig designet app med både frontend og backend som fungerer. Vi har da en app med nok funksjoner til at den kan testes, men som kan bygges ut senere.

## Epics
Det første man gjør når man skal gå fra kravspesifikasjon til produktbacklog er å identifisere hovedtemaene. I softwareutvikling kalles dette ofte *Epics*. En Epic er et stort mål som inneholder mange små oppgaver. Da ser man på både funksjonelle og ikke-funksjonelle krav i kravspesifikasjonen og slår sammen de som hører til under samme tema. 
I eksempelet vårt over kan vi trekke ut FK1 (brukerregistrering) og IFK3 (sikkerhet) til en Epic vil kaller *Autentisering*. FK2 (opprettelse), FK4 (redigering) og FK7 (kategorier) blir til *Epic: Listehåndtering*.

## Brukerhistorier
Når vi har identifisert alle epics skal vi bryte ned disse til enkeltoppgaver. Vi tar utgangspunkt i hva en bruker skal kunne gjøre i appen og lager *brukerhistorier*. En brukerhistorie ser sånn ut:

	"Som en [type bruker] vil jeg [handling], slik at jeg [gevinst]"
For eksempel:
- Som en *bruker* vil jeg kunne *lage lister i forskjellige kategorier*, slik at jeg kan *dele mine favoritter med andre*.
- Som en *bruker* vil jeg *logge inn*, slik at jeg kan *se mine lagrede lister*
- Som en *bruker* vil jeg kunne *se andre sine lister*, slik at jeg kan *gi dem stjerner*.
- Som en *moderator* vil jeg kunne *skjule brukere sine lister*, slik at jeg kan *fjerne upassende innhold*.

## Teknisk dekomponering
Når vi har lagd brukerhistoriene må vi finne ut hvilke spesifikke oppgaver som må gjøres for å oppfylle hver enkelt brukerhistorie. Hver av brukerhistoriene trenger mest sannsynlig både elementer fra frontend, backend og database. Vi må derfor bryte ned historiene. 

### Eksempel
Brukerhistorien "Som en bruker vil jeg logge inn, slik at jeg kan se mine lagrede lister" krever at vi har registrert brukere og lagret lister i en database, at vi har en innloggingsside og et skjema for å legge inn lister. Dette kan vi bryte ned slik:
- **Backend**: Lage POST-rute for å sende innloggingsinfo til databasen (POST /login).
- **Database**: Opprette tabell for brukere i databasen med brukernavn og hashet passord
- **Frontend**: Lage UI-komponent for innlogging (to input-felter og en knapp)
- **Frontend**: Koble skjemaet til POST-ruta.
- **Backend**: Lage POST-rute for å sende listedata til databasen (POST /api/lists)
- **Database**: Opprette tabell for lister i databasen og koble denne til brukere
- **Frontend**: Lage UI-komponent for liste-skjema (5 nummererte input-felter, combobox for kategori og knapp).
- **Frontend**: Koble skjemaet til POST-ruta (API)

## Backlog/issues
Når vi har brutt ned alle Epics og har en lang liste med korte oppgaver, kan vi samle alle disse i en backlog. Hver oppgave i backlogen skal være sånn at en person kan gjennomføre oppgaven alene i løpet av en eller to dager.

Nå kan vi legge inn oppgavene i backlogen i Github-repoen vår, som Issues. Da blir det enkelt for hele teamet å se hva som må gjøres, og man kan se status på oppgavene om de er gjort, og av hvem.

