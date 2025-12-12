# GabeGPT - Deployment Checklist

## ✅ SCHRITT FÜR SCHRITT

### Phase 1: HuggingFace Space Vorbereitung (15 min)

- [ ] HuggingFace Account erstellen: https://huggingface.co/join
- [ ] Neuen Space erstellen
  - Name: `gabegpt`
  - SDK: `Docker`
  - Visibility: `Public`
- [ ] Space Git-URL kopieren (Format: `https://huggingface.co/spaces/USERNAME/gabegpt`)
- [ ] Lokal klonen:
  ```bash
  git clone https://huggingface.co/spaces/USERNAME/gabegpt
  cd gabegpt
  ```

### Phase 2: Code ins Space hochladen (10 min)

- [ ] Kopiere folgende Dateien in den Space-Ordner:
  - `app.py`
  - `requirements.txt`

- [ ] Erstelle `documents/` Folder:
  ```bash
  mkdir documents
  ```

- [ ] Kopiere `documents/beispiel.txt`

- [ ] Git Commit & Push:
  ```bash
  git add .
  git commit -m "Init GabeGPT"
  git push
  ```

- [ ] Warte 5-10 Minuten bis Space deployed ist
- [ ] Teste Space unter: `https://USERNAME-gabegpt.hf.space`

### Phase 3: GitHub Pages Setup (10 min)

- [ ] GitHub Account erstellen (falls nicht vorhanden)
- [ ] Neues Repo erstellen: `gabegpt` oder `USERNAME.github.io`
- [ ] Öffne Repo Einstellungen → Pages
- [ ] Source: `main` Branch → `root folder`
- [ ] Save

### Phase 4: Frontend hochladen (5 min)

- [ ] Kopiere `index.html` in GitHub Repo

- [ ] **WICHTIG:** Öffne `index.html` und ändere Zeile 125:
  ```javascript
  const HUGGINGFACE_SPACE_URL = 'https://USERNAME-gabegpt.hf.space';
  ```
  (Deine echte Space URL!)

- [ ] Commit & Push:
  ```bash
  git add index.html
  git commit -m "Add chatbot frontend"
  git push
  ```

- [ ] GitHub Pages ist live unter:
  ```
  https://USERNAME.github.io/gabegpt
  ```

- [ ] Öffne die URL und teste Chat!

### Phase 5: Optimierung (Optional)

- [ ] **System Prompt anpassen**: `app.py` Zeile 16-19
  ```python
  SYSTEM_PROMPT = """Deine Anleitung hier..."""
  ```

- [ ] **Modell wechseln**: `app.py` Zeile 10
  Optionen:
  - `meta-llama/Llama-2-7b-chat-hf` (beste Qualität)
  - `mistralai/Mistral-7B-Instruct-v0.1` (schnell)
  - `microsoft/phi-3-mini-4k-instruct` (extrem schnell)

- [ ] **Eigene Dokumente hochladen**:
  - Platziere TXT-Dateien im `documents/` Ordner
  - Push zu HuggingFace
  - Bot nutzt sie automatisch!

### Phase 6: Debugging (Falls es nicht funktioniert)

**Problem: Space lädt nicht**
- [ ] Öffne HF Space → Settings → Logs
- [ ] Suche nach Python-Errors
- [ ] Prüfe ob alle Dependencies in `requirements.txt` sind

**Problem: Chat funktioniert nicht**
- [ ] Öffne Browser Console: `F12`
- [ ] Tab "Network" ansehen
- [ ] Prüfe Request zu HuggingFace Space
- [ ] CORS-Fehler? Space muss public sein!

**Problem: Langsame Antworten**
- [ ] Space könnte überlastet sein
- [ ] Wechsel zu kleinerem Modell: `microsoft/phi-3-mini-4k-instruct`
- [ ] Oder nutze HuggingFace Inference API (kostenlos)

---

## 🚀 FERTIG!

Dein kostenloses KI-Chatbot-System läuft jetzt:
- Frontend: GitHub Pages (0€/Monat)
- Backend: HuggingFace Spaces (0€/Monat)
- Datenspeicher: GitHub + HF (0€/Monat)

**Gesamtkosten: 0€** ✅

---

## 📌 Nützliche Links

- HuggingFace Spaces: https://huggingface.co/spaces
- GitHub Pages Docs: https://pages.github.com
- Verfügbare Modelle: https://huggingface.co/models?pipeline_tag=text-generation
- Dokumentation RAG: https://www.pinecone.io/learn/retrieval-augmented-generation/
