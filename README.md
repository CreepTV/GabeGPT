# GabeGPT - Kostenloser KI-Chatbot (2025)

Ein vollständig kostenloses KI-Chatbot-System mit HuggingFace Spaces + GitHub Pages.

**Kosten: 0€** ✅

---

## 🚀 Setup-Anleitung

### SCHRITT 1: HuggingFace Space erstellen

1. Gehe zu https://huggingface.co/spaces
2. Klick "Create new Space"
3. Wähle diese Einstellungen:
   - **Name:** `gabegpt` (oder dein Name)
   - **License:** OpenRAIL
   - **Space SDK:** Docker
   - **Visibility:** Public

4. Klick "Create Space"

### SCHRITT 2: Code zum Space hochladen

1. Klone deinen neuen Space lokal:
   ```bash
   git clone https://huggingface.co/spaces/DEIN_USERNAME/gabegpt
   cd gabegpt
   ```

2. Kopiere folgende Dateien aus deinem GabeGPT Projekt:
   - `app.py` → in den Space Ordner
   - `requirements.txt` → in den Space Ordner

3. Erstelle einen `documents` Ordner:
   ```bash
   mkdir documents
   ```
   
   Hier kannst du später PDF/TXT-Dateien hochladen.

4. **Wichtig:** Änder die `requirements.txt` - HF Spaces können nicht alle Libraries automatisch installieren. Nutze stattdessen:
   ```bash
   pip install -r requirements.txt
   ```

5. Git Commit & Push:
   ```bash
   git add .
   git commit -m "Initial commit"
   git git push
   ```

   Der Space wird automatisch gebaut und deployed!

6. Nach 5-10 Minuten → Space ist live unter:
   ```
   https://DEIN_USERNAME-gabegpt.hf.space
   ```

### SCHRITT 3: GitHub Pages Setup

1. Erstelle ein GitHub Repo namens `gabegpt` oder `username.github.io`

2. Lade die `index.html` in dein Repo hoch (oder push lokal):
   ```bash
   git clone https://github.com/YOUR_USERNAME/gabegpt
   cd gabegpt
   
   # Kopiere index.html hierhin
   # Editiere die HuggingFace URL in index.html:
   ```

3. **WICHTIG:** In `index.html` Zeile 125 ersetzen:
   ```javascript
   const HUGGINGFACE_SPACE_URL = 'https://YOUR_USERNAME-gabegpt.hf.space';
   ```
   
   Mit deiner echten Space URL!

4. Aktiviere GitHub Pages:
   - Repo Settings → Pages
   - Source: `main` branch, root folder
   - Save

5. Deine Website ist live unter:
   ```
   https://YOUR_USERNAME.github.io/gabegpt
   ```
   oder
   ```
   https://github.com/pages/YOUR_USERNAME/gabegpt
   ```

---

## 📚 Eigene Dokumente hinzufügen

1. Platziere TXT/PDF-Dateien im HuggingFace Space unter `documents/`

   Beispiel: `documents/mein_wissen.txt`

2. Der Bot nutzt automatisch **RAG** (Retrieval Augmented Generation):
   - Sucht die relevantesten Stellen aus deinen Dokumenten
   - Antwortet basierend auf deinem Wissen

3. Formate:
   ```
   documents/
   ├── anleitung.txt
   ├── faq.txt
   └── berichte.txt
   ```

---

## 🤖 Modelle-Optionen

Alle sind kostenlos auf HuggingFace:

| Modell | Größe | Geschwindigkeit | Qualität |
|--------|-------|-----------------|----------|
| Llama 2 7B Chat | 7B | ⚡⚡⚡ | ⭐⭐⭐ |
| Mistral 7B Instruct | 7B | ⚡⚡⚡ | ⭐⭐⭐ |
| Phi 3 Mini | 3.8B | ⚡⚡⚡⚡ | ⭐⭐⭐ |
| Gemma 2 7B | 7B | ⚡⚡⚡ | ⭐⭐⭐ |

**Empfehlung:** 
- Schnell & Kostenlos: **Phi 3 Mini**
- Beste Qualität: **Llama 2 7B Chat** oder **Mistral 7B**

Ändere in `app.py` Zeile 10:
```python
MODEL_NAME = "meta-llama/Llama-2-7b-chat-hf"
```

---

## ⚙️ Konfiguration

### System Prompt anpassen

In `app.py` Zeile 16-19:
```python
SYSTEM_PROMPT = """Du bist GabeGPT, ein hilfreicher KI-Assistent. 
Antworte auf Deutsch, sei freundlich und präzise.
Basiere deine Antworten auf den verfügbaren Dokumenten."""
```

Ändere diese Instructions nach Bedarf!

### Chat-Parameter

In `app.py` um Zeile 200:
```python
response = chat_with_rag(
    message,
    max_tokens=512,      # Antwortlänge
    temperature=0.7,     # 0=präzise, 1=kreativ
    top_p=0.9            # Diversität
)
```

---

## 🆘 Troubleshooting

### "HuggingFace Space lädt ewig"
- Check: Space Logs auf HF (Spaces → Settings → Logs)
- Modell zu groß? Nutze **Phi 3 Mini** statt Llama

### "Frontend kann nicht mit Space kommunizieren"
- CORS muss aktiviert sein
- `index.html` URL prüfen
- Browser Console öffnen (F12) → Netzwerk-Fehler ansehen

### "Modell kann nicht geladen werden"
- Nutze das Gradio Interface für 8-bit quantization
- Oder wechsel zu **HuggingFace Inference API** (kostenlos!)

---

## 🔗 API-Integration (Advanced)

Falls du statt Gradio ein Custom API möchtest:

**In `app.py`** den FastAPI-Code uncommented (Zeile ~220):

```python
from fastapi import FastAPI

app = FastAPI()

@app.post("/api/chat")
async def api_chat(request: ChatRequest) -> ChatResponse:
    response = chat_with_rag(request.message, request.history)
    return ChatResponse(response=response)
```

Dann `requirements.txt` nutzen und deployen.

---

## 📌 Zusammenfassung

```
GitHub Pages (Webseite)
        ↓
    fetch() Request
        ↓
HuggingFace Space (KI + Deine Dokumente)
        ↓
JSON Response
        ↓
Chat auf der Webseite
```

**Kostenlos. Einfach. Skalierbar.**

---

## 🎯 Nächste Schritte

- [ ] HuggingFace Account erstellen (kostenlos)
- [ ] Neuen Space erstellen
- [ ] `app.py` + `requirements.txt` hochladen
- [ ] Space testen (Gradio UI)
- [ ] GitHub Pages aktivieren
- [ ] `index.html` mit Space URL updaten
- [ ] Deine Dokumente hinzufügen
- [ ] Fertig! 🚀

---

**Viel Erfolg mit GabeGPT!** 🤖
