---
title: Lag en web-app med KI-agent
feed: show
date: 26-02-2026
---
I denne oppgaven skal du sette opp en Web-app med HTML og CSS og Python, med en KI-chatbot som vi kommuniserer med via tjenesten HuggingFace.

## Mål med oppgaven

- Installere Python på Windows 11 og sette opp et isolert virtuelt miljø i VS Code
- Opprette Hugging Face‑konto og generere en API‑nøkkel (Access Token)
- Lage en Flask‑app som
    - leser inn `.txt`‑dokumenter fra en `data/`‑mappe
    - kaller en språkmodell via Hugging Face Inference API
    - viser en chatlogg (brukerens spørsmål og modellens svar)
- Levere en fungerende løsning og kort refleksjon

---

## Forutsetninger

- VS Code er installert (du bruker **Terminal** i VS Code)
- Du har nettleser for å opprette Hugging Face‑konto

---

# Del A — Installer Python (Windows 11)

1. Gå til python.org og last ned siste stabile versjon for Windows.
2. Kjør installasjonsprogrammet.
3. Kryss av for **Add Python to PATH**.
4. Fullfør installasjonen.

Test i VS Code Terminal (Ctrl+ø):

python --version

Får du et versjonsnummer, er alt klart.

---

# Del B — Opprett Hugging Face‑konto og API‑nøkkel

1. Gå til [huggingface.co](https://huggingface.co/) og opprett en gratis konto. Hugging Face Hub og Spaces støtter gratis bruk for læring, prototyper og statisk/lettvektsapper; plattformen lar deg lagre modeller, data og enkle apper gratis. 
2. Når du er innlogget: Klikk på profilbildet ditt → **Settings** → **Access Tokens** → **New token**.
    - Velg et navn, og klikk på *Make calls to Inference Providers*.
    - Trykk på *Create Token*
    - Kopier tokenet og ta vare på det (du trenger det straks).  
    

---

# Del C — Opprett prosjektet i VS Code

1. I VS Code, opprett en ny mappe ved å bruke Explorer:
    
    - Klikk på **New Folder** og gi den navnet: `flask-schoolbot`.
2. Opprett følgende mapper og filer i Explorer
```md
flask-schoolbot/ 
	app.py 
	.env 
	data/ (mappe) 
	templates/ (mappe) 
		index.html 
	static/ (mappe) 
		style.css
```

    
3. Åpne **Terminal** i VS Code (Ctrl+ø) og sørg for at arbeidskatalogen er` flask-schoolbot`(du kan bruke`pwd` for å sjekke).
    

---

# Del D — Lag virtuelt miljø og installer pakker

I VS Code Terminal:

python -m venv venv

.\venv\Scripts\activate

pip install flask python-dotenv requests

Du skal se `(venv)` foran prompten.

---

# Del E — Legg inn skolens dokumenter

- Kopier minst 3 tekstfiler inn i `data/`, for eksempel:
    - `skolerute.txt`
    - `ordensreglement.txt`
    - `fravær.txt`

Kun `.txt` støttes i denne første versjonen.

---

# Del F — Konfigurer .env

Åpne `.env` og fyll inn:

```
HF_TOKEN=DIN_HF_TOKEN_HER
MODEL=mistralai/Mistral-7B-Instruct-v0.3
```

MERK:

- HF_TOKEN er nøkkelen du hentet fra Hugging Face.
- Du kan bytte modell senere ved å endre `MODEL`. Gratis/åpne modeller via Inference API egner seg til undervisning og enkle demoer

---

# Del G — HTML‑skjema (elevene lager resten av HTML/CSS selv)

Åpne `templates/index.html`. Du bestemmer tittel, head, CSS‑kobling osv.  
Men **disse delene må ligge i dokumentet**:

  
```html
<form method="POST">

    <input type="text" name="question" placeholder="Skriv spørsmålet ditt..." />

    <button type="submit">Send</button>

</form>

  

{% if chat %}

<h2>Chatlogg</h2>

<ul>

    {% for item in chat %}

        <li><strong>Du:</strong> {{ item.user }}<br>

        <strong>Bot:</strong> {{ item.bot }}</li>

    {% endfor %}

</ul>

{% endif %}
```

Legg gjerne til egen CSS i `static/style.css` for utseende.

---

# Del H — Flask‑appen (kopier hele filen under til `app.py`)

**Viktig:** Ingen TODO‑merker. Hvis noe kan endres, står det med EGEN KOMMENTARLINJE I STORE BOKSTAVER.

```python
# app.py

# -------------------------------

# En enkel Flask-basert skoleassistent.

# Leser .txt-filer fra ./data og kaller en språkmodell via Hugging Face Inference API.

# Viser chatlogg (bruker-spørsmål og modell-svar).

# -------------------------------

  

from flask import Flask, request, render_template

from dotenv import load_dotenv

import os

import requests

  

# Laster miljøvariabler fra .env (HF_TOKEN og MODEL)

load_dotenv()

  

app = Flask(**name**)

  

# HENTER API-NØKKEL OG MODELLNAVN FRA .env

HF_TOKEN = os.getenv("HF_TOKEN")

MODEL = os.getenv("MODEL")

  

# SJEKKER AT NØKKEL FINNES

if not HF_TOKEN:

    raise RuntimeError("HF_TOKEN mangler i .env. Legg inn din Hugging Face API-nøkkel.")

  

# ENKEL FUNKSJON SOM LESER ALLE .txt-FILER I ./data VED OPPSTART

def load_documents():

    docs = ""

    data_dir = "data"

    if not os.path.isdir(data_dir):

        return docs

  

    for filename in os.listdir(data_dir):

        if filename.endswith(".txt"):

            path = os.path.join(data_dir, filename)

            try:

                with open(path, "r", encoding="utf-8") as f:

                    content = f.read().strip()

                    # Legg til filnavn som skille for tydeligere kontekst

                    docs += f"\n\n### FIL: {filename}\n{content}"

            except Exception as e:

                print(f"Kunne ikke lese {filename}: {e}")

    return docs

  

# LASTER DOKUMENTER EN GANG (VED OPPSTART)

DOCUMENTS = load_documents()

  

# CHATLOGG I MINNET (LISTE AV DIKTIONARIES)

# MERK: DENNE TØMMES HVIS APPEN STARTES PÅ NYTT. FOR VEDVARENDE LAGRING MÅ DU BRUKE DATABASE.

chatlog = []

  

def build_prompt(question: str, chat_history: list) -> str:

    """

    Bygger prompt til språkmodellen.

    - Legger ved dokumentkontekst

    - Legger ved tidligere meldinger i økten (chat_history)

    - Presiserer at model skal svare KUN ut fra dokumentene

    """

    history_text = ""

    for entry in chat_history:

        history_text += f"Bruker: {entry['user']}\nBot: {entry['bot']}\n\n"

  

    prompt = f"""

Du er en hjelpsom skoleassistent. Du svarer KUN basert på informasjon i dokumentene.

Dersom svaret ikke finnes i dokumentene, svar: "Det står ikke i dokumentene."

  

DOKUMENTER:

{DOCUMENTS}

  

TIDLIGERE SAMTALE I DENNE ØKTEN:

{history_text}

  

BRUKERENS SPØRSMÅL:

{question}

  

SVAR:

"""

    return prompt

  

def ask_model(prompt: str) -> str:

    """

    Ringer Hugging Face Inference API med gitt prompt.

    Forventer HF_TOKEN og MODEL fra .env.

    """

    headers = {

        "Authorization": f"Bearer {HF_TOKEN}",

        "Content-Type": "application/json"

    }

    body = {

        "inputs": prompt,

        "parameters": {

            "max_new_tokens": 200,

            "temperature": 0.3

        }

    }

    try:

        resp = requests.post(

            f"[https://api-inference.huggingface.co/models/{MODEL}",](https://api-inference.huggingface.co/models/%7BMODEL%7D%22,)

            headers=headers,

            json=body,

            timeout=60

        )

        data = resp.json()

        # De fleste tekstdemo-modeller returnerer en liste med 'generated_text'

        if isinstance(data, list) and len(data) > 0 and "generated_text" in data[0]:

            return data[0]["generated_text"]

        # Fallback for avvikende svarformat

        return str(data)

    except Exception as e:

        return f"Feil ved kall til modellen: {e}"

  

@app.route("/", methods=["GET", "POST"])

def index():

    """

    Viser forsiden og håndterer innsending av skjema (POST).

    Oppdaterer chatlogg og rendrer index.html med chat-listen.

    """

    global chatlog

  

    if request.method == "POST":

        user_question = request.form.get("question", "").strip()

        if user_question:

            prompt = build_prompt(user_question, chatlog)

            answer = ask_model(prompt)

            chatlog.append({"user": user_question, "bot": answer})

  

    # RENDERER siden med dagens chatlogg

    return render_template("index.html", chat=chatlog)

  

if **name** == "**main**":

    # KJØRER FLASK I UTVIKLINGSMODUS

    # DU KAN ENDR E 'debug=False' HVIS DU IKKE VIL SE RESTART/FEILLOGG I TERMINALEN.

    app.run(debug=True)
```

Hva kan du endre i `app.py` etter kopiering:

- LINJE MED `MODEL` I `.env`: bytt til en annen åpen instruksjonsmodell om ønskelig. (Dette endres i `.env`, ikke i koden.)
- `temperature` og `max_new_tokens` i `ask_model`: juster svarstil og lengde.
- Tekst i `build_prompt`: tone, språk, retningslinjer.

---

# Del I — Start appen og test

1. Sørg for at venv er aktivt i Terminal:

.\venv\Scripts\activate

2. Start appen:

python app.py

3. Åpne nettleser på:

```
http://127.0.0.1:5000
```

4. Still spørsmål som finnes i dokumentene dine. Sjekk at chatloggen bygges opp.

---

# Del J — Feilsøking

- 401/403 eller “mangler nøkkel”: sjekk at `HF_TOKEN` ligger i `.env` og at du har startet appen på nytt etter endringer.
- Tomme svar: sjekk at `data/` inneholder `.txt`‑filer med reelt innhold.
- Sært svar: stram inn prompten i `build_prompt` eller reduser `temperature`.

---

# Del K — Levering

- Hele prosjektmappen (uten `venv/`, hvis lærer ikke vil ha den med)
- Minst tre `.txt`‑filer i `data/`
- Skjermbilde av kjørende app
- Kort refleksjon (2–5 setninger) om hva du lærte

---

## Ekstraoppgave (frivillig): Støtte for PDF, DOCX og Markdown

- Installer ekstra pakker: pip install pdfplumber mammoth
- Utvid `load_documents()`:
    - `.md`: les som vanlig tekst (utf‑8)
    - `.pdf`: bruk `pdfplumber` til å ekstrahere text per side
    - `.docx`: bruk `mammoth` og `extract_raw_text`
- Skriv en kort setning i refleksjonen om hva som fungerte/ikke fungerte.

---
