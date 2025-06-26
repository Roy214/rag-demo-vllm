# RAG Demo with vLLM + Quantized Mistral + LangChain

This project is a minimal implementation of **Retrieval-Augmented Generation (RAG)** assistant using:

* `vllm.pdf` as the knowledge base
*  Local embeddings via Sentence Transformers
*  Fast vector search with FAISS
*  Local quantized **Mistral** model via [Ollama](https://ollama.com/)
*  LangChain for retrieval orchestration

---

## Quick Start

### 1. Clone the Repo

```bash
git clone git@github.com:Roy214/rag-demo-vllm.git
cd rag-demo-vllm
```

### 2. Set Up the Environment

```bash
pip install -r requirements.txt
```

Or with `uv`:

```bash
uv pip install -r requirements.txt
```

---

### 3. Download the Embedding Model Locally

Only needed once:

```python
from sentence_transformers import SentenceTransformer
model = SentenceTransformer('sentence-transformers/all-MiniLM-L6-v2')
model.save('./local_models/all-MiniLM-L6-v2')
```

---

### 4. Start the Ollama Server

Install and run [Ollama](https://ollama.com):

```bash
ollama pull mistral
ollama serve
```

---

### 5. Run the Script

```bash
python main.py
```

 It will:

* Load `vllm.pdf`
* Embed and index the content with FAISS
* Query it using your local Mistral model
* Return short, precise answers

---

##  Sample Q\&A

```bash
 Question: What is main benefit of PageAttention in vLLM?

 Answer: PagedAttention enables efficient memory management in vLLM by virtualizing the KV cache.
```

---

##  .gitignore Notice

This repo ignores large/local files:

* `local_models/`
* FAISS index files (`*.faiss`, `*.pkl`)
* `*.pdf`

Make sure you regenerate or manually place these files in your local env.

---

## Project Structure

```
rag-demo-vllm/
├── main.py                 # RAG pipeline: load, embed, query
├── requirements.txt
├── vllm.pdf                # Source document (gitignored)
├── local_models/           # Local embedding model (gitignored)
├── vllm_faiss_index/       # FAISS vectorstore (gitignored)
└── README.md
```

---

##  Requirements

* Python 3.9+
* `ollama` (for running quantized Mistral locally)
* Internet access (first run only for models)

---


