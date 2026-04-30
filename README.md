# Smart Civilian — Windows Setup Guide

Complete step-by-step setup for a fresh Windows laptop.

---

## Prerequisites — Install These First

### 1. Python 3.11+
1. Go to https://www.python.org/downloads/
2. Download **Python 3.11** or **3.12** (click the latest release)
3. Run the installer — **IMPORTANT: check "Add python.exe to PATH"** at the bottom before clicking Install
4. Verify in a new terminal:
   ```cmd
   python --version
   ```

### 2. Node.js 18+
1. Go to https://nodejs.org/
2. Download the **LTS** version
3. Run the installer with default settings
4. Verify:
   ```cmd
   node --version
   npm --version
   ```

### 3. pnpm
Open Command Prompt or PowerShell and run:
```cmd
npm install -g pnpm
```
Verify:
```cmd
pnpm --version
```

### 4. Git
1. Go to https://git-scm.com/download/win
2. Download and install with default settings
3. Verify:
   ```cmd
   git --version
   ```

---

## Step 1 — Clone the Repository

Open **Command Prompt** or **PowerShell**:

```cmd
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
```

> Replace `YOUR_USERNAME/YOUR_REPO_NAME` with the actual GitHub repo URL.

---

## Step 2 — Backend Setup (Python / FastAPI)

### 2a. Create virtual environment

```cmd
cd rag_backend
python -m venv .venv
```

### 2b. Activate the virtual environment

```cmd
.venv\Scripts\activate
```

You should see `(.venv)` at the start of your prompt. **You must run this every time you open a new terminal before starting the backend.**

### 2c. Install Python dependencies

```cmd
pip install -r requirements.txt
```

This installs FastAPI, Pinecone, sentence-transformers, python-docx, and all other packages. It may take 3–5 minutes the first time (downloads the embedding model).

### 2d. Create the .env file

In the `rag_backend` folder, create a new file called `.env` (no extension):

```cmd
copy .env.example .env
```

Then open `.env` in Notepad or VS Code and fill in your values:

```env
# Pinecone
PINECONE_API_KEY=your-pinecone-api-key-here
PINECONE_INDEX_NAME=is456-slab-design

# LLM provider — use "gemini" (recommended) or "ollama"
LLM_PROVIDER=gemini

# Gemini (get key from https://aistudio.google.com/app/apikey)
GEMINI_API_KEY=your-gemini-api-key-here
GEMINI_MODEL=gemini-2.5-flash

# Embedding model (downloaded automatically from HuggingFace)
EMBEDDING_MODEL=sentence-transformers/all-MiniLM-L6-v2

# Document paths (relative to rag_backend/)
PDF_PATH=../is.456.2000 (1).pdf
EXTRA_DOCUMENT_PATHS=../Dataset.docx,../Research and History Main.docx
```

### 2e. Run the backend

Make sure your virtual environment is still activated (you see `(.venv)`), then:

```cmd
python -m uvicorn main:app --reload --port 8000
```

You should see:
```
INFO:     Uvicorn running on http://127.0.0.1:8000
INFO:     Application startup complete.
```

Test it — open your browser and go to: **http://localhost:8000/health**

You should see: `{"status":"ok","service":"smart-civilian-rag"}`

---

## Step 3 — Frontend Setup (Next.js)

Open a **second** Command Prompt or PowerShell window (keep the backend running in the first one).

```cmd
cd smart_civilian
pnpm install
```

This installs all Node.js packages. First time takes 2–4 minutes.

Then start the frontend:

```cmd
pnpm dev
```

You should see:
```
▲ Next.js 15.x.x
- Local: http://localhost:3000
```

Open your browser and go to: **http://localhost:3000**

---

## Step 4 — Ingest Documents (First Time Only)

This step uploads your documents to Pinecone. Only needs to be done **once** per Pinecone index.

In the `rag_backend` terminal (with `.venv` activated):

```cmd
python ingest.py
```

You should see it process the PDF and both DOCX files, ending with:
```
Ingestion complete! Processed 3 document(s).
```

> **Skip this step** if someone else on the team has already ingested into the same Pinecone index.

---

## Running the Project Every Day

You need **two terminals** open:

**Terminal 1 — Backend:**
```cmd
cd path\to\project\rag_backend
.venv\Scripts\activate
python -m uvicorn main:app --reload --port 8000
```

**Terminal 2 — Frontend:**
```cmd
cd path\to\project\smart_civilian
pnpm dev
```

Then open **http://localhost:3000** in your browser.

---

## Troubleshooting

### `python` not found
Re-install Python and make sure to check **"Add python.exe to PATH"**. Then restart your terminal.

### `pnpm` not found after installing
Close and reopen your terminal. If still not found, try:
```cmd
npm install -g pnpm
```

### `.venv\Scripts\activate` gives an error about execution policy
Run this once in PowerShell as Administrator:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### `pip install` fails on `sentence-transformers`
Make sure you have Microsoft Visual C++ Build Tools. Download from:
https://visualstudio.microsoft.com/visual-cpp-build-tools/
Select "Desktop development with C++" during install.

### Backend starts but returns errors about Pinecone
Check that your `PINECONE_API_KEY` in `.env` is correct and the index name matches exactly: `is456-slab-design`.

### Port 8000 already in use
Find and kill the process:
```cmd
netstat -ano | findstr :8000
taskkill /PID <PID_NUMBER> /F
```

### Port 3000 already in use
```cmd
netstat -ano | findstr :3000
taskkill /PID <PID_NUMBER> /F
```

---

## Project Structure (Quick Reference)

```
clg/
├── rag_backend/          ← Python AI backend (run on port 8000)
│   ├── main.py           FastAPI endpoints
│   ├── rag_chain.py      RAG logic + Gemini calls
│   ├── retriever.py      Pinecone search
│   ├── ingest.py         One-time document upload
│   ├── requirements.txt  Python dependencies
│   └── .env              Your API keys (never commit this!)
│
├── smart_civilian/       ← Next.js frontend (run on port 3000)
│   └── src/
│       ├── app/page.tsx            Chat interface
│       └── components/
│           └── Slab3DViewer.tsx    3D slab visualization
│
├── is.456.2000 (1).pdf   IS 456:2000 standard document
├── Dataset.docx          Engineering dataset
└── Research and History Main.docx  Research content
```

---

## API Keys You Need

| Service | Where to Get | Used For |
|---|---|---|
| Pinecone | https://app.pinecone.io | Vector database (stores document embeddings) |
| Gemini | https://aistudio.google.com/app/apikey | AI language model (generates answers) |

Both have free tiers sufficient for this project.
