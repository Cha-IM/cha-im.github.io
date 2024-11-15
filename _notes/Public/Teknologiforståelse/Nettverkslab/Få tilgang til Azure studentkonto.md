---
title: Få tilgang til Azure studentkonto
feed: show
date: 19-03-2024
tags: []
---
## Steg 1: Chamedia e-postadresse
Du vil motta en Chamedia e-postadresse fra skolen. Denne e-posten består av ditt elevnummer + @chamedia.no (eksempel: elevXXXXXX@chamedia.no).

<img src="/assets/img/nettverkslab/onecomforward.png" style="float:right;width:50%">
Du skal ha fått en e-post fra **one.com Kundservice** på skole-eposten din (Outlook) med emnet **Verifiser videresending av e-post fra chamedia.no**


## Steg 2: Legg til adressen til en (personlig) Microsoftkonto
Denne e-postadressen må du legge til i en Microsoft-konto. Her kan du velge å legge til e-posten i din personlige Microsoft-konto (ikke trøndelag-kontoen), eller så kan du opprette en ny Microsoft konto med den e-postadressen.

### Lag ny konto:
1. Gå til [signup.live.com](https://signup.live.com)
2. Skriv inn @chamedia.no-e-postadressen din, og fortsett videre med å opprette kontoen. 
4. Spørsmål? Følg denne guiden fra Microsoft: [Slik oppretter du en ny Microsoft-konto](https://support.microsoft.com/nb-no/account-billing/slik-oppretter-du-en-ny-microsoft-konto-a84675c3-3e9e-17cf-2911-3d56b15c0aaf)


## Steg 3: Logg på Azure for students
Logg inn på Microsoft Azure gjennom student-innloggingen. Uansett om du har laget en ny konto med chamedia e-postadressen eller om du har lagt til e-postadressen i en eksisterende personlig konto, skal du logge inn i Azure ved å skrive inn chamedia e-postadressen din i innloggingsfeltet i [Azure login (Microsoft.com)](https://azure.microsoft.com/nb-no/free/students) (Klikk på den grønne knappen "Start gratis")

Skriv inn passordet ditt, og så må du bekrefte identiteten din med en sikkerhetskode som blir sendt til @chamedia-adressen din. Mail til denne adressen vil du motta på skole-eposten din (elevXXXXXX@skole.trondelagfylke.no).

Når du har logget inn med sikkerhetskoden vil du komme til et skjema der du skal fylle ut info om deg og skolen (navn, land, skolenavn, fødselsdato). Under **Skolens e-postadresse** skriver du in din @chamedia.no-adresse. Klikk på **Kontroller akademisk status**.

Du skal nå ha tilgang til Azure for students

## Steg 4: Hent ut Lisensnøkler
Naviger til [Software(Azure.com)](https://portal.azure.com/#view/Microsoft_Azure_Education/EducationMenuBlade/~/software)

Finn den versjonen av Windows du skal ha lisensen til (Windows 11 Education, Version 23H2 og Windows Server 2019 Standard (updated Mar 2023)), og trykk “Vis produktnøkkel”

## Steg 5: Aktiver maskinen din

### For Klient-PC:

1. Se til at maskinen din er tilkoblet nett
2. Gå til Innstillinger > System > Aktivering > Oppdater produktnøkkel > Endre produktnøkkel.
3. Skriv inn Windows 11 Education, Version 23H2-produktnøkkelen du fikk fra Azure.
4. Maskinen din vil gjennomføre en omstart før den er ferdig-aktivert. 
Spørsmål? [Følg denne guiden fra Microsoft (microsoft.com)](https://support.microsoft.com/nb-no/windows/aktivere-windows-c39005d4-95ee-b91e-b399-2820fda32227)

### For Server-PC:
1. Åpne ledetekst som administrator (også kjent som CMD) ved å høyreklikke på Windows-ikonet på skrivebordet, og velg “Ledeteskt (administrator)”.
2. Skriv inn følgende kommando I vinduet som åpnes: 
	`DISM /online /Set-Edition:ServerStandard /ProductKey:(**product key**) /AcceptEula`
4. Bytt ut (**product key**) med din produktnøkkel. 
	Eksempel: `DISM /online /Set-Edition:ServerStandard /ProductKey:N69G4-B89J2-4G8F4-WWYCC-J464C /AcceptEula`
6. Trykk enter på tastaturet, og følg eventuelle instrukser på skjemen. Får du spørsmål om å bekrefte ved å skrive y eller n, skriver du y og trykker enter
7. Maskinen vil begyne prosessen med å oppgradere Windows-versjonen fra Windows Server 2019 Standard Evaluation til Windows Server 2019 Standard. Denne prosessen kan ta opp til 15 minutter, så smør deg med tålmodighet.
8. Maskinen vil gjennomføre en omstart før den er ferdig aktivert. Det kan være du må bekrefte omstarten ved å skrive inn y i ledetekst-vinduet før maskinen kan gjennomføre en omstart.


Guiden er laget av Scott Bloomberg.