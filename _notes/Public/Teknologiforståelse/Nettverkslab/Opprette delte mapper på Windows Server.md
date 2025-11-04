---
title: Opprette delte mapper på Windows Server
feed: show
date: 04-11-2025
---
*NB: Denne artikkelen er skrevet av en KI-chatbot, og ikke kvalitetssikret. Den kan inneholde feil. Ta kontakt hvis du oppdager feil.*

Her er en guide for hvordan du setter opp **delte mapper på en Windows Server-filserver**, slik at brukere kan koble seg til dem via **nettverksstasjoner (folder mapping)** – enten manuelt eller automatisk via **Group Policy (GPO)**.

---

## 🗂️ Del 1: Opprett og del mapper

### 1. Opprett mappen

- Lag en mappe, f.eks. `D:\Felles`.
- Gi den et beskrivende navn, f.eks. `Felles`, `Prosjekt`, `Avdeling`, etc.

### 2. Del mappen

1. Høyreklikk på mappen → **Properties** → **Sharing**-fanen.
2. Klikk **Advanced Sharing** → Huk av for **Share this folder**.
3. Gi et navn, f.eks. `Felles`.
4. Klikk **Permissions**:
    - Fjern "Everyone"
    - Legg til relevante AD-grupper (f.eks. `Avdeling_IT`)
    - Gi ønskede rettigheter (Read, Change, Full Control)

### 3. NTFS-tillatelser (Security-fanen)

- Juster tilgang basert på AD-grupper.
- Eksempel:
    - `Avdeling_IT`: Full Control
    - `Avdeling_Økonomi`: Read

---

## 🧭 Del 2: Koble brukere til mappen via Group Policy (GPO)

### 1. Åpne Group Policy Management

- På en DC: Start **Group Policy Management Console (GPMC)**.

### 2. Opprett eller rediger en GPO

- Høyreklikk på ønsket OU → **Create a GPO** eller rediger en eksisterende.

### 3. Konfigurer Folder Mapping

1. Gå til: User Configuration → Preferences → Windows Settings → Drive Maps
2. Høyreklikk → **New → Mapped Drive**
3. Sett følgende:
    - **Action**: `Create`
    - **Location**: `\\ServerNavn\Felles`
    - **Drive Letter**: Velg f.eks. `F:`
    - **Label**: `Fellesmappe`
    - Huk av for **Reconnect** hvis ønskelig

### 4. Filtrer med sikkerhet (valgfritt)

- Under **Common**-fanen → Huk av for **Item-level targeting**
- Legg til filter basert på gruppe, bruker, OS, etc.

---

## 🧪 Del 3: Test og verifiser

- Logg inn med en bruker i riktig OU.
- Åpne **File Explorer** → Se om nettverksstasjonen vises.
- Test lesing og skriving i mappen.

---

## 🛠️ Alternativ: Manuell tilkobling

Brukere kan også koble til manuelt:

net use F: \ServerNavn\Felles

Eller via File Explorer:

- Høyreklikk på "Denne PC-en" → **Koble til nettverksstasjon**

---
