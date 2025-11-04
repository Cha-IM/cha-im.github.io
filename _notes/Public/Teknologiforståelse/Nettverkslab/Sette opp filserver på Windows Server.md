---
title: Sette opp filserver på Windows Server
feed: show
date: 04-11-2025
---
*NB: Denne artikkelen er skrevet av en KI-chatbot, og ikke kvalitetssikret. Den kan inneholde feil. Ta kontakt hvis du oppdager feil.*

Her er en komplett guide for å sette opp en **filserver på Windows Server** og konfigurere **hjemmemapper for brukere via Active Directory (AD)**, slik at brukere automatisk får tilgang til sin egen nettverksmappe ved pålogging.

---

## 🖥️ Del 1: Oppsett av filserver

### 1. Installer filserverrollen

1. Åpne **Server Manager**.
2. Gå til **Manage > Add Roles and Features**.
3. Velg:
    - **Role-based or feature-based installation**
    - Serveren du vil bruke
4. Under **Roles**, huk av:
    - **File and Storage Services**
    - Under denne: **File Server**
5. Fullfør installasjonen og start serveren om nødvendig.

---

## 📁 Del 2: Opprett en delt mappe for hjemmemapper

### 1. Opprett en mappe

- F.eks. `D:\HomeFolders`

### 2. Del mappen

1. Høyreklikk på mappen → **Properties** → **Sharing**-fanen.
2. Klikk **Advanced Sharing** → Huk av for **Share this folder**.
3. Sett et navn, f.eks. `Home$` (dollar-tegnet gjør den skjult).
4. Klikk **Permissions**:
    - Fjern "Everyone"
    - Legg til **Authenticated Users** eller en AD-gruppe
    - Gi **Full Control**

### 3. NTFS-tillatelser (Security-fanen)

1. Gå til **Security**-fanen.
2. Legg til **CREATOR OWNER** med **Full Control**.
3. Legg til **Domain Users** med:
    - **List folder contents**
    - **Create folders / append data**
4. Fjern "Everyone" hvis den finnes.

---

## 👥 Del 3: Konfigurer hjemmemapper via AD

### 1. Åpne **Active Directory Users and Computers (ADUC)**

### 2. Rediger brukere

1. Høyreklikk på en bruker → **Properties**.
2. Gå til **Profile**-fanen.
3. Under **Home folder**:
    - Velg **Connect**: f.eks. `H:`
    - Skriv inn sti: `\\ServerNavn\Home$\%username%`

> `%username%` gjør at hver bruker får sin egen mappe automatisk.

### 3. Automatiser for flere brukere

- Bruk **PowerShell** eller **Group Policy** for å sette hjemmemappe for mange brukere samtidig.

Eksempel PowerShell:

Get-ADUser -Filter * -SearchBase "OU=Brukere,DC=eksempel,DC=no" | ForEach-Object {

    $homeDir = "\Filserver\Home$\" + $_.SamAccountName_

    _Set-ADUser $_ -HomeDirectory $homeDir -HomeDrive "H:"

}

---

## 🧪 Test

- Logg inn med en AD-bruker på en klient-PC.
- Sjekk at `H:`-stasjonen vises og peker til brukerens mappe.

---
