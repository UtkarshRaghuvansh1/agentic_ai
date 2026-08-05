# RAG — Retrieval Augmented Generation

RAG lets an LLM answer questions using **your own data** (PDFs, URLs, code)
instead of only its training knowledge. It **retrieves** relevant info first,
then **generates** an answer grounded in it.

---

## Why RAG?
- LLMs have a **knowledge cutoff** and don't know your private data.
- LLMs have a **context limit** — you can't paste a 1000-page PDF at once.
- RAG fetches only the **relevant chunks** and feeds them to the model.

---

## Part 1 — Indexing (prepare your data)

Done once, to make your data searchable.

### Step 1 — Data Ingestion (Load)
- Load your source data: **PDF, URL, code, text**, etc.

### Step 2 — Data Transformation (Split)
- Break the data into small **chunks**.
- **Why:** LLMs have a context-size limit — large files can't be processed at
  once, so we split them.

### Step 3 — Embedding
- Convert each text chunk into a **vector** (list of numbers).
- **Why:** enables **similarity search** — finding text by meaning, not keywords.

### Step 4 — Vector Store (Store)
- Save the vectors in a **vector database**.
- Examples: **Chroma DB, FAISS, Astra DB**.

```text
Load → Split → Embed → Store
PDF    chunks   vectors  vector DB
```

---

## Part 2 — Retrieval + Generation (answer queries)

Runs every time a user asks a question.

### Step 5 — User Query
1. User asks a **question**.
2. The **Retriever** searches the vector store using **similarity search** and
   pulls the most relevant chunks.
3. A **Prompt** combines: system instructions + retrieved context + the question.
4. The **LLM** reads it and produces a grounded **Answer**.

```text
Question → Retrieve (vector DB) → Prompt → LLM → Answer
```

---

## Key Terms

| Term | Meaning |
|------|---------|
| **Chunking** | Splitting data into small pieces |
| **Embedding** | Turning text into vectors (numbers) |
| **Vector Store** | DB that holds vectors (Chroma, FAISS, Astra) |
| **Similarity Search** | Finding chunks closest in meaning to the query |
| **Retrieval Chain** | The interface that queries the vector store |
| **Prompt** | System instructions + context + question sent to the LLM |

---

## The full