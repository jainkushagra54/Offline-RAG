# 🦙 Offline RAG — Local Document Q&A System

A fully offline Retrieval-Augmented Generation (RAG) pipeline that lets you query your own PDF documents using a local LLM (via Ollama) and HuggingFace embeddings — no OpenAI key required.

---

## 📁 Project Structure

```
OFFLINE RAG/
├── data/                      # Place your PDF files here
├── chroma/                    # Auto-generated vector database (ChromaDB)
├── .env                       # Your API keys (never commit this!)
├── get_embedding_function.py  # HuggingFace embedding setup
├── populatedb.py              # Ingests PDFs and builds the vector store
├── query_data.py              # Query the vector store using a local LLM
└── requirements.txt           # Python dependencies
```

---

## 🧰 Tech Stack

| Component | Tool |
|---|---|
| LLM (local) | [Ollama](https://ollama.com) + Mistral |
| Embeddings | HuggingFace `sentence-transformers/all-MiniLM-L6-v2` |
| Vector Store | [ChromaDB](https://www.trychroma.com/) |
| PDF Loader | LangChain `PyPDFDirectoryLoader` |
| Framework | [LangChain](https://www.langchain.com/) |

---

## ⚙️ How It Works

1. **Populate** — PDFs are loaded, split into chunks, embedded via HuggingFace, and stored in ChromaDB
2. **Query** — Your question is embedded, similar chunks are retrieved, and Ollama (Mistral) generates an answer grounded in those chunks

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- [Ollama](https://ollama.com) installed
- A free [HuggingFace account](https://huggingface.co/settings/tokens) for the API token

### 1. Clone the repository

```bash
git clone  https://github.com/jainkushagra54/offline-rag.git
cd offline-rag
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Pull the Mistral model via Ollama

```bash
ollama pull mistral
```

### 4. Create a `.env` file in the project root

```
HF_TOKEN=hf_your_huggingface_token_here
```

### 5. Add your PDFs to the `data/` folder

```
OFFLINE RAG/
└── data/
    ├── document1.pdf
    └── document2.pdf
```

### 6. Populate the vector database

```bash
python populatedb.py
```

To reset and rebuild from scratch:

```bash
python populatedb.py --reset
```

### 7. Query your documents

```bash
python query_data.py "Your question here"
```

Example:

```bash
python query_data.py "What is the refund policy?"
```

---

## 🔒 Environment Variables

| Variable | Description |
|---|---|
| `HF_TOKEN` | HuggingFace API token for generating embeddings |

> ⚠️ Never commit your `.env` file to GitHub.

---

## 📦 Dependencies

```
langchain
langchain-community
langchain-huggingface
langchain-text-splitters
chromadb
pypdf
python-dotenv
ollama
boto3
pytest
```

---

## 🙈 .gitignore

Add this `.gitignore` to your project before pushing:

```
.env
chroma/
__pycache__/
*.pyc
```

---

## 📝 License

MIT License — free to use and modify.